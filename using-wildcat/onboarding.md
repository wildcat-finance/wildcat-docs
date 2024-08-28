---
description: How to make use of the Wildcat protocol.
---

# Onboarding

The Wildcat protocol is fundamentally permissioned in both roles that it is possible to fill while using it. \
\
The operators of the Wildcat protocol grant permission to borrower candidates to deploy markets, whilst borrowers are the ones that determine which categories of lenders are able to interact with the markets that they deploy.

## Borrowers

Borrowers who wish to make use of Wildcat are encouraged - on the landing page and the protocol UI itself - to get in touch via this [**form**](https://forms.gle/irca7KeC7ASmkRh16).

After first contact, what Wildcat is looking for is proof that the borrower is a legal entity in a jurisdiction that is a) not sanctioned, and b) we reasonably believe won't expose the protocol to legal or regulatory risk. Discretion is currently being exercised in that we seek to reach 'up', meaning that we are more likely to accept recognised market makers, trading desks, protocols and such as borrowers. That's not to say that your smaller, less-recognised entity has a more significant probability of default

We be asking what you intend to utilise Wildcat for, checking that you're a going concern, who your ultimate beneficiaries are and so on. We may request that you engage with a third-party assessment service (such as SumSub) - we'll let you know if that's the case.

In short, this stage can be summarised as: play ball with us and be honest.

Following this, Wildcat requests an Ethereum address, which will be added as a borrower capable of deploying hooks instances and markets to the [**archcontroller**](terminology.md#archcontroller). Should you wish to make use of a third-party credential-granting service for your markets, Wildcat will refer you to the appropriate entity and ensure that relevant policies are cloned-and-owned by yourself so that you can make use of them.

After this point, Wildcat steps back.

## Lenders

If you're a party that wishes to lend to a particular borrower, Wildcat itself cannot onboard you.

Rather, the process is determined by the policies in place for a particular market, as these are what grant you a credential 'through' the market hook that gates deposit access.

It's hard to abstract the above into a 'this is how you onboard into market X' for this documentation, because one market may require you to reach out to the borrower and get explicitly whitelisted, another may require you to pass a third-party KYC check via [Keyring Network](https://keyring.network) to verify your jurisdiction and that you're accredited (or whatever other requirement the borrower has), and another still may be content to accept a [Coinbase Verification](https://www.coinbase.com/en-gb/onchain-verify) or [Binance Account Bound Token](https://www.binance.com/en-GB/babt).

Wildcat does not decide what a particular borrower should demand in terms of lender onboarding, as we consider this a compliance/legal issue for each borrower depending on their location, risk appetite and purpose. However, the protocol UI provides contact points for borrowers (i.e. email, Telegram), and each market will also indicate the requirements that are in place for onboarding.

In a smooth case, you will be able to briefly head off-site, give some information to a provider, submit an on-chain transaction with a ZK proof that proves you've met the requirements and receive an onboarding credential without ever reaching out to the borrower directly.&#x20;

Credentials may not last forever depending on borrower configuration, and may require periodic refreshing if you wish to deposit again in the future.

However, in Wildcat V2, addresses that have previously been authorised are always be able to make withdrawal requests, even if their credentials have expired. For this reason, we encourage that you make use of a hardware wallet or a multisig when engaging with Wildcat.

There's some more detail on this available [here](day-to-day-usage/borrowers/keyring-policies.md), and we will provide a clearer walkthrough once live.

Note that addresses which are flagged as sanctioned by the [Chainalysis oracle contract](https://go.chainalysis.com/chainalysis-oracle-docs.html) are prevented from interacting with the protocol at the code-level - although it's a _brave_ entity that tries either asking for or seeking to extend credit from any of these.&#x20;
