---
description: "How a borrower can pledge separate, liquidatable ERC-20 collateral to back a market."
---

# Optional Collateral Contracts

Wildcat allows for a borrower to deploy one or more smart contracts holding assets that can be liquidated and transferred in to a specific Wildcat market should capital calls (withdrawal requests) not be honoured in the appropriate time frame. The intention here is to offer lenders a mechanism by which they can underwrite a credit opportunity by referring to backing assets visible on-chain.

While the 'default' behaviour of Wildcat is that markets are under/uncollateralized depending on the [reserve ratio/CRR](../terminology.md#reserve-ratio) set on creation, making use of collateral contracts permits a market to be partially, fully or even _ove&#x72;_&#x63;ollateralised, in _any_ ERC20 asset provided that there is a path to convert them to the underlying (base) asset of a Wildcat market.

This is distinct from the concept of a borrower 'over-repaying' assets to a market itself (i.e. transferring 1,000 USDC to a market where they only have 900 USDC in outstanding debt) - collateral contracts are defined in assets that are _different_ to the asset being borrowed, such as depositing Wrapped Ether (WETH) as a pledge against a USDC credit line.

In the current version of collateral contracts, the assets pledged within a collateral contract are not deployed further to, for example, yield farm: rather, they sit 'in stasis' until the earlier of:\
\
a) the market being terminated (all outstanding debt is repaid), whereupon the borrower can withdraw the assets from the collateral contract, or\
\
b) the market enters penalised delinquency, whereupon the appropriate amount can be liquidated by an approved executor address into the underlying asset of the market and repaid.

#### Using Collateral Contracts As A Borrower

<figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

#### Technical Details

