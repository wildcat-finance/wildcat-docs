---
description: Downloadable Agent Skill for ChatGPT and Claude which exports, verifies and analyses a Wildcat market's complete on-chain history.
---

# Wildcat Market CSV Exporter

The **Wildcat Market CSV Exporter is a downloadable Agent Skill for ChatGPT and Claude**. It is not a feature built into the Wildcat app.

Give the agent the Ethereum mainnet address of a Wildcat market and it reconstructs the market's history at a fixed snapshot block. The standard export contains:

* A transaction ledger covering deposits, borrowing, repayments, queued and executed withdrawals, fees and other underlying-asset movements
* A row-by-row record of every decoded market event
* A quarantine file for unrelated or potentially malicious token transfers which would otherwise pollute the market's explorer history

The skill can also produce lender position reports. These split withdrawals and lender-to-lender transfers between principal and interest under FIFO, LIFO and pro-rata accounting conventions.

{% file src="wildcat-market-csv.skill" %}

The standard files are `<SYMBOL>_transactions.csv`, `<SYMBOL>_events.csv` and `<SYMBOL>_spam_token_transfers_excluded.csv`. Position analysis adds `<SYMBOL>_interest_allocations_<method>.csv`, with one row per executed withdrawal or lender transfer, and `<SYMBOL>_position_analytics_<method>.csv`, with one row per lender.

## How the Export Is Built

No single source contains the complete history. The skill joins three:

1. Archive-node `eth_getLogs` results provide every event emitted by the market, including transactions routed through intermediary contracts which do not appear in an explorer's direct account history.
2. Etherscan's transaction list adds failed or reverted direct transactions, which emit no logs, and supplies readable method names.
3. Etherscan's token-transfer list adds movements of the underlying asset which have no matching market event, including direct transfers and excess assets returned when a market closes.

Transfers emitted by unrelated token contracts are kept out of the ledger. Scam airdrops can mention the market address and imitate very large stablecoin movements, so the skill writes those records to the separate quarantine CSV instead.

The fetch is resumable. It caches raw results and log-scan checkpoints, so an interrupted run can continue without starting again from the deployment block.

## What the Verification Proves

The export is checked against data fetched independently of the original reconstruction. The verifier compares the event history with Etherscan's logs API, checks a sample of transaction receipts and reads contract state at the same snapshot block.

The central invariant is exact, not approximate:

`deposited + repaid + untracked_asset_in - borrowed - withdrawal_executed - fees_collected - escrowed_out - untracked_asset_out = balanceOf(market)`

Queued withdrawals are deliberately absent from the outflow side. Queueing creates a claim but does not send cash out of the market; the asset leaves only when the withdrawal executes. The verifier requires the ledger's resulting balance to equal the underlying token's on-chain `balanceOf(market)` in raw integer units.

The skill does not deliver an export if these checks fail. A stale cache, an RPC endpoint without archive data or a newly introduced event which the exporter does not yet understand all require investigation rather than an accounting guess.

## Lender Principal and Interest

Wildcat market tokens rebase as interest accrues. A lender's visible token balance therefore blends deposited principal with accrued interest, while the contract tracks scaled units beneath it. The chain records the position and its value, but it does not record which historical deposit should count as the principal disposed of when a lender transfers tokens or requests a withdrawal.

FIFO, LIFO and pro-rata answer that reporting question differently:

| Method | Principal selected when scaled units leave a position |
| --- | --- |
| FIFO | The oldest acquired units are used first |
| LIFO | The newest acquired units are used first |
| Pro-rata | Principal is taken from the blended position in proportion to the scaled units disposed of |

These are accounting conventions applied by the report, not facts asserted by the contract and not tax advice. If no method has been chosen, the skill runs all three so the effect of the policy is visible.

### A Worked Example

Suppose a lender makes two deposits into the same market:

1. They deposit 100 USDC when the scale factor is 1.0 and receive 100 scaled units. That lot has 100 USDC of principal.
2. Later, when the scale factor is 1.5, they deposit 150 USDC and receive another 100 scaled units. That lot has 150 USDC of principal.

When the scale factor reaches 2.0, the lender holds 200 scaled units worth 400 USDC. Their total principal is 250 USDC and their total accrued interest is 150 USDC.

They then queue 100 scaled units. Assume the batch is fully funded at that point and later pays 200 USDC. The three methods split the same payout as follows:

