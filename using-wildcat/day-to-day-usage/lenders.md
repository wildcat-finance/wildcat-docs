---
description: Things you need to know as a would-be lender through Wildcat.
---

# Lenders

## Making Deposits

Depositing assets to a Wildcat market is a fairly simple process, but depends somewhat on the policy in place for said market.

With that said, the first thing we want you to remember is that _Wildcat does not underwrite these markets or provide any guarantees as to whether or not the borrower is guaranteed to repay them._ We keep harping on about this, but it really does bear repeating.

Moving on: this is what you're faced with when you get to the main lender dashboard.

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption><p>Note that the lender has active loans to three markets - the 'No Active Markets' under the 'Non-Deposited' is indicative of the fact that there are no markets where the lender has been explicitly onboarded to by a borrower (or otherwise holds an access credential) and they haven't deposited any assets yet. This might be confusing, let us know if that's the case! </p></figcaption></figure>

To look for a new market, you can either click _Other Markets_ in the table itself, or the **Observe New Markets** button in the top-right.

At this stage, there are two types of markets: ones where you can onboard yourself provided that you are not OFAC-sanctioned, and ones where you must be explicitly onboarded by the borrower.

<figure><img src="../../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>

Note that if you try to enter a market which requires borrower onboarding, you will only be able to view descriptive statistics plus the market history.

<figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption><p>You can reach out to the borrower through one of the methods available on their borrower profile if you want to ask about being added (click the blue underlined borrower name for that market).</p></figcaption></figure>

Upon entering a self-onboarding market, if the borrower has specified that this market is to be bound by one, the lender will be asked to countersign the associated Wildcat Master Loan Agreement (MLA) parameterised for the specific market terms.

<figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

Note that dependent on the borrower, this may not be in place: for all Wildcat itself knows, you may be looking to lend to a market which you've been added to an allow-list for having signed a separate agreement which you may be asked to sign off-chain. If the market does not offer an MLA, the UI simply presents you with the ability to deposit.

To sign the MLA, click the View/Sign MLA button, scroll to the bottom, and sign with your wallet. No pesonal details other than your wallet address and your ECDSA signature will be stored: this is sufficient to prove that you've accepted it (and can enforce it against the borrower if needed down the line).

Once you've signed it, you're faced with the following:

<figure><img src="../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

