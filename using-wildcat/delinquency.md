---
description: What it means for a market to be delinquent, and what the impact is.
---

# Delinquency

Any given Wildcat market contains a reserve ratio that dictates what percentage of the assets that are currently being loaned must be available to be withdrawn at any given moment by lenders.

This ratio applies to the current _supply_ of assets to the market. If a market exists that has a capacity of 10,000,000 USDC and a reserve ratio of 20%, the reserve ratio does not apply to that capacity figure unless the market is fully subscribed.

Rather, if the market has a supply of 4,000,000 USDC from lenders, then 800,000 USDC must be in reserve. The amount required by reserves inflates as interest accrues, since the market token and underlying asset are exchangeable 1:1.

A market that goes below the reserve ratio by way of lender withdrawals, it is considered _delinquent_.

When creating a market, another two parameters were needed:

* The penalty APR: fill out
* The grace period: fill out

\---

How reserve ratios change with pending withdrawals (100% collateralisation)

how the grace tracker works when heading over and back

