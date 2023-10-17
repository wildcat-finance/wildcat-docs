---
description: What's the worst that could happen?
---

# The Sentinel

We do not expect this to happen to any users of the protocol, but we have accounted for the potential that a lender address is added to a national sanctions list such as the OFAC SDN in a repeat of the Tornado Cash incident of August 2022.

The strict liability nature of transfers to and from addresses that have been tagged in such a manner means that we need to account for the potential for them to poison a entire market.

Here's how we've handled it:

### Lender Gets Sanctioned

In the event that a lender address is sanctioned, the sentinel contract can deploy an escrow contract between the borrower of a market and the lender in question.

Within each market contract itself, a `nukeFromOrbit` function exists that creates an escrow contract, transfers the market balance corresponding to the lender from the market to the escrow, erases the lenders market token balance, and blocks them from any further interaction with the market itself.

The underlying assets can be retrieved by the lender from the escrow contract via the `releaseEscrow` function in one of two cases:

* The lender address is no longer flagged as being sanctioned by the Chainalysis oracle, or
* The borrower involved in that particular escrow contract specifically overrides the sanction status via the `overrideSanction` function.

Note that this power cannot be randomly used to erase lenders from markets: the Chainalysis oracle **must** return `true` when asked if the lender address is sanctioned in order for the escrow contract to be created.

We do not believe that Wildcat protocol users are at risk of a simultaneous exploit of the Chainalysis oracle and excision from a market as a result - in fact we do not _expect_ `nukeFromOrbit` to ever actually be _called_ - but better to be prepared.

### Borrower Gets Sanctioned

In the event that the _borrower_ of a market is added to the Chainalysis oracle, any markets that they have deployed are immediately considered irreparably poisoned: _all_ lenders will be affected by strict liability if they withdraw assets after the borrower deposits any back to the market after this point.

If this happens, the archcontroller is likely to sever the market - this means that while it will still operate normally, it will no longer show up on the UI (which queries the archcontroller for a list of which markets to display), and escrow contracts cannot be created for it.

You're going to want to speak to a lawyer in your jurisdiction if you're a lender to a market where this happens.
