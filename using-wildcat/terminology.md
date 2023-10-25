---
description: It's dangerous to go alone - learn these.
---

# Terminology

#### **Archcontroller**

* Smart contract which doubles up as a registry and permission gate. [Borrowers](terminology.md#borrower) are added or removed from the archcontroller by the operators of the protocol itself (granting/rescinding the ability to deploy [controllers](terminology.md#controller) and/or [markets](terminology.md#market)), and the addresses of any controller factories, controllers or markets that get deployed through the protocol are stored here.

#### **Base APR**

* The interest rate that lenders receive on [assets](terminology.md#underlying-asset) that they have deposited into a particular [market](terminology.md#market), in the absence of the [penalty APR](terminology.md#penalty-apr) being enforced.

#### **Borrow**

* To withdraw [assets](terminology.md#underlying-asset) from a [market](terminology.md#market) that has a non-zero [supply](terminology.md#supply) and [reserve ratio](terminology.md#reserve-ratio) less than 100%, with the intent of repaying the assets (plus any accrued interest) to the market either when the required purpose of using the assets has concluded or as a response to [withdrawal requests](terminology.md#withdrawal-request).

#### **Borrower**

* Both:
  * The counterparty that wishes to make use of a credit facility through a Wildcat [market](terminology.md#market), and
  * The blockchain address that defines the parameters of a market and deploys the [controller](terminology.md#controller) and market contracts that comprise it.

#### **Capacity**

* Parameter required of [borrower](terminology.md#borrower) when creating a new [market](terminology.md#market).
* The _maximum_ amount of an asset that a borrower is looking to source via a market - the sum total of what all lenders can [deposit](terminology.md#deposit) and earn interest on.

#### **Claim**

* Removing [assets](terminology.md#underlying-asset) from the [unclaimed withdrawals pool](terminology.md#unclaimed-withdrawals-pool) that were requested for withdrawal by a [lender](terminology.md#lender) at the end of a [withdrawal cycle](terminology.md#withdrawal-cycle).&#x20;
* Depending on the reserve ratio of the market when the withdrawal request associated with a claim was made, claiming _may_ require the burning of [market tokens](terminology.md#market-token) (see [**Lenders**](day-to-day-usage/lenders.md) for details).
* Note that retrieving your [deposits](terminology.md#deposit) from a Wildcat market requires a [withdrawal request](terminology.md#withdrawal-request) and _then_ a claim - it is a two transaction process with at least one withdrawal cycle in between them.

#### **Controller**

* Smart contract deployed by a [borrower](terminology.md#borrower) which contains the list of addresses which are authorised to [deposit](terminology.md#deposit) to any [markets](terminology.md#market) deployed through it.
* Contains logic concerning parameters of markets deployed through it (e.g. maximum [grace period](terminology.md#grace-period), minimum [penalty APR](terminology.md#penalty-apr)).
* Controls APR adjustments and enforces [reserve ratios](terminology.md#reserve-ratio) of markets.
* Imposes protocol fees (either lump-sum origination or APR-based) on markets.

#### **Default**

* Event in which a counterparty has failed their obligations in some form or another, _typically_ involving the unwillingness or inability of the [borrower](terminology.md#borrower) to [deposit](terminology.md#deposit) to a [delinquent](terminology.md#delinquency) [market](terminology.md#market) after a [lender](terminology.md#lender) has waited a sufficiently long period of time with an [expired withdrawal request](terminology.md#expired-withdrawal).
* Gives rise to the right to arbitration or civil action in the courts.
* Further defined in both the [Service Agreement](terminology.md#service-agreement) and the [Master Loan Agreement](terminology.md#master-loan-agreement-mla) between borrower and lender (if countersigned by the latter).

#### **Delinquency**

* A [market](terminology.md#market) state wherein there are insufficient [assets](terminology.md#underlying-asset) in the market to meet the [reserve ratio](terminology.md#reserve-ratio) as specified by the borrower.
* Arises via the passage of time through interest if the borrower borrows right up to their reserve ratio.
* Can also arise if a [lender](terminology.md#lender) makes a [withdrawal request](terminology.md#withdrawal-request) and moves assets within the market into the [unclaimed withdrawals pool](terminology.md#unclaimed-withdrawals-pool).
* A market being delinquent for an extended period of time (as specified by the [grace period](terminology.md#grace-period)) results in the [penalty APR](terminology.md#penalty-apr) being enforced in addition to the [base APR](terminology.md#base-apr) and any [protocol APR](terminology.md#protocol-apr) that may apply.
* 'Cured' by [depositing](terminology.md#deposit) sufficient assets into the market as to reattain the required reserve ratio.

#### **Deposit**

* Both:
  * The act of sending [assets](terminology.md#underlying-asset) as a [lender](terminology.md#lender) to a [market](terminology.md#market) for the purposes of being [borrowed](terminology.md#borrow) by the [borrower](terminology.md#borrower),
  * The act of sending assets as a borrower to a market for the purposes of being [withdrawn](terminology.md#withdrawal-request) by lenders,
  * A term for the lenders' assets themselves once in a market.

#### **Escrow Contract**

* An auxiliary smart contract that is deployed in the event that the [sentinel](terminology.md#sentinel) detects that a [lender](terminology.md#lender) address has been added to a sanctioned list such as the OFAC SDN: this check is performed through the [**Chainalysis oracle**](https://go.chainalysis.com/chainalysis-oracle-docs.html).
* Used to transfer the debt (for the [lender](terminology.md#lender)) and obligation to repay (for the [borrower](terminology.md#borrower)) away from the [market](terminology.md#market) contract to avoid wider contamination through interaction. Interest ceases to accrue upon creation and transfer.
* Any [assets](terminology.md#underlying-asset) relating to an attempted claim by the affected lender as well as any market tokens tied to their remaining [deposit](terminology.md#deposit) are automatically transferred to the escrow contract when blocked (either through an attempt to withdraw or via a call to a 'nuke from orbit' function found within the market).
* Assets can only be released to the lender in the event that they are no longer tagged as sanctioned by the Chainalysis oracle.

#### Expired Withdrawal

* A [withdrawal request](terminology.md#withdrawal-request) that could not be fully honoured by [assets](terminology.md#underlying-asset) in the [unclaimed withdrawals pool](terminology.md#unclaimed-withdrawals-pool) within a single [withdrawal cycle](terminology.md#withdrawal-cycle).

#### **Grace Period**

* Parameter required of [borrower](terminology.md#borrower) when creating a new [market](terminology.md#market).
* Rolling period of time for which a market can be [delinquent](terminology.md#delinquency) before the [penalty APR](terminology.md#penalty-apr) of the market activates.
* Note that the grace period does not 'reset' to zero when delinquency is cured. See [grace tracker](terminology.md#grace-tracker) below for details.

#### **Grace Tracker**

* Internal [market](terminology.md#market) parameter associated with the [grace period](terminology.md#grace-period).
* Once a market becomes [delinquent](terminology.md#delinquency), begins counting seconds up from zero - when the value of the grace tracker exceeds the grace period, the [penalty APR](terminology.md#penalty-apr) activates.
* Once a market is cured of delinquency, begins counting seconds down to zero - the penalty APR continues to apply _until the grace tracker value is below the grace period value_.
* Enforces the rolling nature of the grace period.

#### **Lender**

* Both:
  * A counterparty that wishes to provide a credit facility through a Wildcat [market](terminology.md#market), and
  * The blockchain address associated with that counterparty which [deposits](terminology.md#deposit) [assets](terminology.md#underlying-asset) to a market for the purposes of being [borrowed](terminology.md#borrow) by the [borrower](terminology.md#borrower).

#### **Market**

* Smart contract that accepts [underlying assets](terminology.md#underlying-asset), issuing [market tokens](terminology.md#market-token) in return.
* Deployed by [borrower](terminology.md#borrower) through an associated [controller](terminology.md#controller).
* Holds assets in escrow pending either being [borrowed](terminology.md#borrow) by the borrower or [withdrawn](terminology.md#withdrawal-request) by a [lender](terminology.md#lender).
* Permissioned: only lenders that have been authorised on the associated controller by the borrower to deposit can interact.

#### **Market Token**

* ERC-20 token indicating a [claim](terminology.md#claim) on the [underlying assets](terminology.md#underlying-asset) in a [market](terminology.md#market).
* Issued to [lenders](terminology.md#lender) after a [deposit](terminology.md#deposit).
* [Supply](terminology.md#supply) rebases after every non-static call to the market contract depending on the total current APR of the market: always redeemable 1:1.
* Transferable to arbitrary addresses.
* Can only be redeemed by authorised lender addresses (not necessarily the same one that received the market tokens initially).
* Name and symbol prefixes are customisable in market creation, prepending to the name and symbol of the underlying asset.

#### **Master Loan Agreement (MLA)**

* Legal agreement binding [borrowers](terminology.md#borrower) and [lenders](terminology.md#lender) together on a one-to-one basis for a specific [market](terminology.md#market).
* Defines expected behaviour and various covenants and representations concerning identity, usage of funds, security practices and various events that constitute [default](terminology.md#default).
* Sets jurisdiction for any arbitration or civil suits as the UK.
* Must be signed by borrower when deploying a market using the protocol UI.
* Is offered to lender to countersign when first encountering a market via the protocol UI (which can be signed or declined depending on lenders preference, or whether counterparties have entered into another agreement).
* Offered by Wildcat as protection for lenders.

#### **Penalty APR**

* Parameter required of [borrower](terminology.md#borrower) when creating a new [market](terminology.md#market).
* Additional interest rate (above and beyond the [base APR](terminology.md#base-apr) and any [protocol APR](terminology.md#protocol-apr) imposed by a market [controller](terminology.md#controller)) that is applied for as long as the [grace tracker](terminology.md#grace-tracker) value for a market is in excess of the specified [grace period](terminology.md#grace-period).
* Encourages borrower to responsibly monitor the [reserve ratio](terminology.md#reserve-ratio) of a market.
* No part of the penalty APR is receivable by the Wildcat protocol itself (does not inflate the protocol APR if present).

#### **Pending Withdrawal**

* A [withdrawal request](terminology.md#withdrawal-request) that has not yet [expired](terminology.md#expired-withdrawal) (i.e. was created in the current [withdrawal cycle](../technical-deep-dive/component-overview/wildcat-market-overview/wildcatmarketwithdrawals.sol.md#processunpaidwithdrawalbatch)).

#### Protocol APR

* Percentage of [base APR](terminology.md#base-apr) that accrues to the Wildcat protocol itself.
* Fixed parameter in [controller](terminology.md#controller) contracts, applying to all [markets](terminology.md#market) deployed by said [controller](terminology.md#controller).
* Can be zero.
* Does not increase in the presence of an active [penalty APR](terminology.md#penalty-apr) (which only increases the APR accruing to [lenders](terminology.md#lender)).&#x20;
* Example: market with base APR of 10% and protocol APR of 20% results in borrower paying 12% when penalty APR is not active.&#x20;

#### **Reserve Ratio**

* Parameter required of [borrower](terminology.md#borrower) when creating a new [market](terminology.md#market).
* Percentage of current market [supply](terminology.md#supply) - [deposited](terminology.md#deposit) [assets](terminology.md#underlying-asset) - that must be kept in the market (but still accrue interest).
* Intended to provide a liquid buffer for [lenders](terminology.md#lender) to make [withdrawal requests](terminology.md#withdrawal-request) against, partially 'collateralising' the credit facility through lenders' deposits.
* Increases temporarily when:
  * a borrower reduces the [base APR](terminology.md#base-apr) of a [market](terminology.md#market) (fixed-term increase), or
  * there are [pending](terminology.md#pending-withdrawal) or [expired withdrawals](terminology.md#expired-withdrawal) which cannot be honoured by the contents of the [unclaimed withdrawals pool](terminology.md#unclaimed-withdrawals-pool) (increased until resolved).
* A market which has insufficient assets in the market to meet the reserve ratio is said to be [delinquent](terminology.md#delinquency), with the [penalty APR](terminology.md#penalty-apr) potentially being enforced if the delinquency is not cured before the [grace tracker](terminology.md#grace-tracker) value exceeds that of the [grace period](terminology.md#grace-period) for that particular market.

#### **Sentinel**

* Smart contract that ensures that addresses which interact with the protocol are not flagged by the [**Chainalysis oracle**](https://go.chainalysis.com/chainalysis-oracle-docs.html) for sanctions.
* Can deploy escrow contracts to excise a [lender](terminology.md#lender) flagged by the oracle from a wider [market](terminology.md#market).

#### **Service Agreement**

* Agreement that must be signed by all users of the protocol ([borrower](terminology.md#borrower) or [lender](terminology.md#lender)) when first accessing the protocol UI and connecting their wallet.
* Presents - among other things - protocol terminology and logic, and constitutes a waiver of protocol responsibility for any damages incurred via its use.
* For the full text, please see [**Service Agreement**](terminology.md#service-agreement) (pending as of 09/10/2023).

#### **Supply**

* Current amount of [underlying asset](terminology.md#underlying-asset) [deposited](terminology.md#deposit) in a [market](terminology.md#market).
* Tied 1:1 with the supply of [market tokens](terminology.md#market-token) (rate of growth APR dependent).
* Can only be reduced by burning market tokens as part of a [withdrawal request](terminology.md#withdrawal-request) or [claim](terminology.md#claim).
* [Reserve ratios](terminology.md#reserve-ratio) are enforced against the supply of a market, _not_ its [capacity](terminology.md#capacity).
* Capacity can be reduced below current supply by a [borrower](terminology.md#borrower), but this only prevents the further deposit of assets until the supply is once again below capacity.

#### **Unclaimed Withdrawals Pool**

* A sequestered pool of [underlying assets](terminology.md#underlying-asset) which are pending their [claim](terminology.md#claim) by [lenders](terminology.md#lender) following a [withdrawal request](terminology.md#withdrawal-request).
* Assets are moved from market reserves to the unclaimed withdrawals pool by burning [market tokens](terminology.md#market-token) at a 1:1 ratio (reducing the [supply](terminology.md#supply) of the market).
* Assets within the unclaimed withdrawals pool do not accrue interest, but similarly cannot be [borrowed](terminology.md#borrow) by the [borrower](terminology.md#borrower) - they are considered out of reach.

#### **Underlying Asset**

* Parameter required of [borrower](onboarding.md#borrowers) when creating a new [market](terminology.md#market).
* The asset which the borrower is seeking to [borrow](terminology.md#borrow) by deploying a market - for example DAI (Dai Stablecoin) or WETH (Wrapped Ether).
* Can be _any_ ERC-20 token.

#### **Vault**

* See [market](terminology.md#market).
* If you see this term anywhere, it's a mistake that we should have cleared up!

#### **Withdrawal Cycle**

* Parameter required of [borrower](terminology.md#borrower) when creating a new [market](terminology.md#market).
* Period of time that must elapse between the first [withdrawal request](terminology.md#withdrawal-request) of a 'wave' of withdrawals and [assets](terminology.md#underlying-asset) in the [unclaimed withdrawals pool](terminology.md#unclaimed-withdrawals-pool) being made available to [claim](terminology.md#claim).
* Withdrawal cycles do not work on a rolling basis - at the end of one withdrawal cycle, the next cycle will not start until the next withdrawal request.
* In the event that the amount being claimed in the same cycle across all lenders is in excess of the reserves currently within a market, all [lenders](terminology.md#lender) requests within that cycle will be honoured _pro rata_ depending on overall amount requested.
* Intended to prevent a run on a given market (mass withdrawal requests) leading to slower lenders receiving nothing.
* Can have a value of zero, in which case each withdrawal request is processed - and potentially added to the [withdrawal queue](terminology.md#withdrawal-queue) - as a standalone batch.

#### **Withdrawal Queue**

* Internal data structure of a [market](terminology.md#market).
* All [withdrawal requests](terminology.md#withdrawal-request) that could not be fully honoured at the end of their [withdrawal cycle](terminology.md#withdrawal-cycle) are batched together, marked as [expired](terminology.md#expired-withdrawal) and added to the withdrawal queue.
* Tracks the order and amounts of [lender](terminology.md#lender) [claims](terminology.md#claim).
* FIFO (First-In-First-Out): when [assets](day-to-day-usage/lenders.md) are returned to a market which has a non-zero withdrawal queue, assets are immediately routed to the [unclaimed withdrawals pool](terminology.md#unclaimed-withdrawals-pool) and can subsequently be claimed by lenders with the oldest expired withdrawals first.

#### Withdrawal Request

* An instruction to a [market](terminology.md#market) to transfer reserves within a market to the [unclaimed withdrawals pool](terminology.md#unclaimed-withdrawals-pool), to be [claimed](terminology.md#claim) at the end of a [withdrawal cycle](terminology.md#withdrawal-cycle).
* A withdrawal request made of a market with non-zero reserves will burn as many [market tokens](terminology.md#market-token) as possible 1:1 to fully honour the request.
* Any amount requested - whether or not it is in excess of the market reserves - is marked as a [pending withdrawal](terminology.md#pending-withdrawal), either to be fully honoured at the end of the cycle, or marked as [expired](terminology.md#expired-withdrawal) and added to the [withdrawal queue](terminology.md#withdrawal-queue), depending on the actions of the [borrower](terminology.md#borrower) during the cycle.

#### **Whitelisted**

* The state in which either:
  * A [borrower](terminology.md#borrower) address has been added to the [archcontroller](terminology.md#archcontroller) and is permitted to deploy [controllers](terminology.md#controller) and [markets](terminology.md#market), or
  * A [lender](terminology.md#lender) address has been added to a controller by a borrower and is permitted to [deposit](terminology.md#deposit) to any [markets](terminology.md#market) deployed by said controller.

