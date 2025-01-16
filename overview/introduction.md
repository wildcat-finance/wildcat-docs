# Introduction

## The Elevator Pitch <a href="#the-elevator-pitch" id="the-elevator-pitch"></a>

Wildcat is a protocol that allows borrowers to deploy massively configurable, unopinionated, hands-off un(der)collateralised on-chain credit rails.\
\
That's it.\
\
Wildcat borrowers can dictate the terms of almost any parameter that they would care to adjust when crafting their credit line:

* underlying asset,
* interest rate,
* maximum capacity,
* penalties,
* withdrawal cycle lengths, and so on.

Markets can also impose various access constraints that they may require:

* disabling withdrawals for a certain period (corresponding to a fixed-duration agreement),
* disabling transfers for the tokenised debt that Wildcat issues,
* enforcing minimum deposit amounts to prevent dust from accumulating,
* requiring lenders to prove compliance with a given profile before self-onboarding, etc.

Wildcat markets are not controlled or upgradable by the protocol itself once deployed.\
\
A market and its goings-on are between the borrowers and lenders alone. Wildcat does not custody _and_ cannot access - or force the movement of - any assets within markets.

**Wildcat** **does not underwrite any risk on any of the markets deployed through it.**

The Wildcat frontend provides an optional template loan agreement between borrower and lender on a per-market basis, but borrowers are free to decline to use this, and lenders are similarly free to decline to countersign.

Wildcat exists to create credit mechanisms _by you_, _for you_.

Your markets, your terms.

***

### ​A Comment Before You Head Further In <a href="#undefined" id="undefined"></a>

This documentation is currently undergoing revision as the protocol shifts towards the deployment of V2 and the deprecation of V1. There may be some inconsistencies, which we are seeking out.

There is some repetition of terms and definitions in various sections.

There is some repetition of terms and definitions in various sections.

There is some repetition of terms and definitions in various sections.

You aren't going insane: this is intentional, as we don't want (or expect) people to have to read through the entire site in order to understand the section that they're interested in.

After the V2 launch, we will be fleshing various pages out more screenshots, illustrations, videos and so forth to help explain more concepts more clearly - waves of text can be difficult to parse, and we're walking a tightrope between explaining the protocol to would-be users and also acting as a source of truth for security researchers and developers who would make use of or extend our code.

Please forgive any arcane ramblings: if there's anything you'd like to see expanded upon or clarified further, we'd consider it a favour if you got in touch with us.

​​
