---
description: There's no such thing as a free lunch.
---

# Protocol Usage Fees

Wildcat takes a fee for the usage of vaults deployed using it. The fee is variable, and depends on the _controller_ that underpins a given vault.

Once a borrower has been added to the global registry by the archcontroller, they have free reign to deploy vaults with whatever combination of parameters they see fit to.

However, they do so by **first** deploying a controller contract that is both specific to them and supports the functionality that they wish to utilise. There are distinct variants of controller, and each of them are suited to particular circumstances. For example -&#x20;

* **Controller Null is the MVP launch controller (basic functionality, limited access),**
* **Controller Alpha is the general launch controller (basic functionality),**
* Controller Beta might permit the deployment of long-dated call option vaults,

\- and so on.&#x20;

Each controller has a specified protocol fee, which either manifests as an origination fee (i.e. it must be paid during the deployment of a vault), or as a proportion of vault APR.\
\
**Controller Null - used in the launch stages - has a protocol origination fee of 100 USDC.**\
**Controller Alpha has a protocol fee of 20% of the current vault APR.**

The borrower that deploys a vault through their own Controller Alpha instance with an APR of 10% will find themselves paying 12% (the base rate receivable by lenders plus 20% of that base rate).

Decreasing or increasing that APR will similarly adjust the actual protocol fee APR.

Protocol fees are claimed by either the archcontroller or the designated fee recipient of a vault.

Protocol fees accrued as part of a vault APR are senior to lender claims within a vault - a lender who attempts to withdraw all of the reserves within a vault will only be capable of removing that amount net any protocol fees that have accrued over time and not been withdrawn.