| Method | Principal returned | Interest realised | Principal left active | Unrealised interest left active |
| --- | ---: | ---: | ---: | ---: |
| FIFO | 100 USDC | 100 USDC | 150 USDC | 50 USDC |
| LIFO | 150 USDC | 50 USDC | 100 USDC | 100 USDC |
| Pro-rata | 125 USDC | 75 USDC | 125 USDC | 75 USDC |

Nothing economic changes between the rows. In every case the lender has earned 150 USDC in total: the method only moves that amount between realised interest on the payout and unrealised interest in the remaining position.

The implementation performs this calculation in raw token units. When a partial lot must be split, integer rounding stays in the remaining lot so the principal identity continues to reconcile exactly.

## Queued Withdrawals

Queueing a withdrawal moves the chosen scaled units and their allocated principal out of the lender's active lots and into a pending claim. It does **not** realise principal or interest, because the lender has not received any underlying asset.

A batch can contain both funded and unfunded value:

* The funded, unclaimed part has been set aside in the unclaimed-withdrawals pool. It no longer accrues interest.
* The unfunded part remains a scaled claim. Its value continues to grow with the market's scale factor until those scaled units are burned by a batch payment.

If the batch is funded or claimed in stages, the skill allocates principal cumulatively. Each executed payment receives its proportion of the claim's original principal; the remainder stays pending. Interest becomes cash-realised only when `WithdrawalExecuted` records the payout.

This distinction also matters in the transaction ledger: `withdrawal_queued` records the claim, while `withdrawal_executed` records the underlying asset leaving the market.

## Transfers Between Lenders

For the sender, a transfer is another disposal of scaled units. FIFO, LIFO or pro-rata selects the principal attached to those units, and the difference between their market-token value and that principal is reported as `transfer_interest`.

That figure is economic value embodied in the transfer, not cash received by the sender. The recipient starts a new lot with principal basis equal to the market-token value at the time of transfer; they do not inherit the sender's historical basis.

## Realised and Unrealised Interest

The position report separates earnings into four places:

* `cash_realized_interest`: interest included in executed withdrawal payments
* `transfer_interest`: interest included in market tokens sent to another lender
* `active_unrealized_interest`: current on-chain value of active market tokens less their remaining principal
* `pending_unrealized_interest`: current value of queued claims less their remaining principal

The spelling of the CSV field names follows the scripts. In the report's accounting, only an executed withdrawal produces cash-realised interest. A transfer is shown separately, and a queued claim remains unrealised until paid.

## Position Checks

For delivered analytics, the skill reads `balanceOf`, `scaledBalanceOf` and `currentState` at the export's pinned snapshot block. It refuses to write the reports if the event-by-event walk does not reproduce a lender's on-chain scaled balance.

The interest verifier then checks every result in raw units:

* Every disposal satisfies `value = allocated principal + allocated interest`.
* Every lender satisfies `deposits + transfer basis in = active principal + pending principal + cash principal returned + principal transferred out`.
* Total economic earnings equal cash-realised interest, transfer interest, active unrealised interest and pending unrealised interest added together.
* Disposal rows roll up exactly to the corresponding position totals.
* Every allocated address has one position summary produced from snapshot RPC data.
* Total economic earnings are identical under FIFO, LIFO and pro-rata, even though the realised and unrealised split differs.

Offline estimates are useful for test fixtures, but the skill does not accept them for an accounting, audit or other delivered result.

## Using the Files

The standard transaction and event CSVs are an independently checked protocol history, not a finished annual accounting statement. The optional position files add a transparent cost-basis convention, but they remain reports derived from on-chain records rather than certified financial or tax accounts.

Once the CSVs exist, Fable or Sol can help derive further reports such as annual borrowing and repayment figures. Anything used for formal reporting may still need review by an accountant or another suitable provider, with the chosen FIFO, LIFO or pro-rata convention stated explicitly.

## Requirements

The skill needs Python 3.10 or later, an Ethereum archive-node RPC endpoint and an Etherscan API key.

If those last two are new to you:

* `RPC_URL` is the URL the skill uses to read Ethereum data. [Alchemy](https://www.alchemy.com/docs/what-is-archive-data-on-ethereum) is one place to create an Ethereum mainnet endpoint with archive access. Other providers are fine, but check that the endpoint serves historical archive data rather than current state alone.
* `ETHERSCAN_API_KEY` lets the exporter request transaction and contract data from Etherscan. Create an Etherscan account, then add a key from its API Dashboard by following the [Etherscan getting-started guide](https://docs.etherscan.io/getting-started).

They are separate credentials. Put the RPC URL in `RPC_URL` and the Etherscan key in `ETHERSCAN_API_KEY` within a local `.env` file. Never commit that file or include either value in an exported CSV.
