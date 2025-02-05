---
description: How to make use of the Wildcat protocol.
---

# Onboarding

The Wildcat protocol is fundamentally permissioned in both roles that it is possible to fill while using it. \
\
The owners of a given Wildcat deployment grant permission to borrowers to deploy markets, whilst borrowers are the ones that determine which categories of lenders are able to interact with the markets that they deploy.

## Borrowers

Borrowers who wish to make use of Wildcat are encouraged - on the landing page and the protocol UI itself - to get in touch via the landing page, or reach out directly to [contact@thewildcat.foundation](mailto:contact@thewildcat.foundation).\
\
At present, Wildcat is only accepting registered legal entities as borrowers. In time, individual retail lenders may be permitted as borrowers.

The operations team of Wildcat Foundation will get in touch in time, and seek to perform a KYB/C check that is on par with what is expected when onboarding to a centralised exchange. This covers such aspects as certificates of incumbency, proofs of address/identity of persons with significant control and directors.

Following this, Wildcat requests an Ethereum address, which will be registered on-chain as a borrower capable of deploying hooks instances and markets to the [**archcontroller**](terminology.md#archcontroller).

After this point, Wildcat steps back.

## Lenders

If you're a party that wishes to lend to a particular borrower, Wildcat itself does not onboard you.

Rather, the process is determined by the [policies](day-to-day-usage/market-access-via-policies-hooks.md) in place for a particular market, as these are what grant you a credential 'through' the market hook that gates deposit access.

It's hard to abstract the above into a 'this is how you onboard into market X' for this documentation, because one borrower may be content that you are not subject to a sanctions designation, another require you to reach out to the borrower and get explicitly whitelisted, another may require you to pass a third-party KYC/B check to verify your jurisdiction and that you're accredited (or whatever other requirement the borrower has), and another still may be content to accept a [Coinbase Verification](https://www.coinbase.com/en-gb/onchain-verify) or [Binance Account Bound Token](https://www.binance.com/en-GB/babt) (which we haven't got hooks for yet, but we will soon!).

Wildcat does not decide what a particular borrower should demand in terms of lender onboarding, as we consider this a compliance/legal issue for each borrower depending on their location, risk appetite and purpose. However, the protocol UI provides contact points for borrowers through their borrower profile page (i.e. email, Telegram, Twitter), and each market will also indicate the requirements that are in place for obtaining deposit credentials.

In most cases, we envisage that you will be able to receive a deposit credential for a market without ever reaching out to a borrower directly, although that option is of course available to you.

Credentials may not last forever depending on borrower configuration, and may require periodic refreshing if you wish to deposit again in the future.

In Wildcat V2, addresses that have previously deposited assets or received market tokens (the debt of a market) while holding a valid deposit credential are _always_ be able to make withdrawal requests, even if their deposit credential has expired. For this reason, we encourage that you make use of a hardware wallet or a multisig when engaging with Wildcat.

There's some more detail on this available [here](day-to-day-usage/market-access-via-policies-hooks.md), and we will provide a clearer walkthrough once live.

Note that addresses which are flagged as sanctioned by the [Chainalysis oracle contract](https://go.chainalysis.com/chainalysis-oracle-docs.html) are prevented from interacting with the protocol at the code-level - although it's a _brave_ entity that tries either asking for or seeking to extend credit from any of these.&#x20;
