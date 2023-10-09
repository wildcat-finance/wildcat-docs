# What Wildcat Enables

The core premise of a Wildcat market is fairly simple: borrowing and lending between two parties - but that simplicity belies creative applications.

Consider the following examples - all are well served by making use of Wildcat:

* Acquiring temporary inventory to provide a market spread for an asset,
* Bringing long-dated call options on new assets on-chain,
* Raising funds without issuing a token immediately (foregoing an initial LBP), or
* Issuing interest-bearing variants of assets held in escrow, creating an on-chain quasi-'bond' with the borrower as counterparty and source of yield,

You will have seen these use-cases before, associated with other protocols. What's different here is the amount of freedom the borrower has, provided with a novel mechanism for scheduling redemptions on behalf of lenders. However, Wildcat is very much tilted towards borrowers in the sense of who stands to benefit the most from the differences: they are responsible for maintaining the health of their markets, but this comes with substantial power to dictate their terms.

If you have admin costs associated with middle and back-office functionality because you're handling loans OTC via Telegram or the like, you're probably going to find using a Wildcat market useful, since you can track everything using associated events.

If you're trying to raise funds more generally (i.e. you're a legal entity associated with a DAO that wants to pay salaries without selling a native token to do so at the moment), a Wildcat market may prove convenient to you as well.

With that said, it's not our place to proscribe what Wildcat _should_ and _shouldn't_ be used for - tokenised lending instruments have a wide scope, and we've intentionally designed the protocol to be as hands-off as possible. Beyond vetting borrowers (to confirm that they are, in fact, extant legal entities that don't operate in sanctioned countries), we can't and don't get involved in the interactions between borrower and lender(s).

Please note that as a lender, counterparty risk is very real: usage of this protocol requires trust in your borrower - Wildcat provides no insurance fund for defaults, and the collateral provided comes from _you_ in the form of the reserve ratio selected by your borrower in the market you are lending to them through. To re-emphasise: the protocol cannot help you if your borrower disappears with your assets.

We're looking forward to seeing what you use us for.