After this point provided that the lender holds some of the [**underlying asset**](../terminology.md#underlying-asset), and there is [**capacity**](../terminology.md#capacity) in the market, the lender is able to deposit as much of the asset as they are willing to (or up to the capacity), receiving in exchange a 1:1 amount of the [**market token**](../terminology.md#market-token) associated with that particular market. The lender that deposits 133.7 XYZ tokens into a market will receive 133.7 market tokens - with the market token name depending on what was selected by the borrower when the market was launched: e.g. wildcatXYZ.

<figure><img src="../../.gitbook/assets/image (8).png" alt=""><figcaption><p>This particular market has a minimum deposit amount, but otherwise it's the same<br>pattern you're used to from everywhere else that you know and love.</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (9).png" alt="" width="369"><figcaption><p>These are mock tokens on Sepolia, but tokens in, debt tokens out.</p></figcaption></figure>

Market tokens are _rebasing_ - depositing 1,000 tokens of an underlying asset into a market offering 10% base APR will result in a wallet balance of 1,100 market tokens after a year, giving rise to a claim on 1,100 tokens of the underlying.

Wildcat market tokens differ somewhat from aTokens/eTokens from Aave and Euler in that they do not have an internal exchange rate whereby 1 market token will be worth - for example - 1.05 of the underlying asset after a year. Rather, after every interaction with the market that changes the state, market token balances will be adjusted to maintain the 1:1 ratio between market tokens held and the claim of each lender.

Depending on the constraints placed upon the markets, lenders _may_ be able to transfer market tokens freely (you can send them to a cold wallet, you can LP them, you can build additional infrastructure around them). Borrowers are able to constrain transfers to only those addresses that hold an unexpired deposit credential or are marked as known lenders, or completely prevent transfers except for those to/from the market contract. Check the details of your particular market via the protocol interface, it's all explained there.

<figure><img src="../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

If your address has ever deposited to a market or received market tokens while holding a valid deposit credential, you will be marked as a known lender, and always be allowed to place withdrawal requests for that market. If the market permits it and Lender A sends their market tokens from their depositing wallet to a secondary one, those markets must either be sent back to the original wallet in order to claim, or the secondary wallet address must also become a known lender.

## Making Withdrawals

[**Withdrawals**](../terminology.md#withdraw) are handled slightly differently within Wildcat markets than in other DeFi protocols you might be used to interacting with.

To that end, this section provides a brief guide to how withdrawals are processed, and the ways in which you reclaim assets from a market that you have requested, either in full or _pro rata_ depending on both the reserves currently in the market and how many other lenders are simultaneously requesting a withdrawal.

Wildcat does not permit immediate withdrawals - rather, the borrower that you are lending to specified a [**withdrawal cycle**](../terminology.md#withdrawal-cycle) length when creating the market you are attempting to withdraw from.

A withdrawal involves:

* Transferring the total number of market tokens corresponding to your requested amount to the market, which are either burned immediately or held to be burned (which one happens depends on the amount of reserves currently in the market),
* Waiting for the withdrawal cycle period to elapse (either the full period if you were the request that kickstarted the cycle, or the remainder if you placed the request in the middle of a cycle), and then
* Claiming the assets that are available to you at the end of the cycle.

If your market is Open Term (i.e. you can place withdrawals requests at any time, the dashboard for your market will allow you to access a Withdrawal button):

<figure><img src="../../.gitbook/assets/image (12).png" alt=""><figcaption><p>I went and took this image after the one below, no one ever accused me of being good at this.</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

However, if your market is Fixed Term, then you will not be able to place a withdrawal request until such time as that maturity passes (well, either that or the market is closed by the borrower), and as such the Withdraw button is hidden from you

<figure><img src="../../.gitbook/assets/image (13).png" alt=""><figcaption><p> We did this because we, as its' developers, got confused at one point as to why we weren't able to place withdrawal requests.</p></figcaption></figure>

### The Unclaimed Withdrawals Pool

Within a given market, there is a unclaimed withdrawals pool - a 'side-pot' containing reserves that are still technically 'within' the market, but have been earmarked for withdrawal by lenders via a _withdrawal request_. Assets that are placed within this pool are unavailable to the borrower (they are considered to be removed from the market supply), and the [**reserve ratio**](../terminology.md#reserve-ratio) of a market does not factor them in.

When you request a withdrawal, whether any of the market tokens you transfer to the market are burned or not depends on whether there are any reserves that are _not_ yet in the unclaimed withdrawals pool.

* If there are reserves in the pool that are not in the unclaimed withdrawals pool, then market tokens are burned at a 1:1 rate in order to move those reserves into the pool. If there is no current withdrawal cycle ongoing, this action begins the countdown for a new cycle.
* If all assets within the market are currently within the unclaimed withdrawals pool (or there are no reserves in the pool to speak of at present), then your withdrawal request is logged, but no market tokens are burned after you transfer them (as there is nothing to move into the pool). Instead, you tokens will burn as assets become available (see below).

### Claiming

<figure><img src="../../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

Once a withdrawal cycle completes, then lenders who made withdrawal requests during that cycle are able to _claim_ assets that they requested from the unclaimed withdrawals pool, subject to the following:

* If there are enough assets in the unclaimed withdrawals pool to cover the total amount requested for withdrawal in that cycle, then the lender can claim the full amount of their requested withdrawal.
* In the scenario where the total amount requested (across several lenders) exceedes the amount in the unclaimed withdrawals pool, then the lender is able to claim a _pro rata_ amount of the assets in the reserved pool proportional to the size of _their_ overall withdrawal amount compared to the total. To illustrate:
  * If Lender A requested a withdrawal of 10,000 tokens from a pool with 5,000 tokens in reserve, they would be able to withdraw all 5,000 if they were the only lender in that withdrawal cycle.
  * In the event that Lender B requests a withdrawal of 40,000 tokens in the same cycle, however, Lender A would only be able to claim 1,000 tokens while Lender B would be able to claim 4,000 (because 10,000 : 40,000 is a 1:4 ratio).
  * Note in this scenario that Lender A - if they requested the withdrawal first - would have had half of their market tokens burned to place these 5,000 assets in the unclaimed withdrawals pool, while Lender B had none burned. Rather, Lender B's market tokens will be burned later on as assets are repaid by the borrower.
  * The above situation leaves Lender A having burned 5,000 market tokens and only able to claim 1,000 - the discrepancy here is logged, and is resolved as the overall outstanding amount is paid off by the borrower.

<figure><img src="../../.gitbook/assets/image (14).png" alt=""><figcaption><p>Example of the lender's perspective when a withdrawal cycle is ongoing.</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

### Expired Claims and The Withdrawal Queue

Any withdrawal amounts that cannot be honoured at the end of a withdrawal cycle (either due to the assets in market reserves being insufficient, or due to a _pro rata_ claim on assets within the unclaimed withdrawals pool) are batched together, marked as 'expired' and placed into a queue.

Subsequent repayments by the borrower to a market with a non-zero queue will route assets to the unclaimed withdrawals pool in the amounts required to fully honour _all_ expired claims _in the order that they were initiated_ - only after this obligation is met do repaid assets start counting towards the reserve ratio of a market.

To illustrate in some depth (this is pretty picky stuff, no harm no foul if you don't read it):

* A market with capacity 50,000 has a supply of 40,000 tokens, and 10,000 tokens in reserve (for a reserve ratio of 25%).
* Lender A makes a withdrawal request for 15,000 tokens, moving 15,000 market tokens to the market and burning 10,000 of them to move the reserves to the unclaimed withdrawals pool (reserve ratio now 0%).
* The supply of the market is reduced to 30,000 tokens (10,000 burned).
* Lender B makes an additional withdrawal request in the same cycle for 5,000 tokens: there are no assets in reserve to move, so no market tokens are burned.
* The withdrawal cycle period elapses.
* There is a total of 10,000 tokens in the unclaimed withdrawals pool and an outstanding claim of 20,000 tokens from both lenders:
  * Lender A can claim 7,500 tokens,
  * Lender B can claim 2,500 tokens,
* Lender A now has an outstanding claim of 7,500 tokens (2,500 of which have been 'pre-paid' in the sense that an extra 2,500 market tokens were burned than they were able to access), and Lender B has an outstanding claim of 2,500 tokens.
* This claim of a total of 10,000 tokens is marked as expired and placed in the queue as **Batch A.**
* Lender C starts a new withdrawal cycle by requesting a withdrawal of 5,000 tokens. As with Lender B, no reserves means no market tokens are burned.
* This second withdrawal cycle elapses, and a second expired claim for 5,000 tokens is added to the queue as **Batch B.**
* At this point, the borrower returns 13,000 tokens to the market.
* These tokens are immediately placed into the unclaimed withdrawals pool, and since the amount returned is less than the total amount outstanding in the queue (15,000), the reserve ratio of the market remains at 0%.
* Since the unclaimed withdrawals pool now contains enough assets to fully honour Batch A, the remaining 10,000 market tokens held by the market and associated with this batch are burned.
* Both Lender A and Lender B can now claim the remainder of their withdrawal request amounts.
* After factoring in the assets to honour Batch A, Batch B has 3,000 assets against a 5,000 claim. 3,000 of the market tokens transferred by Lender C are burned, and so Lender C can claim 3,000.
* **Important:** even though the 13,000 tokens returned to the market were in excess of the 5,000 token claim of Lender C, they were only eligible to claim that part in excess of the amount owed to the previous batch in the queue .
* If all of these claims are processed, the Batch A is eliminated from the queue, leaving only a 2,000 token claim for Lender C.
* If the borrower subsequently returns an additional 11,000 tokens to the market at this point, then 2,000 are again assigned to the unclaimed withdrawals pool, burning the remaining 2,000 market tokens associated with Batch B.
* The remaining 9,000 are now considered 'true' reserves, bringing the reserve ratio of the market back up to 9,000 / 15,000 = 60%.

One final point: if there are multiple lenders in a batch, and the batch can only be partially honoured (via a return of less than the total amount due), then each individual lender in the batch can only claim a pro-rata amount of the assets isolated to that batch.

Phrased differently: if a batch has been 60% honoured with deposited assets, then each lender can only withdraw 60% of their outstanding claim, until such time as more assets arrive to completely honour the batch.

This logic can be _very_ confusing when first encountering it, so please ask us if there's any particular part you'd like us to expand on differently!
