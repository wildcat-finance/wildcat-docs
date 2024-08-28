---
description: What you need to know as a Wildcat borrower.
---

# Borrowers

## Launching A New Market

For the purpose of this section, we assume that the borrower has already gotten in contact with Wildcat and been added as a whitelisted borrower on the [**archcontroller**](../../terminology.md#archcontroller) (the registry that tracks permissions and deployments).

Once this is done, the borrower can go to the protocol UI, and having signed the [**Service Agreement**](../../terminology.md#service-agreement) (if not done already), navigate to the Borrower section, and then click New Market.

There are a number of parameter fields that are presented here, and the screen may appear a bit overwhelming, but they fundamentally represent the degrees of freedom you have available to you. \
\
They are:

### **Underlying Asset**

This is the asset that you wish to borrow, such as LUSD or WETH.

### Master Loan Agreement Type

This is not directly relevant to the structure of the market which is deployed, but borrowers are presented with the option of whether or not to make use of a Wildcat-specific master loan agreement.&#x20;

If selected, this agreement is presented to lenders via the front-end to sign before they first deposit.

### **Market Type**

Following the deprecation of Wildcat V1, the only type of market currently supported is the V2 market 'base' type. However, the functionality of a V2 market can be widely configured.

Each market is fundamentally open access to start (anyone can deposit, debt is freely transferable etc.), however there are a number of choices to be made which constrain access in certain ways depending on borrower preference. Examples are:

* **Minimum deposit amounts**: what is the minimum amount of the underlying asset that will be accepted by the market in a single deposit transaction by an approved lender?
* **Minimum market-freeze duration** (enabling fixed duration markets): how many days after market launch before withdrawal requests will process?
* **Transferability restrictions**: should the debt token issued by your Wildcat market be freely transferable to any recipient, restricted only to addresses that have credentials/authorisation to engage with the market, or further constrained to only move to/from the market itself?
* **Onboarding policy**: what mechanism do you want to use to enable lenders to engage with your market? At present, the options are an explicit address whitelist operated by the borrower, or adopting a [Keyring Network](https://keyring.network) policy (substantially on this [here](keyring-policies.md)).

### **Market Token Name Prefix**

The prefix string that the **market token** issued to represent debt will use. For example, if you are borrowing _WETH_ (Wrapped Ether_)_ and enter '_Market Maker X_' here, the name of the market token will be _Market Maker X Wrapped Ether_.\


### **Market Token Symbol Prefix**

The prefix string that the market token issued to represent debt will use. For example, if you are borrowing _WETH_ and enter 'mmx' here, the symbol of the market token will be _mmxWETH_.\


### **Market Capacity**

This represents the initial **capacity** of the market - the maximum amount of debt that you're willing to pay interest on at launch. Note that depending on what you set the **reserve ratio** as, this does _not_ correspond to the amount that you are able to **borrow** from the market when fully subscribed.\


### **Reserve Ratio (%)**

The percentage of the market **supply** that must remain _within_ the market available for redemption. For example, a market with a capacity of 100,000 tokens, a supply of 20,000 tokens and a reserve ratio of 25% must have 5,000 tokens within the market ready for lenders to withdraw.\
\
Wildcat V2 markets allow for this ratio to range between **0 - 100%.** This enables fully uncollateralised markets: however, a borrower will still be expected to maintain a small amount within the market in the event that a protocol fee is active or when withdrawal requests are made.\
\
Failing to maintain this level will result in the market becoming **delinquent**.\
\
Note that the capacity and the reserve ratio together dictate the _maximum_ that you are able to borrow from a market. A higher reserve ratio leads to a greater amount that you are paying interest on, but provides more of a cushion for lenders to easily exit their position, presuming that you fix delinquencies in a timely manner (lest you incur the _penalty rate_, see below).\


### **Lender APR (%)**

The amount of interest that you are willing to pay on deposits to _lenders_. This is the rate that will apply presuming that your market never stays delinquent for long enough for the **penalty rate** to activate.

Wildcat V2 markets allow for this value to range between **0 - 100%**.\
\
Note that this may not be the true APR that you pay - markets which utilise a [protocol fee](../../protocol-usage-fees.md) will add that rate onto the base rate (e.g. selecting a base rate of 10% for a market that includes a 5% protocol fee produces a final rate for the borrower of 10% + (0.05 \* 10%) = 10.5%.\


### **Penalty Rate (%)**

The amount of _additional_ APR that you agree to pay in the event that your market becomes [**delinquent**](../../terminology.md#delinquency) (i.e. falls below the reserve ratio) and the delinquency is not resolved within the amount of time specified by the [**grace period**](../../terminology.md#grace-period), as observed by the [**grace tracker**](../../terminology.md#grace-tracker).

Wildcat V2 markets allow for this value to range between **0 - 100%**. Note that a penalty rate of zero means that the borrower does not incur a penalty for ignoring delinquency until such time as they are marked as having defaulted (either as defined in a master loan agreement or as might be declared during legal proceedings after an extended period of non-repayment). We encourage borrowers to select a non-zero value to illustrate the seriousness with which they intend to monitor their obligations.\
\
This penalty rate is added on to the base rate only for as long as the value of the grace tracker is above that of the grace period.\


### **Grace Period Length (Hours)**

The amount of time that a market is permitted to be delinquent for before the penalty APR activates. This parameter is measured in hours, and comes with a corresponding variable called the grace tracker, which measures the amount of time for which the market has been delinquent.\
\
The grace period is a _rolling limit_: once delinquency has been cured within a market, the grace tracker will count back down to zero from whatever value it had reached, and any penalty APR that is currently in force will only cease to do so after the grace tracker value is once again below the grace period.

Wildcat V2 markets allow for this value to range between **0 - 2160 hours** (90 days).\
\
Note: this means that if a markets grace period is 3 days, and it takes 5 days to cure delinquency, this means that **4** days of penalty APR are paid. **This is important**: a borrower does not necessarily have `grace_period` amount of time to cure each distinct instance of delinquency!\


### **Withdrawal Cycle Length (Hours)**

The amount of time that a lender who has filed a withdrawal request must wait before they are permitted to claim their assets from the market.

Wildcat V2 markets allow for this value to range between **0 - 8760 hours (365 days)**.\
\
This parameter exists in order to fairly distribute assets across multiple lenders given the undercollateralised nature of Wildcat markets. In the event that a significant amount of the supply is recalled at once, a longer withdrawal cycle permits reserves to be handed out _pro rata_ depending on the reserves within the market. For more on how this looks from the lenders perspective, please see the [**Lenders**](../lenders.md) page.



***



Provided that all of these parameters are within range for the market type you are deploying, you will then be asked to submit a transaction which deploys a hooks instance and market contract parameterised as you have directed.&#x20;

If the template Master Loan Agreement has been selected, the borrower is required to pre-sign a [**Master Loan Agreement**](../../terminology.md#master-loan-agreement-mla). This document is then offered to lenders which seek to deposit to a market after onboarding, binding them to the borrower via contract. It defines certain warranties and covenants, accounts for the mutability of certain parameters and is intended to offer the lender protection via the legal system, as they shoulder the bulk of the risk in a trusted relationship.

## Sourcing Deposits

Once a given market is live, lenders can start onboarding to the market, depending on the hooks policy in place. For those markets which make use of an explicit address whitelist, the borrower must make use of the Market Details section of a market page to execute an on-chain transaction specifying one or multiple addresses.

If you wish to make use of a Keyring Network policy to enable lender self-onboarding, you will need to register with Keyring Network off-site and either clone the default Wildcat Keyring policy or create your own. Note: you cannot piggyback off of the Wildcat policy for your markets - you _must_ clone-and-own the policy which you make use of. This is both for compliance reasons and because if you own your policy, you're capable of editing it yourself. If you have any questions here, we're happy to help.

For those markets which make use of an such a Keyring policy, would-be lenders are directed off-site to Keyring to verify they meet the policy requirements, concluding in their submitting a transaction containing a zero-knowledge proof of adherence which will grant them an market access credential.

We defer the decision-making of who is allowed to be onboarded to borrowers, but require that they will not seek to approve lenders either resident in sanctioned nations or those that come with extant regulatory risk preventing interaction with the protocol.

If Wildcat notices that policies are breaching this, we are likely to [offboard](./#archcontroller-removal) the offending borrower, and may opt to remove affected markets from the UI. Crypto is global, and Wildcat isn't going to stand by and watch a borrower reap the whirlwind by allowing non-accredited American retail trader Joe Bloggs to lend them ten thousand dollars.

## Borrowing From A Market

If we fast forward from here to the stage where lenders have onboarded and deposited assets, we can finally get to the _point_ of all of this: borrowing assets from the market that you have set up.

Remember that the _capacity_ you set for your market only dictates the maximum amount that you are able to source from lenders, and that your _reserve ratio_ will dictate the amount of the _supply_ that you cannot remove from a market.

If you have created a market with a maximum capacity of 1,000,000 USDC and a reserve ratio of 20%, this means you can borrow _up to_ 800,000 USDC provided that the market is 'full' (i.e. _supply_ is equal to _capacity_). In the event where the supply to this market is 600,000 USDC, you can only borrow up to 480,000 USDC.

The process of actually borrowing available assets from a market is simple: navigate to the market details page of your market, and you will be presented with the ability to withdraw assets up to the current reserve ratio. If you've used protocols such as Euler or Aave in the past, you'll be familiar with this.

We strongly advise not borrowing right up to the limit, as the result of this will be that your market becomes delinquent after the very next non-static call which updates the market state and rebases the market token supply.

## Repaying A Market

The primary mechanic by which funds are recalled by lenders is through **withdrawal requests**, which isolate assets currently in reserve in a market for lenders to claim at the end of a withdrawal cycle (for more details on this, please refer to the [**Lenders**](../lenders.md) page).

Withdrawal requests impact the liquid and required reserves of your market, and as such borrowers are minded to monitor their reserve ratios to determine when funds are being requested. Requests (including who has placed the request and for how much) are also logged within the Market Details page.

The act of repaying is simple in the sense that it just requires moving assets back to the market contract via a standard ERC-20 transfer. Further, _anyone_ can repay assets to the market in this way - we've permitted this in case the borrower address is compromised.

In the event of such an address compromise, all lenders can file withdrawal requests, assets can subsequently be repaid from a third party, and - due to the manner in which withdrawal requests sequester assets during a withdrawal - can be honoured through the market contract without the compromised borrower address being able to access any assets.

## Reducing APR

The interest rate on a market is fixed at any given point in time (i.e. markets do not make use of a utilisation-rate based curve), however the borrower is free to adjust this rate step-wise should they wish, under the following formula:

* Should a borrower wish to increase the APR of a market in order to encourage additional deposits, they are able to do so without constraint.
* Should they wish to decrease the APR, they are able to do so by up to 25% of the current APR in a given two week period: a decrease of more than this requires that twice the amount is returned to the market reserves for that two week period to permit lenders to opt out ('ragequit') if they choose.\
  \
  To illustrate:
  * A borrower can reduce a market APR from 10% to 7.5% with no penalty, and two weeks thereafter will be able to reduce it again to 5.625%, and so on.
  * However, should a borrower reduce a market APR from 10% to 7.4% (a 26% reduction), they will be required to return 52% of the outstanding supply to the market for two weeks. After that time has passed, the reserve ratio will drop back to the prior level and the assets can be borrowed again.

Note that the above only applies if your market is in an 'open-term' setting: i.e. there is no hook enabled which is preventing withdrawals at the time of the proposed change. If this is the case, you will not be able to reduce the APR while that hook is active (otherwise that enables a fairly obvious rug mechanic).

If you're confused by this, ask us directly!

## Altering Capacity

As a borrower, you are able to adjust the capacity up to whatever amount you wish, or down to the market's current outstanding supply of market tokens, however it should be noted that rebasing of market tokens can bring their total supply above such a capacity. Interest accrues on the outstanding supply until such time as lenders reduce the supply through withdrawal requests that burn market tokens. The required reserves of a market remain unchanged regardless of capacity changes.

## Forced Withdrawals

A new addition to Wildcat V2 is that a borrower has the ability to eject specific lenders into a withdrawal cycle. We are wary that this ability in effect enables a preferential repayment mechanism whereby they can evacuate a preferred counterparty if they know that they are likely to default in the near future, but this risk is offset by the fact that other lenders are free to join the same withdrawal cycle alongside them.\
\
This functionality has been introduced to account for the fact that lenders have the ability to onboard themselves by self-generating an access credential if a policy hook is in place: a borrower may decide that someone that has self-onboarded is not a counterparty they wish to be exposed to.

More generally, this ability resolves an issue within V1 markets where a borrower may have been forced to terminate a market before they were ready because a lender refused to exit their position in order to accrue further interest.

## Terminating A Market

In the event that a borrower has finished utilising the funds for the purpose that the market was set up to facilitate, the borrower can _terminate_ (close) a market at will.

This is a special case of reducing the APR (with the associated increased reserve rate that accompanies it). When a market is closed, sufficient assets must be repaid to increase the reserve ratio to 100%, after which interest ceases to accrue and _no further parameter adjustment or borrowing is possible_. The only thing possible to do in a closed market is for the lenders to file withdrawal requests and exit via claiming.

Note that the withdrawal cycle period is erased in terminated markets: lenders still have to file two distinct transactions, but if the live market previously had a withdrawal cycle of a week, this duration is not enforced.

## Archcontroller Removal

For whatever reason, it may be the case that the Wildcat protocol itself no longer wishes to permit a given borrower to engage further with it. In this case, the address(es) of a borrower can be removed from the archcontroller by its owners. If this happens, the borrower can no longer deploy _new_ hooks instances or markets.

However, they are still capable of interacting with _existing_ markets as before - neither the protocol nor its operators can force these closed. This is because there are likely to be master loan agreements surrounding market usage, and Wildcat having the power to unilaterally step in and sever them would make it a key participant in the arrangement.
