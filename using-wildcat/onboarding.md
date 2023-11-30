---
description: How to make use of the Wildcat protocol.
---

# Onboarding

The Wildcat protocol is fundamentally permissioned in both roles that it is possible to fill while using it. The primary difference is that it is the Wildcat protocol itself that  grants permission to borrower candidates to deploy markets, whereas borrowers are the ones that themselves grant permission to their selected lenders to interact with the markets that they deploy.

## Borrowers

Borrowers who wish to make use of Wildcat are encouraged - on the UI landing page and the protocol site itself - to get in touch via this [**Typeform**](https://rvficirw76q.typeform.com/to/FKBzhnmo)**.**

After first contact, what we're looking for is proof that the borrower is a legal entity in a jurisdiction that is a) not sanctioned, and b) we reasonably believe won't expose the protocol to legal risk (sorry, Americans).

We aren't interested in receiving a live feed of your financial data, but we'll be asking what you intend to utilise Wildcat for, checking that you're a going concern, who your ultimate beneficiaries are and so on. We can't dictate the terms of a market that a borrower deploys once they're onboarded, but we'll be emphasising expected behaviour to you by double checking you've actually read the Service Agreement.

We'll ask what process you intend to follow to check that lenders are who they say they are if you're utilising a market that requires explicit whitelisting of addresses, and ask you to agree to periodic check-ins on how funds are being used (plus getting feedback from you on what else you'd like to see!).

We may well be running your documents past our lawyers and a third-party assessment service to check their veracity - we'll let you know if that's the case. Truth be told, our lawyers are probably going to tell us to firm this entire process up a lot more, but while we're in the launch stages, we can summarise this as - play ball with us and be honest.

If all is well, we'll be asking you for an address, which will subsequently be added as a borrower capable of deploying controllers and markets to the [**archcontroller**](terminology.md#archcontroller).

## Lenders

If you're a party that wishes to fulfil the role of a lender, Wildcat itself cannot onboard you - this must be done by an active borrower via a controller that they deployed.

On the protocol UI, we intend to provide contact points for such borrowers (i.e. email, Telegram), however the protocol does not play any further role in this process.

In terms of any KYC/AML policy that must be followed in order for a lender to be onboarded, Wildcat defers this entirely to the borrowers themselves - we'll have asked them what they intend their process to be when onboarding them, but we won't have any way to verify this. If it turns out they've told us one thing and are doing another, though, we'll be offboarding them - this means that while their current markets will remain untouched, they cannot deploy new ones.

Note that addresses which are flagged as sanctioned by the Chainalysis oracle contract are prevented from interacting in any way with the protocol - although it's a _brave_ entity that tries asking for credit from one of these.
