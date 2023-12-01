# Risk Disclosure Statement

This RDS describes those risks which are present within the Wildcat Protocol, both from a technical standpoint and within the context of its usage.

The contents of this RDS are acknowledged and accepted by all parties that have signed the Service Agreement. This RDS may periodically be updated, and it is the responsibility of protocol users to ensure that they are aware of - and accept - the latest version of this document.

_Last update: 30 November 2023_

***

### Contract Risks

As is the case with any smart-contract powered protocol, there are risks involved when placing assets within Wildcat markets involving unauthorised access or manipulation of contract functions and/or state contrary to intent.

We have followed best security practices as they apply to development of protocol contracts, but there is always the chance, _however slim_, that internal reviews, external audits, integrated security solutions and the presence of a bug bounty program still give rise to an attack vector we haven't accounted for.

#### Unauthorised Access

The Wildcat Protocol is currently permissioned, with addresses belonging to borrowers being explicitly granted the ability to deploy markets and addresses belonging lenders being given access to interact with them. Market tokens are intended to only be issued to and redeemed by lenders which have been given this authorisation.

There is a risk that malicious third-parties could gain access to one of these roles (either by taking control of an already authorised address or by somehow granting themselves this power), which may put markets and the balances/assets they track at risk of theft.

#### Rounding Errors

Wildcat contracts occasionally utilise rounding when dividing large numbers. Given the way in which Wildcat works, any loss in precision that results from this should not have any impact on protocol operations, relating mostly to growth of the scale factor to determine interest due.

There is a risk that this rounding might be exploitable in some manner to interfere with the way that interest is calculated, manifesting as the ability to dramatically scale market token balances and allowing a lender (or potentially a third party) to make a claim on far more underlying assets than should be due.

#### SphereX Transaction Rejection

It may be the case that your legitimate transaction follows a path that was not encountered sufficiently many times during the SphereX training stage to be considered acceptable. The SphereX engine may subsequently reject your transaction as a false positive as a result. If this happens, the Wildcat team will investigate and determine whether or not to update the reference set with that particular transaction pattern in order to permit it going forward.

***

### Product Risks

TBA

