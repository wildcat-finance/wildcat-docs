---
description: How to make use of the Wildcat protocol.
---

# Onboarding

The Wildcat protocol is fundamentally permissioned in both roles that it is possible to fill while using it. \
\
The operators of the Wildcat protocol grant permission to borrower candidates to deploy markets, whilst borrowers are the ones that determine which categories of lenders are able to interact with the markets that they deploy.

## Borrowers

Borrowers who wish to make use of Wildcat are encouraged - on the landing page and the protocol UI itself - to get in touch via this [**form**](https://forms.gle/irca7KeC7ASmkRh16).

After first contact, what Wildcat is looking for is proof that the borrower is a legal entity in a jurisdiction that is a) not sanctioned, and b) we reasonably believe won't expose the protocol to legal or regulatory risk. Discretion is currently being exercised in that we seek to reach 'up', meaning that we are more likely to accept recognised market makers, trading desks, protocols and such as borrowers. That's not to say that your smaller, less-recognised entity has a more significant probability of default: it very likely doesn't!

We be asking what you intend to utilise Wildcat credit lines _for_, checking that you're a going concern, who your ultimate beneficiaries are and so on. We may request that you either send us documents directly so we can keep records, or engage with a third-party KYB service (such as SumSub or the like) - we'll let you know at the time.

In short, this stage can be summarised as: play ball with us and be honest.

Following this, Wildcat requests an Ethereum address, which will be added as a borrower capable of deploying hooks instances and markets to the [**archcontroller**](terminology.md#archcontroller). Should you wish to make use of a third-party credential-granting service for role providers granting deposit credentials for your markets, Wildcat will refer you to an appropriate entity and help ensure that you are configured in a way that enables you to make use of them.

After this point, Wildcat steps back.

## Lenders

If you're a party that wishes to lend to a particular borrower, Wildcat itself cannot onboard you.

Rather, the process is determined by the [policies](day-to-day-usage/market-access-via-policies-hooks.md) in place for a particular market, as these are what grant you a credential 'through' the market hook that gates deposit access.

It's hard to abstract the above into a 'this is how you onboard into market X' for this documentation, because one borrower may be content that you are not subject to a sanctions designation, another require you to reach out to the borrower and get explicitly whitelisted, another may require you to pass a third-party KYC/B check to verify your jurisdiction and that you're accredited (or whatever other requirement the borrower has), and another still may be content to accept a [Coinbase Verification](https://www.coinbase.com/en-gb/onchain-verify) or [Binance Account Bound Token](https://www.binance.com/en-GB/babt).&#x20;

Wildcat does not decide what a particular borrower should demand in terms of lender onboarding, as we consider this a compliance/legal issue for each borrower depending on their location, risk appetite and purpose. However, the protocol UI provides contact points for borrowers (i.e. email, Telegram), and each market will also indicate the requirements that are in place for obtaining deposit credentials.

In most cases, we envisage that you will be able to receive a deposit credential for a market without ever reaching out to a borrower directly, although that option is of course available to you.

Credentials may not last forever depending on borrower configuration, and may require periodic refreshing if you wish to deposit again in the future.

However, in Wildcat V2, addresses that have previously deposited assets or received market tokens (the debt of a market) while holding a valid deposit credential are _always_ be able to make withdrawal requests, even if their deposit credential has expired. For this reason, we encourage that you make use of a hardware wallet or a multisig when engaging with Wildcat.

There's some more detail on this available [here](day-to-day-usage/market-access-via-policies-hooks.md), and we will provide a clearer walkthrough once live.

Note that addresses which are flagged as sanctioned by the [Chainalysis oracle contract](https://go.chainalysis.com/chainalysis-oracle-docs.html) are prevented from interacting with the protocol at the code-level - although it's a _brave_ entity that tries either asking for or seeking to extend credit from any of these.&#x20;
