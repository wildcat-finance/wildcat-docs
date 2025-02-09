---
description: There's no such thing as a free lunch.
---

# Protocol Usage Fees

Wildcat has the ability to charge a fee for the usage of its markets.

Once a borrower has been added to the global registry by the archcontroller, they have free reign to deploy markets however they see fit, both in market parameters themselves (e.g. capacity, withdrawal period) and which hooks are in place to gate access.

However, there is one parameter associated with a market that a borrower cannot change: the _protocol fee._ This manifests as:

* an _origination fee_ (which must be paid during the deployment of a market),
* a 'streaming' proportion of base APR which accrues over the supply of assets rather than the capacity (meaning that its' presence doesn't cause market tokens to rebase any faster), or
* both.

The borrower that deploys a market with a base APR of 10% that has a 5% streaming protocol fee in place will find themselves paying 10.5% (the base APR receivable by lenders plus 5% of that rate). The lender will receive 10% as expected, the rest accrues to the protocol over time.

Decreasing or increasing that APR will similarly adjust the actual protocol fee APR: reducing the base APR to 8% will result in a borrower paying 8.4%.

Protocol fees do _not_ increase in the presence of a penalty APR if a market is delinquent and over the grace period: if a market has a base rate of 10% and is currently paying an additional penalty APR of 20%, the total market APR is 30.5% ((10% + 0.5%) + 20%), _not_ 31.5%.

Protocol fees accrued as part of a market APR are senior to lender claims within a market - a lender who attempts to withdraw all of the reserves within a market will only be capable of removing that amount net any protocol fees that have accrued over time and not been withdrawn.\
\
The fee configuration of an active market can be adjusted by the archcontroller owner, and changes are retroactive in V2 markets.

If your market launched with a 0% streaming protocol fee which is subsequently increased to 5%, that fee will start to take effect after the appropriate hook instance contract tied to a market is updated. Any origination fee update will be rendered void for existing markets (since the market exists already!).

At the time of the Wildcat V2 launch, the fee was set at **5% streaming and no origination fee**.

In Wildcat V2, streaming protocol fees are hard-capped at 10% of base APR.





