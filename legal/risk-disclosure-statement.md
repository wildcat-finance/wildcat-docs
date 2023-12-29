# Risk Disclosure Statement

This RDS describes those risks which are present within the Wildcat Protocol, both from a technical standpoint and within the context of its usage.

The contents of this RDS are acknowledged and accepted by all parties that have signed the Service Agreement. This RDS may periodically be updated, and it is the responsibility of protocol users to ensure that they are aware of - and accept - the latest version of this document. Users that do not accept are requested to cease usage of the protocol at their earliest convenience.

_Last update: 29 December 2023_

***

### Smart Contract Risks

As is the case with any smart-contract powered protocol, there are risks involved when placing assets within Wildcat markets involving unauthorised access or manipulation of contract functions and/or state contrary to intent.

We have followed best security practices as they apply to development of protocol contracts, but there is always the chance, _however slim_, that internal reviews, external audits, integrated security solutions and the presence of a bug bounty program still give rise to an attack vector we haven't accounted for.

#### Unauthorised Access

The Wildcat Protocol is currently permissioned, with addresses belonging to borrowers being explicitly granted the ability to deploy markets and addresses belonging lenders being given access to interact with them. Market tokens are intended to only be issued to and redeemed by lenders which have been given this authorisation.

There is a risk that malicious third-parties could gain access to one of these roles (either by taking control of an already authorised address or by somehow granting themselves this power), which may put markets and the balances/assets they track at risk of theft.

#### Rounding Errors

Wildcat contracts occasionally utilise rounding when dividing large numbers. Given the way in which Wildcat works, any loss in precision that results from this should not have any impact on protocol operations, relating mostly to growth of the scale factor to determine interest due.

There is a risk that this rounding might be exploitable in some manner to interfere with the way that interest is calculated, manifesting as the ability to dramatically scale market token balances and allowing a lender (or potentially a third party) to make a claim on far more underlying assets than should be due.

#### SphereX Transaction Rejection

It may be the case that your transaction follows a path that was not encountered during the SphereX training stage. The SphereX engine may subsequently reject your transaction as a false positive attack as a result. If this happens, the Wildcat team will investigate and determine whether or not to update the reference set with that particular transaction pattern in order to permit it going forward, whereupon it can be successfully resubmitted.

***

### Product Risks

**Counterparty/Default Risk**

Fundamentally, Wildcat involves undercollateralised lending, and this comes with risk of the borrower defaulting. Parties to a market are expected to have performed their desired level of due diligence and research on their counterparties in order to determine creditworthiness: the standards of which we do not impose externally. In the event of a default, there may be substantial or total loss of assets for individual lenders, depending on the reserve ratio of a given market and withdrawal queue ordering.



**Malicious Parameter Adjustment**

The ability to adjust the base lender APR and capacity of a market is one that can only be invoked by the deployer of that market - the borrower. Regardless of any off-chain agreement that may be in place, the borrower has the power to change these at will, and while there are some lender-oriented safeguards in place (such as potentially requiring a temporarily increased reserve ratio when reducing the APR), Wildcat itself cannot prevent or revert such adjustments.



***

### Administrative Risks

**Upgrade Powers**

The Wildcat protocol is designed such that existing markets cannot be shut down or altered in any way by the team, even in the event of an emergency.&#x20;



