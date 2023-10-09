# Component Overview

The Wildcat Protocol consists of several components:

**NOTE \[9 OCTOBER 2023]: Following a major refactor of controllers, this section is still WIP. Go read the rest of the Gitbook, we'll be back up and running here soon.**

* The Archcontroller is responsible for authorising borrowers to deploy controllers and markets, as well as maintaining a list of all protocol associated contracts.
* A Controller Factory deploys new controllers
* A Controller may interface with markets, adjust parameters, and set authorisation rules.
* A Market is responsible for the borrowing and lending within the protocol.
* The Sanctions Sentinel is responsible for deploying escrow contracts to remove lenders that are flagged by the Chainalysis oracle from markets.
* A Sanctions Escrow holds the assets of a lender flagged by the sentinel.
