---
name: wildcat-protocol
description: >-
  Comprehensive reference for the Wildcat Protocol — a decentralised, fixed-rate,
  UNDERCOLLATERALISED on-chain credit protocol (live on Ethereum mainnet and Plasma).
  Use this skill whenever a question touches Wildcat: creating or using markets,
  borrowers and lenders, market/debt tokens and the scale factor, capacity, reserve
  ratio, base/penalty/protocol APR, delinquency, withdrawal cycles/claims and the
  withdrawal queue, hooks and role providers, access control and "known lenders",
  the sanctions sentinel and escrow, the ERC-4626 wrapper, optional collateral,
  protocol fees, contract addresses/deployments, audits/SphereX/security, the Master
  Loan Agreement, or anything under docs.wildcat.finance. Covers borrower and lender
  workflows, technical/contract internals, and security/legal pointers.
---

# Wildcat Protocol

## What Wildcat is (read this first)

Wildcat is a decentralised protocol for **fixed-rate, undercollateralised borrowing and lending**, live on **Ethereum mainnet** and **Plasma** (with a Sepolia testnet). A **borrower** deploys a permissioned on-chain **market** — a single credit facility with fully customisable terms — and **lenders** deposit an ERC-20 asset into it in exchange for a rebasing **market token** (a debt token) that grows with interest.

Wildcat is deliberately **hands-off**: it is a settlement layer that does **not** assess borrower creditworthiness, custody funds, set rates, or insure against default. Lenders carry full counterparty risk. The protocol's own description is "an Uatu the Watcher figure: interested, watching, but it will not and cannot interfere."

The current generation is **V2**. V1 is deprecated (its docs survive only for historical/audit reference). When answering, assume V2 unless told otherwise.

Three audiences use the docs, and most questions fall into one: **users/researchers** (how do I borrow/lend?), **auditors/developers** (how does the code behave?), and **lawyers/regulators** (terms, risk, sanctions, MLA).

