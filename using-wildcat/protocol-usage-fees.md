---
description: There's no such thing as a free lunch.
---

# Protocol Usage Fees

Wildcat takes a fee for the usage of markets deployed using it. The fee is variable, and depends on the _controller_ that underpins a given market.

Once a borrower has been added to the global registry by the archcontroller, they have free reign to deploy markets with whatever combination of parameters they see fit to.

However, they do so by first deploying a controller contract that is both specific to them and supports the functionality that they wish to utilise. There are distinct variants of controller, and each of them are suited to particular circumstances. For example -&#x20;

* **Controller Null is the MVP launch controller (basic functionality, limited access),**
* Controller Alpha is the general launch controller (basic functionality),
* Controller Beta might permit the deployment of long-dated call option markets,

\- and so on.&#x20;

Each controller has a specified protocol fee, which either manifests as an origination fee (which must be paid during the deployment of a market), or as a proportion of base APR, which accrues over the supply of assets rather than the capacity.\
\
**Controller Null - used in the launch stages - is likely to have a symbolic protocol origination fee and no protocol APR fee. Controller Null is a test, and will not be made widely available.**\
\
Controller Alpha will have a protocol fee of 20% of the current base APR.

The borrower that deploys a market through their own Controller Alpha instance with an APR of 10% will find themselves paying 12% (the base APR receivable by lenders plus 20% of that base rate).

Decreasing or increasing that APR will similarly adjust the actual protocol fee APR.

Protocol fees do _not_ increase in the presence of a penalty APR if a market is delinquent and over the grace period: if a market deployed through Controller Alpha has a base rate of 10% and is currently paying an additional penalty APR of 20%, the total market APR is 32% ((10% + 2%) + 20%), _not_ 36%.

Protocol fees are claimed by either the archcontroller or the designated fee recipient of a market.

Protocol fees accrued as part of a market APR are senior to lender claims within a market - a lender who attempts to withdraw all of the reserves within a market will only be capable of removing that amount net any protocol fees that have accrued over time and not been withdrawn.

