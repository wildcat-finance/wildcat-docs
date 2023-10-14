# Component Overview

**NOTE \[13 October]: Hey, if you're here from Code4rena, we haven't really got this part of the Gitbook fully specified yet because we only recently finalised everything for the code freeze. Should be standing up properly soon, but if there isn't an explainer for a function yet and you can't work it out from looking at source, ping us in the C4 Discord and we'll respond/update.**

It's worth re-emphasising here that we currently move interchangeably between _vaults_ and _markets_. They're referring to the same thing, but our apologies either way!

The Wildcat Protocol consists of several components:

* The [**Archcontroller**](wildcatarchcontroller.sol.md) is responsible for authorising borrowers to deploy controllers and markets, as well as maintaining a list of all protocol associated contracts.
* A [**Controller Factory**](wildcatvaultcontrollerfactory.sol.md) deploys new controllers.
* A [**Controller**](wildcatvaultcontroller.sol.md) may interface with markets, adjust parameters, and set authorisation rules.
* A [**Market**](wildcatmarket/) is responsible for the borrowing and lending within the protocol.
* The [**Sanctions Sentinel**](wildcatsanctionssentinel.sol.md) is responsible for deploying escrow contracts to remove lenders that are flagged by the Chainalysis oracle from markets.
* A [**Sanctions Escrow**](wildcatsanctionsescrow.sol.md) holds the assets of a lender flagged by the sentinel.

Each hyperlink in the above will direct you to a breakdown and explanation of the various _public or external_ functions, variables and structs contained therein.
