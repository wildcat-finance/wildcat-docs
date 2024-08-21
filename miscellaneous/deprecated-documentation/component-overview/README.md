# Component Overview

**NOTE \[16 October]: Hey, if you're here from Code4rena, we haven't really got this part of the Gitbook fully specified yet because we only recently finalised everything for the code freeze. We're working on providing a little explainer for each variable and function, but if it's not present yet and you can't work it out from looking at source, ping us via C4 Discord and we'll respond/update when we can!**

The Wildcat Protocol consists of several components:

* The [**Archcontroller**](wildcatarchcontroller.sol.md) is responsible for authorising borrowers to deploy controllers and markets, as well as maintaining a list of all protocol associated contracts.
* A [**Controller Factory**](wildcatmarketcontrollerfactory.sol.md) deploys new controllers.
* A [**Controller**](wildcatmarketcontroller.sol.md) may interface with markets, adjust parameters, and set authorisation rules.
* A [**Market**](wildcat-market-overview/) is responsible for the borrowing and lending within the protocol.
* The [**Sanctions Sentinel**](wildcatsanctionssentinel.sol.md) is responsible for deploying escrow contracts to remove lenders that are flagged by the Chainalysis oracle from markets.
* A [**Sanctions Escrow**](wildcatsanctionsescrow.sol.md) holds the assets of a lender flagged by the sentinel.
* Protocol-wide [**structs**](structs/) are listed here.

Each hyperlink in the above will direct you to a list of the various _public or external_ functions, variables and structs contained therein.

Little explainers coming (the market components have them already), but you're all bright - you can work it out. ;)
