---
description: What you need to know as a Wildcat borrower.
---

# Borrowers

#### Launching A New Market

For the purpose of this section, we assume that the borrower has already gotten in contact with the Wildcat protocol team itself and jumped through the hoops to be added as a whitelisted borrower on the [**archcontroller**](../terminology.md#archcontroller) (the registry that tracks permissions and deployments).

Once this is done, the borrower can go to the protocol UI, and having signed the [**Service Agreement**](../terminology.md#service-agreement) (if not done already), navigate to the Borrower section, and then click New Market.

There are a number of parameter fields that are presented here, and the screen may appear a bit overwhelming, but they fundamentally represent the degrees of freedom you have available to you. They are:

* **Select Market Type**
  * Dropdown menu indicating what flavour of market you wish to deploy (e.g. vanilla borrowing, call option agreement, permissionless).\
    \
    Each distinct market type is enabled by a distinct **controller** variant - what you are actually picking here is the _type_ of controller which deploys your market.\

* **Underlying Asset**
  * This is the asset that you wish to borrow, such as DAI or WETH. \

* **Market Token Name Prefix**
  * The prefix string that the **market token** issued to represent debt will use. For example, if you are borrowing _DAI_ (_Dai Stablecoin)_ and enter '_West Ham Capital_' here, the name of the market token will be _West Ham Capital Dai Stablecoin_.\

* **Market Token Symbol Prefix**
  * The prefix string that the market token issued to represent debt will use. For example, if you are borrowing _DAI_ (_Dai Stablecoin)_ and enter 'WHC' here, the symbol of the market token will be _WHCDAI_.\

*   **Market Capacity**

    * This represents the initial **capacity** of the market - the maximum amount of debt that you're willing to pay interest on at launch. Note that depending on what you set the **reserve ratio** as, this does _not_ correspond to the amount that you are able to **borrow** from the market when fully subscribed.


* **Reserve Ratio (%)**
  * The percentage of the market **supply** that must remain _within_ the market available for redemption. For example, a market with a capacity of 100,000 tokens, a supply of 20,000 tokens and a reserve ratio of 25% must have 5,000 tokens within the market ready for lenders to withdraw.\
    \
    Failing to maintain this level will result in the market becoming **delinquent**.\
    \
    Note that the capacity and the reserve ratio together dictate the _maximum_ that you are able to borrow from a market. A higher reserve ratio leads to a greater amount that you are paying interest on, but provides more of a cushion for lenders to easily exit their position, presuming that you fix delinquencies in a timely manner (lest you incur the _penalty fee_, see below).\

* **Lender APR (%)**
  * The amount of interest that you are willing to pay on deposits to _lenders_. This is the rate that will apply presuming that your market never stays delinquent for long enough for the **penalty rate** to activate.\
    \
    Note that dependent on controller, this may not be the final APR - markets deployed via controllers that utilise a **protocol fee** will add that rate onto the base rate (e.g. selecting a base rate of 10% for a market that includes a 20% protocol fee produces a final rate for the borrower of 10% + (0.2 \* 10%) = 12%.\

* **Penalty Rate (%)**
  * The amount of _additional_ interest that you agree to pay in the event that your market becomes [**delinquent**](../terminology.md#delinquency) (i.e. falls below the reserve ratio) and the delinquency is not resolved within the amount of time specified by the [**grace period**](../terminology.md#grace-period), as observed by the [**grace tracker**](../terminology.md#grace-tracker).\
    \
    This penalty rate is added on to the base rate only for as long as the value of the grace tracker is above that of the grace period.\

* **Grace Period Length (Hours)**
  * The amount of time that a market is permitted to be delinquent for before the penalty APR activates. This parameter is measured in hours, and comes with a corresponding variable called the grace tracker, which measures the amount of time for which the market has been delinquent.\
    \
    The grace period is a _rolling limit_: once delinquency has been cured within a market, the grace tracker will count back down to zero from whatever value it had reached, and any penalty APR that is currently in force will only cease to do so after the grace tracker value is once again below the grace period.\
    \
    Note: this means that if a markets grace period is 3 days, and it takes 5 days to cure delinquency, this means that **4** days of penalty APR are paid. **This is important**: a borrower does not necessarily have `grace_period` amount of time to cure each distinct instance of delinquency!\

* **Withdrawal Cycle Length (Hours)**
  * The amount of time that a lender who has filed a withdrawal request must wait before they are permitted to claim their assets from the market. This parameter is measured in hours, and _can_ be set to zero in order to enable instant withdrawals.\
    \
    This parameter exists in order to fairly distribute assets across multiple lenders given the undercollateralised nature of Wildcat markets. In the event that a significant amount of the supply is recalled at once, a longer withdrawal cycle permits reserves to be handed out _pro rata_ depending on the reserves within the market. For more on how this looks from the lenders perspective, please see the [**Lenders**](lenders.md) page.

Provided that all of these parameters are within range for the market type you are deploying (and these vary on a per-controller basis), you will then be asked to submit a single transaction which first deploys a controller of the correct type from the controller factory, and subsequently deploys a market parameterised as you have directed.

As part of this market deployment process, prior to submitting the above transaction, the borrower is required to pre-sign a [**Master Loan Agreement**](../terminology.md#master-loan-agreement-mla) populated with the fields provided. This is a document which binds each individual lender to the borrower via contract, and is intended to offer the lender protection via the legal system. For the process of countersigning, please see the [lenders.md](lenders.md "mention") page.

A note: each borrower address is constrained to owning one instance of a controller per variant, but a borrower _can_ deploy several markets with the same underlying asset against such a controller provided that the name and symbols are unique. **However**, while controllers can support multiple markets, the **launch version of the protocol UI insists on a 1:1 association**: as a result, if you wish to deploy multiple markets, the borrower must make use of (and be approved via the archcontroller for) additional deployer addresses.

#### Sourcing Deposits

Once a given market is live, the borrower can start the process of approving lenders that they wish to interact with it (i.e. deposit assets). They can do this through the Market Details page of the market, approving one or multiple addresses per transaction. These transactions target the _controller_ for that particular market. This has two caveats:

* Deploying a new market from a different controller produces a different whitelist: as a borrower you are expected to maintain distinct lender whitelists for each of your markets.
* New markets deployed from the _same_ controller (which is possible, but the current UI does not permit) inherit the whitelist the borrower set up for any previous markets deployed against it.

We defer the process of how the borrower determines the suitability of a lender to be whitelisted for their markets to them, but expect the bare minimum in terms of not approving lenders resident in sanctioned nations or within nations that have legislation preventing their interaction with the protocol (see [**Onboarding**](../onboarding.md)).

#### Borrowing From A Market

If we fast forward from here to the stage where lenders have been whitelisted and deposited assets, we can finally get to the _point_ of all of this: borrowing assets from the market that you have set up.

Remember that the _capacity_ you set for your market only dictates the maximum amount that you are able to source from lenders, and that your _reserve ratio_ will dictate the amount of the _supply_ that you cannot remove from a market.

If you have created a market with a maximum capacity of 1,000,000 USDC and a reserve ratio of 20%, this means you can borrow _up to_ 800,000 USDC provided that the market is 'full' (i.e. _supply_ is equal to _capacity_). In the event where the supply to this market is 600,000 USDC, you can only borrow up to 480,000 USDC.

The process of actually borrowing available assets from a market is quite simple: navigate to the market details page of your market, and you will be presented with the ability to withdraw assets up to the current reserve ratio. If you've used protocols such as Aave or Compound in the past, you'll be familiar with this.

We strongly advise not borrowing right up to the limit, however, as the result of this will be that your market becomes delinquent after the very next non-static call which updates the market state and rebases the market token supply.

#### Repaying A Market

The primary mechanic by which funds are recalled by lenders is through **withdrawal requests**, which isolate assets currently in reserve in a market for lenders to claim at the end of a withdrawal cycle (for more details on this, please refer to the [**Lenders**](lenders.md) page).

Withdrawal requests impact the reserve ratio of your market, and as such a good borrower is minded to monitor their reserve ratios to determine when funds are being requested. Requests (including who has placed the request and for how much) are also logged within the Market Details page.

The act of repaying is simple in the sense that it just requires transferring assets back to the market contract via a standard ERC-20 transfer. Further, _anyone_ can repay assets to the market in this way - we've permitted this in case the borrower address is compromised. In this case, all lenders can file withdrawal requests, assets can subsequently be repaid from a third party, and - due to the manner in which withdrawal requests sequester assets during a withdrawal - can be honoured through the market contract without the compromised borrower address being able to access any assets.

#### Reducing APR

The interest rate on a market is fixed at any given point in time (i.e. markets do not make use of a utilisation-rate based curve), however the borrower is free to adjust this rate step-wise should they wish.

Should a borrower wish to increase the APR of a market in order to encourage additional deposits, they are able to do so without issue.

Should they wish to _decrease_ the APR, however, the controller of that market will likely require a temporarily increased reserve ratio (which will hold in place for some time) before the change, in order to provide liquid reserves to lenders who disagree with the rate decrease and wish to exit (for more details on this, please see the [**Lenders**](lenders.md) page). The exact amount of this reserve ratio increase is controller-dependent: it could be a flat requirement of a 90% reserve ratio, it could be the larger of the current ratio or the relative difference between the old and new rates, or a third, more complex thing.

#### Altering Capacity

As a borrower, you are able to adjust the capacity up or down as you please. However, reducing the capacity below the current supply does not release you from your obligation to that supply: interest will still accrue on the outstanding supply until such time as lenders reduce the supply through withdrawal requests that burn market tokens, and your required reserves remain unchanged.

#### Closing A Market

In the event that a borrower has finished utilising the funds for the purpose that the market was set up to facilitate (or if lenders are choosing not to withdraw their assets and the borrower is paying too much interest on assets that have been re-deposited to the market), the borrower can _close_ a market at will.

This is a special case of reducing the APR (with the associated increased reserve rate that accompanies it). When a market is closed, sufficient assets must be repaid to increase the reserve ratio to 100%, after which interest ceases to accrue and _no further parameter adjustment or borrowing is possible_. The only thing possible to do in a closed market is for the lenders to file withdrawal requests and exit.

#### Removal From The Archcontroller

For whatever reason, it may be the case that the Wildcat protocol itself no longer wishes to permit a given borrower to interact with it. In this case, the address(es) of a borrower are removed from the archcontroller.

If this happens, the borrower can no longer deploy _new_ controllers or markets. However, they are still capable of interacting with _existing_ markets - the protocol cannot force these closed.
