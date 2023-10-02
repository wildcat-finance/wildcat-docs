# Borrowers

#### Launching A New Market

For the purpose of this section, we assume that the borrower has already gotten in contact with the Wildcat protocol team itself and jumped through the hoops to be added as a whitelisted borrower on the **archcontroller** (the registry that tracks permissions and deployments).

Once this is done, the borrower can go to the protocol UI, and having signed the Service Agreement (if not done already), navigate to the Borrower section, and then click New Market.

There are a number of parameter fields that are presented here, and the screen may appear a bit overwhelming, but they fundamentally represent the degrees of freedom you have available to you. They are:

* **Market type**
  * Dropdown menu indicating what flavour of market you wish to deploy (e.g. vanilla borrowing, call option agreement, permissionless).\
    \
    Each distinct market type is enabled by a distinct **controller** variant - what you are actually picking here is the _type_ of controller which deploys your market.\

* **Underlying asset**
  * This is the asset that you wish to borrow, such as DAI or WETH. \

* **Vault token name prefix**
  * The prefix string that the **market token** issued to represent debt will use. For example, if you are borrowing _DAI_ (_Dai Stablecoin)_ and enter '_West Ham Capital_' here, the name of the market token will be _West Ham Capital Dai Stablecoin_.\

* **Vault token symbol prefix**
  * The prefix string that the market token issued to represent debt will use. For example, if you are borrowing _DAI_ (_Dai Stablecoin)_ and enter 'WHC' here, the symbol of the market token will be _WHCDAI_.\

*   **Maximum amount I want to borrow**

    * This represents the initial **capacity** of the vault - the maximum amount of debt that you're willing to pay interest on at launch. Note that depending on what you set the **reserve ratio** as, this does _not_ correspond to the amount that you are able to **borrow** from the market when fully subscribed.


* **Reserve ratio**
  * The percentage of the market **supply** that must remain _within_ the market available for redemption. For example, a market with a capacity of 100,000 tokens, a supply of 20,000 tokens and a reserve ratio of 25% must have 5,000 tokens within the market ready for lenders to withdraw.\
    \
    Failing to maintain this level will result in the market becoming **delinquent**.\
    \
    Note that the capacity and the reserve ratio together dictate the _maximum_ that you are able to borrow from a market. A higher reserve ratio leads to a greater amount that you are paying interest on, but provides more of a cushion for lenders to easily exit their position, presuming that you fix delinquencies in a timely manner (lest you incur the _penalty fee_, see below).\

* **Base interest rate (APR)**
  * The amount of interest that you are willing to pay on deposits to _lenders_. This is the rate that will apply presuming that your vault never stays delinquent for long enough for the **penalty rate** to activate.\
    \
    Note that dependent on controller, this may not be the final APR - markets deployed via controllers that utilise a **protocol fee** will add that rate onto the base rate (e.g. selecting a base rate of 10% for a market that includes a 20% protocol fee produces a final rate for the borrower of 10% + (0.2 \* 10%) = 12%.\

* **Penalty fee rate (APR)**
  * The amount of _additional_ interest that you agree to pay in the event that your market becomes **delinquent** (i.e. falls below the reserve ratio) and the delinquency is not resolved within the amount of time specified by the **grace period**, as observed by the **grace tracker**.\
    \
    This penalty rate is added on to the base rate only for as long as the value of the grace tracker is above that of the grace period.\

* **Grace period**
  * The amount of time that a market is permitted to be delinquent for before the penalty APR activates. This parameter is measured in hours, and comes with a corresponding (internal) variable called the **grace tracker**, which measures the amount of time for which the market has been delinquent.\
    \
    The grace period is a _limit_: once delinquency has been cured within a market, the grace tracker will count back down to zero from whatever value it had reached, and any penalty APR that is currently in force will only cease to do so after the grace tracker value is once again below the grace period.\

* **Withdrawal cycle**
  * The amount of time that a lender who has filed a withdrawal request must wait before they are permitted to claim their assets from the market. This parameter is measured in hours, and _can_ be set to zero in order to enable instant withdrawals.\
    \
    This parameter exists in order to fairly distribute assets across multiple lenders given the undercollateralised nature of Wildcat markets. In the event that a significant amount of the supply is recalled at once, a longer withdrawal cycle permits reserves to be handed out _pro rata_ depending on the reserves within the market. For more on how this looks from the lenders perspective, please see the **Lenders** page.

Provided that all of these parameters are within range for the market type you are deploying (and these can vary on a per-controller basis), you will then be asked to submit a transaction which first deploys a controller of the correct type from the controller factory, and subsequently deploys a vault parameterised as you have directed.

Final note: each borrower address is constrained to owning one instance of a controller per variant, but a borrower can deploy several markets with the same underlying asset against such a controller provided that the name and symbols are unique.



#### Borrowing



#### Repaying
