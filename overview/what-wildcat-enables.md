# What Wildcat Enables

The core premise of a Wildcat market is simple: enabling undercollateralised borrowing and lending.

You will have seen this use-case before, associated with other protocols. What's different here is the amount of freedom the borrower has in how their market is shaped and constrained, alongside a novel mechanism for scheduling redemptions on behalf of lenders.\
\
Borrowers are responsible for maintaining the health of their markets, but this comes with substantial power to dictate their terms.\
\
Conversely, Wildcat is designed so that lenders both know where they stand and can deploy capital in places that they perhaps did not expect.

### For Borrowers

A borrower may wish to create a completely uncollateralised market to borrow 4,000,000 USDC paying 15% to lenders that deposit into it, where they have seven days to repay any withdrawal request they receive before an additional penalty rate of 10% kicks in. They may also wish to set it up such that lenders cannot withdraw for the first six months that the market exists (thereafter switching to open-term), that they must deposit at least 100,000 USDC per transaction and they must prove that they are not sanctioned by OFAC before they can deposit. The debt tokens issued by the resulting market can either be freely tradable, constrained to other approved lenders, or completely locked down.

Wildcat enables this and much more, depending on the selected market configuration.

If you have admin costs associated with middle and back-office functionality because you're handling loans OTC via Telegram or the like, you're probably going to find using a Wildcat market useful, since you can track everything using associated events and other features provided through the protocol UI.&#x20;

If you're trying to raise funds for operational purposes (i.e. you're a legal entity associated with a DAO that wants to pay salaries without selling a native token OTC or into on-chain liquidity to do so), a Wildcat market may prove convenient to you as well.

In crypto/DeFi we often speak at length about how one of the remaining holy grails is an effective reputation/credit risk metric tied to on-chain wallets. However, this suffers from a cold start problem: it's hard to infer any meaningful information when previous wallet interactions _typically_ involve overcollateralised mechanisms or those which offer no real insight into probability of default. We consider honest usage of Wildcat by borrowers an effective bootstrap mechanism upon which such reputations can be built.

### For Lenders

From the lender perspective, the goal of Wildcat is to open up a number of competitive avenues for you to deploy capital: it may not have even dawned on you that some of the borrowers making use of Wildcat would be willing to accept your funds!

Wildcat provides you with a way to direct credit towards a specific counterparty that you may know and trust, rather than into a pool which is distributed across several borrowers.

Wildcat also makes use of fixed rates, which - while adjustable in circumstances where you can ragequit if the rate is no longer to your liking or you reckon you can get better rates elsewhere - provides a measure of certainty, compared to systems using dynamic rates wherein a borrower can drop your APR significantly simply by repaying a large chunk of their debt.

Wildcat V2 enables borrowers to set up structures such as Masterchef contracts on top of their markets: a borrower may offer you a given rate of interest, but also stream additional tokens to you as an additional incentive for you to provide credit. We can easily envisage this being used as a liquidity mining mechanism of sorts, should it be opted for.

The undercollateralised nature of Wildcat markets - and the fact that the asset loaned and borrowed is the same - means that reserves _within_ a market cannot be 'liquidated' in order to repay lenders requesting a withdrawal: lenders are dependent on the borrower for repayment of outstanding debt.

However, Wildcat V2 will - shortly after launch - support optional collateral contracts which borrowers can deploy and place alternative assets into, which _can_ be liquidated and repaid to the market in the event that market reserves drop below their necessary level (i.e. you have asked for your deposit back and the borrower has taken too long to get it back into the market).

Finally, Wildcat has drawn up and open-sourced a Master Loan Agreement that is cognisant of the fact that your engagement is in fact a credit agreement taking place on-chain between yourself and the borrower. We encourage lenders to sign it if the borrower has opted to make use of it.

**Put simply, with Wildcat, you know what you're getting, because you chose it.**

Now, a bit that we need to include here so that we don't accidentally taunt a regulator:

Wildcat does not provide any assurances or underwriting regarding the financial health or creditworthiness of a borrower. Markets will - in the fullness of time - include reference to external reports or dashboards attesting to borrower assets where they exist, but lenders are expected to exercise their judgment as to whether Borrower X is likely going to be good on their word.&#x20;

Counterparty risk is very real, and usage of this protocol requires trust in your borrower: Wildcat provides no insurance fund for defaults, and cannot help you if a borrower disappears with your assets. There is risk here beyond the usual on-chain vectors: _hic sunt dragones_.&#x20;

### Interested?

It's not our place to proscribe what Wildcat _should_ and _shouldn't_ be used for - tokenised lending instruments have a wide scope, and we've intentionally designed the protocol to be as hands-off and abstract as possible.&#x20;

As a settlement layer, consider the protocol itself to be an Uatu the Watcher figure: we're interested, and we're watching, but it will not and _cannot_ interfere.

We're looking forward to seeing how you make use of us!

