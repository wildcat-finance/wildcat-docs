# Lenders

### Deposits

To fill in.

### Withdrawals

Withdrawals are handled slightly differently within Wildcat markets than in other protocols you might be used to interacting with,

To that end, this section provides a brief guide to how withdrawals are processed, and the ways in which you reclaim assets from a market that you have requested, either in full or _pro rata_ depending on the reserves currently in the market and how many other lenders are simultaneously requesting a withdrawal.

Wildcat does not permit immediate withdrawals - rather, the borrower that you are lending to specified a **withdrawal cycle** length when creating the market you are attempting to withdraw from.

A withdrawal involves:

* Burning your market tokens at a 1:1 rate to the amount that you wish to withdraw (there is a caveat to this depending on the amount of reserves currently in the market),
* Waiting for the withdrawal cycle period to elapse (either the full period if you were the request that kickstarted the cycle, or the remainder if you placed the request in the middle of a cycle),
* Claiming the assets that are made available to you at the end of the cycle.

#### The Reserved Assets Pool

Within a given market, there is a **reserved assets pool** - a 'side-pot' containing assets that are still technically within the market, but have been claimed by a lender via a withdrawal request. Assets that are placed within this pool are unavailable to the borrower (they are considered to be removed from the market supply), and the **reserve ratio** of a market does not factor them in.

When you request a withdrawal, whether you are required to burn your market tokens or not depends on whether there are any reserves that are _not_ yet in the reserved assets pool.

* If there are reserves in the pool that are not in the reserved assets pool, then you can burn market tokens that you hold at a 1:1 rate in order to move those reserves into the pool. If there is no current withdrawal cycle ongoing, this action begins the countdown for a new cycle.
* If all assets within the market are currently within the reserved assets pool (or there are no reserves in the pool to speak of at present), then your withdrawal request is logged internally, but you are not required to burn any market tokens (as there is nothing to move into the pool).

Once the withdrawal cycle completes, then lenders are able to withdraw \[complete]

The reserved assets pool 'persists' through distinct withdrawal cycles - if \[complete]&#x20;

\[discuss the situations in which claiming < requested]
