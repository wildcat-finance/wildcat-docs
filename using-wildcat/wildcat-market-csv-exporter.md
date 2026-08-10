---
description: A downloadable Claude skill which exports and checks a Wildcat market's complete on-chain transaction history.
---

# Wildcat Market CSV Exporter

The **Wildcat Market CSV Exporter is a Claude skill**, not a feature built into the Wildcat app.

Give Claude the Ethereum mainnet address of a Wildcat market and the skill builds three files:

* A transaction ledger covering deposits, borrowing, repayments, queued and executed withdrawals, fees and other asset movements
* A row-by-row record of every decoded market event
* A quarantine file for unrelated or potentially malicious token transfers which would otherwise pollute the market's explorer history

Claude then checks the export against independent on-chain data. This includes an exact reconciliation between the ledger's net asset flow and the market's underlying-asset balance at the chosen snapshot block.

{% file src="wildcat-market-csv.skill" %}

## Using the CSVs

The skill gives you an auditable transaction history, not a finished annual accounting statement. Once the CSVs exist, we have found that either Fable or Sol can derive follow-up reports, including annual borrowing, repayment and interest figures, without much fuss.

These are still raw protocol records rather than certified financial or tax reports. You may need an accountant or another suitable provider to review anything used for formal reporting.

## Requirements

The skill needs Python 3.10 or later, an Ethereum archive-node RPC endpoint and an Etherscan API key.

If those last two are new to you:

* `RPC_URL` is the URL Claude uses to read Ethereum data. [Alchemy](https://www.alchemy.com/docs/what-is-archive-data-on-ethereum) is one place to create an Ethereum mainnet endpoint with archive access. Other providers are fine, but check that the endpoint serves historical archive data rather than current state alone.
* `ETHERSCAN_API_KEY` lets the exporter request transaction and contract data from Etherscan. Create an Etherscan account, then add a key from its API Dashboard by following the [Etherscan getting-started guide](https://docs.etherscan.io/getting-started).

They are separate credentials. Put the RPC URL in `RPC_URL` and the Etherscan key in `ETHERSCAN_API_KEY` within a local `.env` file. Never commit that file or include either value in an exported CSV.
