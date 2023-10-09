---
description: It's dangerous to go alone - learn these.
---

# Terminology

#### **Archcontroller**

* Smart contract which doubles up as a registry and permission gate. Borrowers are added or removed from the archcontroller by the operators of the protocol itself (granting/rescinding the ability to deploy controllers and/or markets), and the addresses of any controller factories, controllers or markets that get deployed through the protocol are stored here.

#### **Base APR**

* The interest rate that lenders receive on assets that they have deposited into a particular market, in the absence of the [penalty APR](terminology.md#penalty-apr) being enforced.

#### **Borrow**

* To withdraw assets from a market that has a non-zero supply and reserve ratio less than 100%, with the intent of re-depositing the assets (plus any accrued interest) either when the required purpose of using the assets has concluded or as a response to withdrawals.

#### **Borrower**

* Both:
  * The counterparty that wishes to make use of a credit facility through a Wildcat market, and
  * The blockchain address that defines the parameters of a market and deploys the controller and market contracts that comprise it.

#### **Capacity**

* Parameter required of borrower when creating a new market.
* The _maximum_ amount of an asset that a borrower is looking to source via a market - the sum total of what all lenders can deposit and earn interest on.

#### **Claim**

* Removing assets from the reserved assets pool that were requested for withdrawal by a lender at the end of a withdrawal cycle.&#x20;
* Depending on whether there were assets in reserve when the withdrawal request associated with a claim was made, claiming _may_ require the burning of market tokens (see [**Lenders**](day-to-day-usage/lenders.md) for details).
* Note that retrieving your deposits from a Wildcat market requires a withdrawal request and _then_ a claim - it is a two transaction process with at least one withdrawal cycle in between them.

#### **Controller**

* Smart contract deployed by a borrower which contains the list of addresses which are authorised to deposit to any markets deployed through it.
* Contains logic concerning parameters of markets deployed through it (e.g. maximum APR, minimum penalty rate).
* Controls APR adjustments and minimum reserve ratios of markets.
* Imposes protocol fees (either lump-sum origination or APR-based) on markets.

#### **Default**

* Event in which a counterparty has failed their obligations in some form or another, _typically_ involving the unwillingness or inability of the borrower to repay outstanding debt to a market after a lender has waited a sufficiently long period of time with an expired withdrawal request.
* Gives rise to the right to arbitration or civil action in the courts.
* Further defined in both the Service Agreement and the Master Loan Agreement between borrower and lender (if countersigned by the latter).

#### **Delinquency**

* A market state wherein there are insufficient assets in the market to meet the reserve ratio as specified by the borrower.
* Arises via the passage of time through interest if the borrower borrows right up to their reserve ratio.
* Can also arises if a lender makes a withdrawal request and moves assets within the market into the reserved assets pool.
* A market being delinquent for an extended period of time (as specified by the grace period) results in the penalty APR being enforced in addition to the base APR and any protocol APR that may apply.
* 'Cured' by depositing sufficient assets into the market as to reattain the required reserve ratio.

#### **Deposit**

* Both:
  * The act of sending assets as a lender to a market for the purposes of being borrowed by the borrower,&#x20;
  * A term for the lenders' assets themselves once in a market.

#### **Escrow Contract**

* An auxiliary smart contract that is deployed in the event that the sentinel address detects that a lender address has been added to a sanctioned list such as the OFAC SDN: this check is performed through the Chainalysis oracle.
* Transfers the debt (for the lender) and obligation to repay (for the borrower) into itself and away from the market contract to avoid wider contamination through interaction. Interest ceases to accrue upon transfer.
* Borrower is immediately expected to deposit all outstanding assets relating to the affected lender's deposit into the escrow contract.
* Assets can only be released to the lender in the event that they are no longer tagged as sanctioned by the Chainalysis oracle.

#### Expired Withdrawal

* \[**TO COMPLETE**]

#### **Grace Period**

* Parameter required of borrower when creating a new market.
* Rolling period of time for which a market can be delinquent before the penalty APR of the market activates.
* Note that the grace period does not 'reset' to zero when delinquency is cured. See grace tracker below for details.

#### **Grace Tracker**

* Internal market parameter associated with the grace period.
* Once a market becomes delinquent, begins counting seconds up from zero - when the value of the grace tracker exceeds the grace period, the penalty APR activates.
* Once a market is cured of delinquency, begins counting seconds down to zero - the penalty APR continues to apply _until the grace tracker value is below the grace period value_.
* Enforces the rolling nature of the grace period.

#### **Lender**

* Both:
  * A counterparty that wishes to provide a credit facility through a Wildcat market, and
  * The blockchain address associated with that counterparty which deposits and withdraws assets to a market for the purposes of being borrowed by the borrower.

#### **Market**

* Smart contract that accepts underlying assets, issues market tokens in return.
* Deployed by borrower through an associated controller.
* Holds assets in escrow pending either being borrowed by the borrower or withdrawn by the lender.
* Permissioned: only lenders that have been authorised on the associated controller by the borrower to deposit can interact.

#### **Market Token**

* ERC-20 token indicating a claim on the underlying assets in the market.
* Issued to lenders after a deposit.
* Supply rebases after every non-static call to the market contract depending on the interest rate of the market: always redeemable 1:1.
* Transferable to arbitrary addresses.
* Can only be redeemed by authorised lender addresses (not necessarily the same one that received the market tokens initially).
* Name and symbol prefixes are customisable in market creation, prepending to the name and symbol of the underlying asset.

#### **Master Loan Agreement (MLA)**

* Legal agreement binding borrowers and lenders together on a one-to-one basis for a specific market.
* Defines expected behaviour and various covenants and representations concerning identity, usage of funds, security practices and various events that constitute default.
* Sets jurisdiction for any arbitration or civil suits in the UK.
* Must be signed by borrower when deploying a market using the protocol UI.
* Is offered to lender to countersign when first encountering a vault via the protocol UI (which can be signed or declined dependong on lenders preference, or if counterparties have entered into another agreement).
* Offered by Wildcat as protection for lenders.

#### **Penalty APR**

* Parameter required of borrower when creating a new market.
* Additional interest rate (above and beyond the base APR and any APR-based protocol fee imposed by a market controller) that is applied for as long as the grace tracker value for a market is in excess of the specified grace period.
* Encourages borrower to responsibly monitor the health of a market.

#### **Pending Withdrawal**

* A withdrawal request that has not yet expired (i.e. was created in the current withdrawal cycle).

#### **Reserve Ratio**

* Parameter required of borrower when creating a new market.
* Percentage of current market supply - deposited assets - that must be kept in the market (but still accrue interest).
* Intended to provide a liquid buffer for lenders to make withdrawal requests against, partially 'collateralising' the credit facility through lenders' assets.
* Increases temporarily when:
  * a borrower reduces the base APR of a vault (fixed-term increase), or
  * there are pending or expired withdrawals which cannot be honoured by the contents of the reserved assets pool (increased until resolved).
* A market which has insufficient assets in the market to meet the reserve ratio is said to be delinquent, with the penalty APR potentially being enforced if the delinquency is not cured before the grace tracker value exceeds that of the grace period for that particular market.

#### **Reserved Assets Pool**

* A sequestered pool of underlying assets which are pending their claim by lenders following a withdrawal request.
* Assets are moved from market reserves to the reserved assets pool by burning market tokens at a 1:1 ratio.
* Assets within the reserved assets pool do not accrue interest, but similarly cannot be borrowed by the borrower - they are considered out of reach.

#### **Sentinel**

* Smart contract that ensures that addresses which interact with the protocol are not flagged by the Chainalysis oracle for sanctions.
* Can deploy escrow contracts to excise a lender flagged by the oracle from a wider market.

#### **Service Agreement**

* Agreement that must be signed by all users of the protocol (borrower or lender) when first accessing the protocol UI and connecting their wallet.
* Presents - among other things - protocol terminology and logic, and constitutes a waiver of protocol responsibility for any damages incurred via its use.
* SHA-256 hash of agreement text is signed by wallet.
* For the full text, please see [**Service Agreement**](terminology.md#service-agreement) (pending as of 09/10/2023).

#### **Supply**

* Current amount of underlying asset deposited in a market.
* Tied 1:1 with the supply of market tokens (rate of growth APR dependent).
* Can only be reduced by burning market tokens as part of a withdrawal.
* Reserve ratios are enforced against the supply of a market, not capacity.
* Capacity can be reduced below current supply by a borrower, but this only prevents the further deposit of assets once the supply is once again below capacity.

#### **Underlying Asset**

* Parameter required of borrower when creating a new market.
* The asset which the borrower is seeking to borrow by deploying a market - for example DAI (Dai Stablecoin) or WETH (Wrapped Ether).
* Can be _any_ ERC-20 token.

#### **Vault**

* See market.

#### **Withdrawal Cycle**

* Parameter required of borrower when creating a new market.
* Period of time that must elapse between the first withdrawal request of a 'wave' of withdrawals and assets being made available to claim.
* Withdrawal cycles do not work on a rolling basis - at the end of one withdrawal cycle, the next cycle will not start until the next withdrawal request.
* In the event that the amount being claimed in the same cycle across all lenders is in excess of the reserves currently within a market, all lenders requests within that cycle will be honoured _pro rata_ depending on overall amount requested.
* Intended to prevent a run on a given market (mass withdrawal requests) leading to slower lenders receiving nothing.
* Can have a value of zero, in which case each withdrawal request is processed - and potentially added to the withdrawal queue - as a standalone batch.

**Withdrawal Queue**

* Internal data structure of a market.
* All withdrawal amounts that could not be honoured at the end of their withdrawal cycle are batched together, marked as expired and added to the withdrawal queue.
* Tracks the order and amounts of lender claims.
* FIFO (First-In-First-Out): when assets are returned to a market which has a non-zero withdrawal queue, assets are immediately routed to the reserved assets pool and can subsequently be claimed by lenders with the oldest expired withdrawals first.

#### Withdrawal Request

* An instruction to a market to transfer reserves within a market to the reserved assets pool, to be claimed at the end of a withdrawal cycle.
* A withdrawal request made of a market with non-zero reserves will burn as many market tokens as possible 1:1 to fully honour the request.
* Any amount requested - whether or not it is in excess of the market reserves - is marked as a pending withdrawal, either to be fully honoured at the end of the cycle, or marked as expired and added to the withdrawal queue, depending on the actions of the borrower.

#### **Whitelisted**

* The state in which either:
  * A borrower address has been added to the archcontroller and is permitted to deploy controllers and markets, or
  * A lender address has been added to a controller by a borrower and is permitted to deposit to any markets deployed by said controller.

