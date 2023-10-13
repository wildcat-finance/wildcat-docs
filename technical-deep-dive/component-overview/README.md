# Component Overview

**NOTE \[13 October]: Hey, if you're here from Code4rena, we haven't really got this specced out properly yet because we only recently finalised everything for the code freeze. Should be standing up properly soon.**



The Wildcat Protocol consists of several components:

* The [**Archcontroller**](wildcatarchcontroller.md) is responsible for authorising borrowers to deploy controllers and markets, as well as maintaining a list of all protocol associated contracts.
* A [**Controller Factory**](wildcatvaultcontrollerfactory.md) deploys new controllers.
* A [**Controller**](wildcatvaultcontroller.md) may interface with markets, adjust parameters, and set authorisation rules.
* A [**Market**](wildcatmarket/) is responsible for the borrowing and lending within the protocol.
* The [**Sanctions Sentinel**](wildcatsanctionssentinel.md) is responsible for deploying escrow contracts to remove lenders that are flagged by the Chainalysis oracle from markets.
* A [**Sanctions Escrow**](wildcatsanctionsescrow.md) holds the assets of a lender flagged by the sentinel.

Each hyperlink in the above will direct you to a breakdown and explanation of the various functions, variables and structs contained therein.