**Canonical sources** (cite these, don't guess):
- Docs: https://docs.wildcat.finance — and the curated index `llms.txt` at the docs root.
- App: https://app.wildcat.finance (testnet: https://testnet.wildcat.finance) · Landing: https://wildcat.finance
- Code: https://github.com/wildcat-finance/v2-protocol · Whitepaper v2.0: https://github.com/wildcat-finance/wildcat-whitepaper/blob/main/whitepaper_v2.0.pdf
- Borrower onboarding contact: contact@thewildcat.foundation · Notifications bot: https://t.me/wildcat_notifications_bot

> When you state a specific number, address, or rule, prefer linking the relevant docs page (see the routing table at the end). Facts in this skill are accurate as of the V2 docs but parameters and deployments can change — verify live values (e.g. fees, addresses) against the docs or chain when precision matters.

## Mental model

- A **market** is one borrower's loan. It has a base APR, a capacity, a reserve ratio, a penalty APR, a grace period, a withdrawal-cycle length, an access policy (hooks), and optionally a fixed term and a Master Loan Agreement.
- **Capacity** (`maxTotalSupply`) is the most a borrower wants to *owe interest on*; it is **not** how much they can borrow. The **reserve ratio** is the fraction of outstanding supply that must stay liquid in the market. Borrowable amount ≈ supply × (1 − reserveRatio).
- **Market tokens rebase.** A lender who deposits 1,000 of the asset into a 10% market holds ~1,100 market tokens a year later, redeemable ~1:1 for the asset *if the borrower repays*. This is driven by the **scale factor** (see below), not an internal exchange rate — balances themselves grow.
- **Withdrawals are not instant.** A lender files a **withdrawal request**, waits out a **withdrawal cycle**, then **claims**. It is always a two-transaction, cross-cycle process. If many lenders exit at once, claims are **pro-rata**.
- **Delinquency** is when a market holds less than its required reserves/collateral obligation. Stay delinquent past the **grace period** and the **penalty APR** kicks in.
- **Access is gated by hooks.** Lenders need a **credential** from a **role provider** to deposit. Anyone who has deposited (or received market tokens) while holding a valid credential becomes a **known lender** and can always withdraw.
- **Sanctions** are handled by the **sentinel** + Chainalysis oracle, which can quarantine a flagged lender's funds into an **escrow** contract.

## Core terminology (condensed)

The full glossary is at docs.wildcat.finance/using-wildcat/terminology. Highest-value terms:

- **Archcontroller** — registry + permission gate. Wildcat operators add/remove borrowers; it records all factories, hooks and markets. Removing a borrower stops *new* deployments but cannot force-close existing markets.
- **Base APR** — interest accruing to lenders (set by borrower; fixed at any instant, adjustable stepwise).
- **Penalty APR** — extra rate (0–100%) applied while a market has been delinquent longer than its grace period. Never accrues to the protocol; only to lenders.
- **Protocol APR / fee** — a fraction of base APR accruing to Wildcat, charged *on top of* the lender rate (not subtracted from it).
- **Capacity** — `maxTotalSupply`; deposit ceiling. Can be exceeded by interest accrual.
- **Reserve ratio** — % of outstanding supply that must remain liquid (0–100%). Falling below ⇒ delinquency.
- **Grace period / grace tracker** — allowed delinquency time before penalty (rolling; 0–2160 hours / 90 days). The tracker counts up while delinquent and down while healthy.
- **Delinquency** — market assets < collateral obligation.
- **Market token** — rebasing ERC-20 representing a 1:1 (rebasing) claim on the underlying; name/symbol = borrower prefix + underlying name/symbol.
- **Scale factor** — ray (1e27) ratio between scaled tokens (shares) and market tokens (value); grows with compounding interest.
- **Withdrawal cycle** — wait between a withdrawal "wave" starting and assets becoming claimable. Non-rolling. Zero is allowed.
- **Unclaimed withdrawals pool** — assets earmarked for withdrawal; out of the borrower's reach, not interest-bearing, excluded from reserve ratio.
- **Withdrawal queue** — FIFO of expired/unfulfilled withdrawal batches; repayments fill the oldest first.
- **Known lender** — deposited or received market tokens while holding a valid deposit credential; permanently retains the right to file withdrawals (unless fixed-term or sanctioned).
- **Hook / hook instance / hooks template** — code run on market actions; an instance (a.k.a. **policy**) is deployed from a template and configured per market.
- **Role provider** — contract granting deposit credentials per arbitrary rules ("pull" = queryable by address; "push" = explicitly grants). Credentials may carry a TTL.
- **Sentinel / escrow** — sanctions checker (Chainalysis) and the quarantine contract it can deploy.
- **Underlying asset** — any ERC-20 the borrower wants to borrow. **Rebasing assets (e.g. stETH) break the interest model — never use them.**

## Borrower lifecycle

1. **Onboard.** Currently only registered legal entities. Contact the Wildcat Foundation (contact@thewildcat.foundation); pass KYB/C; provide an Ethereum address that is registered on the archcontroller, granting the ability to deploy hooks instances and markets.
2. **Create a market** (every parameter is a degree of freedom):
   - **Policy / hooks**: reuse or create a policy; choose **Open Term** (withdrawals anytime) or **Fixed Term** (no withdrawals / no base-APR cuts until maturity; optional flags for early termination and maturity reduction; maturity ≤ 1 year out, reducible only). Choose access: **Lender Self-Onboarding** (anyone not OFAC-sanctioned per Chainalysis) or **Borrower-Operated Allowlist**.
   - **Asset & token identity**: underlying ERC-20 (use the token address on mainnet — ticker search is ambiguous); market-token name/symbol prefix.
   - **Terms**: maximum borrowing capacity; base APR; penalty APR (0–100%, non-zero encouraged); reserve ratio (0–100%); grace period (0–2160h); withdrawal cycle (0–2160h); minimum deposit (default 0).
   - **Lender restrictions**: Restrict Withdrawals (strongly recommended), Restrict Transfers, or Disable Transfers (token transferability = Open / Restricted / Disabled).
   - **Loan agreement**: attach the Wildcat **Template MLA** (borrower pre-signs; lenders countersign on deposit) or explicitly decline (still signed, for the record). MLAs cannot currently be added retroactively.
   - Confirm and **deploy** (ECDSA-sign the MLA/refusal; Safe multisig signers must stay available; testnet needs two txs).
3. **Source deposits.** For allowlist markets, add lender addresses on-chain via Edit Policy. Wildcat does not source capital but may advertise markets.
4. **Borrow.** Up to capacity × (1 − reserveRatio) when full. **Do not borrow to the limit** — the next state update will tip the market into delinquency. Protocol fees accrue as required reserves over time.
5. **Repay.** Just ERC-20 transfer assets back to the market — *anyone* can repay (in case the borrower key is compromised). Or repay N days of anticipated interest.
6. **Adjust APR.** Increases are unconstrained. A **decrease of ≤25% of current APR per two-week window** is free; a larger cut temporarily raises required reserves by twice the proportional reduction for two weeks, giving lenders a **ragequit** window. (Not allowed while a withdrawal-blocking hook is active.)
7. **Alter capacity / minimum deposit / maturity.** Capacity up or down at will (setting below current debt just blocks new deposits). Minimum deposit adjustable (set above capacity to halt deposits). Fixed-term maturity can only be brought *closer*.
8. **Terminate.** A special APR reduction: repay enough to reach a 100% reserve ratio; interest stops; no further borrowing/parameter changes; lenders exit via request+claim (the cycle wait is waived on closure).

## Lender lifecycle

1. **Find a market & onboard.** Self-onboarding (not OFAC-sanctioned) or borrower allowlist. Use a hardware wallet/multisig. Credentials may expire and need refreshing.
2. **Sign the MLA** if the market offers one (only wallet address + ECDSA signature are stored).
3. **Deposit.** Receive market tokens 1:1 at deposit time (e.g. 133.7 XYZ → 133.7 wildcatXYZ). Balances then **rebase** upward with interest. Becoming a depositor (or receiving tokens while credentialed) marks you a **known lender**.
4. **Withdraw** (two-step, across a cycle):
   - File a **withdrawal request**: market tokens move to the market; available reserves are moved into the **unclaimed withdrawals pool** by burning tokens 1:1; any excess becomes a **pending withdrawal**.
   - Wait out the **withdrawal cycle**.
   - **Claim**. If the pool can't cover all requests in the cycle, each lender claims **pro-rata** to their share; shortfalls are batched as **expired** and queued **FIFO**; later borrower repayments fill the oldest batches first. (Worked examples in the Lenders doc.)
5. **Transfer / wrap (optional).** Market tokens may be transferable (Open/Restricted/Disabled). The **ERC-4626 wrapper** converts the rebasing token into a stable-balance share (`v-<marketSymbol>`) for bridging, LPing or accounting.

## Delinquency & penalties

- A market is delinquent when total assets < **collateral obligation** =
  `100% of pending (unpaid) withdrawals + 100% of unclaimed (paid) withdrawals + reserveRatio × outstanding supply + accrued protocol fees`.
- The **grace tracker** counts up while delinquent, down while healthy. The penalty APR applies for every second the tracker exceeds the grace period — meaning a borrower effectively pays **2 seconds of penalty for every 1 second over** (once on the way up, once on the way down). Curing late does *not* extend penalties beyond that symmetric count.
- Large withdrawal requests can instantly push a market delinquent and temporarily *raise* the effective reserve ratio (pending withdrawals must be 100% collateralised). Borrowers should actively monitor requests and reserves.
- Interest auto-compounds at each state update (first stateful call per block). The three rates are `annualInterestBips` (to lenders), `delinquencyFeeBips` (penalty, to lenders), `protocolFeeBips` (to protocol, on top).

## Hooks, access control & known lenders

- V2 replaced V1's manual per-lender controller whitelisting with **hooks**: code gated in front of core functions. Ten functions are hookable: `deposit`(/`depositUpTo`), `queueWithdrawal`(/`queueFullWithdrawal`), `executeWithdrawal`(/`executeWithdrawals`), `transfer`(/`transferFrom`), `borrow`, `repay`(/`repayOutstandingDebt`/`repayDelinquentDebt`), `closeMarket`, `setMaxTotalSupply`, `nukeFromOrbit`, `setAnnualInterestAndReserveRatioBips`.
- Hooks are **reactive and restrictive only** — they can block or record an action but cannot change who receives a transfer, redirect funds, or force a withdrawal. Two exceptions: `setAnnualInterestAndReserveRatioBips` (the hook may modify the new APR/reserve values) and `queueWithdrawal` (hook sees post-expiry state). Callers can append an `extraData` calldata buffer (used for signatures/Merkle proofs).
- Two shipped templates: **AccessControlHooks** (open-term) and **FixedTermLoanHooks** (adds a `fixedTermEndTime` before which withdrawals are disallowed).
- **Role providers** grant credentials: `isPullProvider()`, `getCredential(address)`, `validateCredential(address,bytes)`, and push via `grantRole(address,uint32)`. Access resolution tries: existing unexpired credential → provided `hooksData` → refresh from pull providers → loop pull providers. Credentials carry a borrower-set TTL.
- A market deployed with a credential required for *withdrawal but not deposit*, and no role providers, can trap lenders (a documented known issue). The Wildcat frontend mitigates this by forcing deposit credentials on all markets it deploys.

## Sanctions & the sentinel

- The **sentinel** checks the Chainalysis sanctions oracle. If a **lender** is flagged, an **escrow** contract is deployed between borrower and lender — triggered by the lender attempting a withdrawal or anyone calling `nukeFromOrbit` (which forces the lender into a withdrawal). On execution, underlying assets go to the escrow, not the lender.
- Escrowed assets release via `releaseEscrow` only if the lender is no longer flagged, or the borrower calls `overrideSanction`. The oracle must actually return "sanctioned" for an escrow to be created — it can't be used arbitrarily.
- If the **borrower** is sanctioned, all their markets are considered irreparably poisoned; the archcontroller likely severs them (still functional on-chain but hidden from the UI, no new escrows). This is an off-chain legal problem — advise speaking to a lawyer.

## Fees

- Two forms: **origination** (paid at deployment) and **streaming** (a % of base APR accruing over supply). Borrowers cannot modify the protocol fee.
- At V2 launch the default was **5% streaming, 0 origination**, and streaming is **hard-capped at 10% of base APR**.
- Effective rate example: 10% base + 5% streaming ⇒ borrower pays **10.5%**; lenders still get the full 10%, the 0.5% accrues to the protocol (as required reserves, not into the rebasing token). Penalty APR is **not** subject to the fee (10% base + 20% penalty = 30.5%, not 31.5%).
- Protocol fees have **seniority** over lender claims: lenders withdraw only reserves net of accrued unpaid fees. In V2 the archcontroller owner can adjust active markets' fee config (streaming retroactively; origination not for existing markets).

## ERC-4626 wrapper

- Wraps a rebasing market token into a non-rebasing ERC-4626 share named `v-<marketSymbol>`. Share **count stays fixed**; share **value rises** as the scale factor grows.
- Any registered market can have **one** wrapper; either the borrower (at deployment) or any lender (later) can deploy it via `Wildcat4626WrapperFactory.createWrapper(market)`.
- It is a thin layer — same credit risk, same sanctions checks (same sentinel), same capacity limit. It does **not** touch the withdrawal queue: to reach the underlying asset you must **unwrap → market tokens → withdrawal request → batch expiry → claim**.
- Integrator notes: exchange rate is the market `scaleFactor`; helpers `assetsPerShareRay()` / `sharesPerAssetRay()` (ray, 1e27). Preview functions follow ERC-4626 rounding and may differ slightly from execution — don't use previews as exact assertions. Never transfer tokens directly to the wrapper (no shares minted).

## Optional collateral contracts

A borrower can deploy contract(s) holding *different* ERC-20 assets (e.g. WETH pledged against a USDC line) as liquidatable backing — making a market partially, fully, or over-collateralised. Pledged assets sit in stasis until either the market is terminated (borrower withdraws them) or it enters penalised delinquency (an approved executor liquidates the needed amount into the market's underlying). (Distinct from a borrower simply over-repaying the same asset.)

## Technical / contract reference

- **Scale factor math.** `scaleFactor` is a ray (1e27). `balanceOf` / `totalSupply` / `transfer` / `deposit` / `withdraw` use **normalized (market) amounts**; `scaledBalanceOf` / `scaledTotalSupply` return **scaled (share) amounts**. `marketAmount = scaledAmount × scaleFactor`. Deposits divide by the scale factor to mint shares; withdrawals burn `normalizedAmount / scaleFactor` shares. Each first-in-block update multiplies the scale factor by accrued interest. (Same model as Aave aTokens.) Math helpers live in `MathUtils.sol`.
- **Key structs** (see Protocol Structs): `MarketState` (isClosed, maxTotalSupply, accruedProtocolFees, normalizedUnclaimedWithdrawals, scaledTotalSupply, scaledPendingWithdrawals, pendingWithdrawalExpiry, isDelinquent, timeDelinquent, protocolFeeBips, annualInterestBips, reserveRatioBips, scaleFactor, lastInterestAccruedTimestamp), `MarketParameters`, `DeployMarketInputs`, `HooksTemplate`, `WithdrawalBatch`, `LenderStatus`, `FIFOQueue`. Generate them with `scripts/calculate_structs.py`.
- **Withdrawal batches** are Current / Unpaid / Paid; earlier batches get priority but an expiring current batch can be paid before older unpaid ones if liquidity covers both. Scaled tokens in a batch keep accruing interest (shared pro-rata) until burned on payment.
- **V1→V2 highlights:** market controllers removed in favour of borrower-controlled markets + hooks; arbitrary CREATE2 salts; sanctioned accounts forced into a withdrawal batch (not escrow-on-transfer) and reverting with `AccountBlocked`; transient-storage reentrancy guard; `setAnnualInterestAndReserveRatioBips` replaces separate setters; `closeMarket` borrower-callable.
- **Function/event/error signatures** are documented per contract under technical-overview/function-event-signatures (access, interfaces, market, spherex, plus HooksFactory, ArchController, Sanctions{Sentinel,Escrow}).

### Deployed addresses — Ethereum mainnet (V2)

| Contract | Address |
| --- | --- |
| MarketLens | `0xfDA5C5B96bb198D2fca1A01d759620B64Ae5afE7` |
| WildcatArchController | `0xfEB516d9D946dD487A9346F6fee11f40C6945eE4` |
| WildcatSanctionsSentinel | `0x437e0551892C2C9b06d3fFd248fe60572e08CD1A` |
| WildcatHooksFactory | `0xdd7dd3b5076cf89440d05585ff56d246386207be` |
| Wildcat4626WrapperFactory | `0xEA6DE11f8F3F83c79bD9d8Db5517fCFDf2Bb148a` |
| FixedTermHooks template | `0x7e49CabA6FB53CDc70CD98829731A2b8d76dfc36` |
| OpenTermHooks template | `0x4c62B4844C8371f321541E8d564A4B3896cEceC7` |
| WildcatFeeRecipient | `0x35A5D1bd68F3139971027b92c1eE9384A0708554` |

Also deployed on **Plasma mainnet**; **Sepolia** hosts testnet contracts. Always confirm current addresses at docs.wildcat.finance/technical-overview/contract-deployments.

## Security

- **Audits.** V2: independent review by alpeh_v (Aug 2024) + a $100k Code4rena competitive audit (Aug–Sep 2024; 1 high, 8 medium) with follow-up mitigation reviews. V1: alpeh_v review (Sep 2023) + a $60.5k Code4rena audit (Oct 2023).
- **SphereX** runtime protection wraps every external function, rejecting "exploit-shaped" transactions against a trained reference set while keeping normal access continuous. It is on-chain; losing SphereX's off-chain engine only costs the ability to update the reference set.
- **Bug bounty.** Immunefi, **V1 only** (up to $50k; Critical $7.5k–$10k). **No V2 bounty is active yet.**
- **Known issues** are explicitly catalogued (closing while delinquent zeroes the penalty timer; malicious borrowers can always harm lenders; intra-batch interest sharing; bad hooks can brick a function; rounding dust; markets can be configured to block withdrawals; Chainalysis dependency). Treat these as "by design / accepted," not new findings.

## Legal

The optional **Master Loan Agreement (MLA)** template aligns on-chain activity with a traditional credit agreement (warranties, covenants, sanctions handling, parameter mutability) and is enforceable via the legal system; borrowers attach it per market and lenders countersign on-chain. Also: **Terms of Use**, a **Risk Disclosure Statement**, and the UI **Privacy Policy** (effective 16 Jan 2025). Wildcat is not a lender, custodian, underwriter or insurer — be careful not to imply otherwise.

## Common gotchas / FAQ-style answers

- "Why can't I withdraw instantly?" Withdrawals are request → cycle → claim by design (fair pro-rata distribution in undercollateralised markets).
- "My market-token balance keeps changing." That's the rebase; balance tracks your accruing claim, there's no separate exchange rate.
- "Capacity = how much I can borrow?" No — capacity is the deposit ceiling; borrowable ≈ supply × (1 − reserveRatio).
- "Can I use stETH / a rebasing token as the underlying?" No — it breaks the interest model.
- "Fireblocks rejects my deposit." Add a Contract Call TAP rule allowing the market address, above generic blocking rules.
- "Safe multisig — where do I connect?" Add app.wildcat.finance as a Safe Custom App.
- "Is there a fee to wrap/unwrap 4626 shares?" No, only gas.

## Where to read more (routing table)

Point users at the live page; the `llms.txt` index lists every page with a description.

| If the question is about… | Go to |
| --- | --- |
| What Wildcat is / pitch | /overview/introduction |
| Vocabulary | /using-wildcat/terminology |
| Getting access (borrower KYB, lender credentials) | /using-wildcat/onboarding |
| Borrower KYB process and verified profile fields | /using-wildcat/how-borrowers-are-onboarded |
| Creating/operating a market | /using-wildcat/day-to-day-usage/borrowers |
| Depositing / withdrawing / claiming | /using-wildcat/day-to-day-usage/lenders |
| Who can deposit / credentials | /using-wildcat/day-to-day-usage/market-access-via-policies-hooks |
| Sanctions handling | /using-wildcat/day-to-day-usage/the-sentinel |
| 4626 wrapper (user) / (developer) | /using-wildcat/day-to-day-usage/wildcat-4626-wrapper · /technical-overview/security-developer-dives/wildcat-4626-wrapper |
| Collateral | /using-wildcat/day-to-day-usage/optional-collateral-contracts |
| Fees | /using-wildcat/protocol-usage-fees |
| Delinquency mechanics | /using-wildcat/delinquency |
| Proving an affected lender claim after default | /security-measures/proving-you-are-an-affected-lender-in-a-default |
| Event notifications | /using-wildcat/telegram-notification-bot |
| Scale factor / rebasing math | /technical-overview/security-developer-dives/the-scale-factor |
| How the market behaves internally | /technical-overview/security-developer-dives/core-behaviour |
| Hooks internals | /technical-overview/security-developer-dives/hooks/* |
| V1→V2 changes | /technical-overview/security-developer-dives/v1-greater-than-v2-changelog |
| Accepted quirks / out-of-scope | /technical-overview/security-developer-dives/known-issues |
| Structs / signatures | /technical-overview/protocol-structs · /technical-overview/function-event-signatures/* |
| Addresses | /technical-overview/contract-deployments |
| Audits / SphereX / bounty | /security-measures/* |
| Terms / risk / MLA / privacy | /legal/* |

All paths are under https://docs.wildcat.finance.
