# Table of contents

* [The Wildcat Protocol](README.md)

## Overview

* [Introduction](overview/introduction.md)
* [What Wildcat Enables](overview/what-wildcat-enables.md)
* [Whitepaper](overview/whitepaper.md)
* [FAQs](overview/faqs.md)

## Using Wildcat

* [Terminology](using-wildcat/terminology.md)
* [Onboarding](using-wildcat/onboarding.md)
* [Day-To-Day Usage](using-wildcat/day-to-day-usage/README.md)
  * [Borrowers](using-wildcat/day-to-day-usage/borrowers.md)
  * [Lenders](using-wildcat/day-to-day-usage/lenders.md)
  * [Market Access Via Policies/Hooks](using-wildcat/day-to-day-usage/market-access-via-policies-hooks.md)
  * [The Sentinel](using-wildcat/day-to-day-usage/the-sentinel.md)
* [Protocol Usage Fees](using-wildcat/protocol-usage-fees.md)
* [Delinquency](using-wildcat/delinquency.md)

## Technical Overview

* [Security/Developer Dives](technical-overview/security-developer-dives/README.md)
  * [The Scale Factor](technical-overview/security-developer-dives/the-scale-factor.md)
  * [Core Behaviour](technical-overview/security-developer-dives/core-behaviour.md)
  * [V1 -> V2 Changelog](technical-overview/security-developer-dives/v1-greater-than-v2-changelog.md)
  * [Known Issues](technical-overview/security-developer-dives/known-issues.md)
  * [Hooks](technical-overview/security-developer-dives/hooks/README.md)
    * [How Hooks Work](technical-overview/security-developer-dives/hooks/how-hooks-work.md)
    * [Access Control Hooks](technical-overview/security-developer-dives/hooks/access-control-hooks.md)
    * [Fixed Term Loan Hooks](technical-overview/security-developer-dives/hooks/fixed-term-loan-hooks.md)
* [Function/Event Signatures](technical-overview/function-event-signatures/README.md)
  * [/access](technical-overview/function-event-signatures/access/README.md)
    * [AccessControlHooks.sol](technical-overview/function-event-signatures/access/accesscontrolhooks.sol.md)
    * [IRoleProvider.sol](technical-overview/function-event-signatures/access/iroleprovider.sol.md)
    * [MarketConstraintHooks.sol](technical-overview/function-event-signatures/access/marketconstrainthooks.sol.md)
  * [/interfaces](technical-overview/function-event-signatures/interfaces/README.md)
    * [IHooks.sol](technical-overview/function-event-signatures/interfaces/ihooks.sol.md)
    * [IMarketEventsAndErrors.sol](technical-overview/function-event-signatures/interfaces/imarketeventsanderrors.sol.md)
    * [IWildcatArchController.sol](technical-overview/function-event-signatures/interfaces/iwildcatarchcontroller.sol.md)
    * [IWildcatSanctionsEscrow.sol](technical-overview/function-event-signatures/interfaces/iwildcatsanctionsescrow.sol.md)
    * [IWildcatSanctionsSentinel.sol](technical-overview/function-event-signatures/interfaces/iwildcatsanctionssentinel.sol.md)
  * [/market](technical-overview/function-event-signatures/market/README.md)
    * [WildcatMarketConfig.sol](technical-overview/function-event-signatures/market/wildcatmarketconfig.sol.md)
    * [WildcatMarketToken.sol](technical-overview/function-event-signatures/market/wildcatmarkettoken.sol.md)
    * [WildcatMarketWithdrawals.sol](technical-overview/function-event-signatures/market/wildcatmarketwithdrawals.sol.md)
    * [WildcatMarketBase.sol](technical-overview/function-event-signatures/market/wildcatmarketbase.sol.md)
  * [/spherex](technical-overview/function-event-signatures/spherex/README.md)
    * [ISphereXEngine.sol](technical-overview/function-event-signatures/spherex/ispherexengine.sol.md)
    * [ISphereXProtectedRegisteredBase.sol](technical-overview/function-event-signatures/spherex/ispherexprotectedregisteredbase.sol.md)
    * [SphereXConfig.sol](technical-overview/function-event-signatures/spherex/spherexconfig.sol.md)
  * [HooksFactory.sol](technical-overview/function-event-signatures/hooksfactory.sol.md)
  * [IHooksFactory.sol](technical-overview/function-event-signatures/ihooksfactory.sol.md)
  * [WildcatArchController.sol](technical-overview/function-event-signatures/wildcatarchcontroller.sol.md)
  * [WildcatSanctionsEscrow.sol](technical-overview/function-event-signatures/wildcatsanctionsescrow.sol.md)
  * [WildcatSanctionsSentinel.sol](technical-overview/function-event-signatures/wildcatsanctionssentinel.sol.md)
* [Protocol Structs](technical-overview/protocol-structs.md)
* [Contract Deployments](technical-overview/contract-deployments.md)

## Security Measures

* [Code Security Reviews](security-measures/code-security-reviews.md)
* [SphereX Protection](security-measures/spherex-protection.md)
* [Bug Bounty Program](security-measures/bug-bounty-program.md)

## Legal

* [Wildcat Terms Of Use](legal/wildcat-terms-of-use.md)
* [Risk Disclosure Statement](legal/risk-disclosure-statement.md)
* [Template MLA](legal/master-loan-agreement.md)
* [Privacy Policy](legal/protocol-ui-privacy-policy.md)

## Miscellaneous

* [Protocol History/Development](miscellaneous/who-we-are.md)
* [Contact Us](miscellaneous/contact-us.md)
* [DEPRECATED DOCUMENTATION](miscellaneous/deprecated-documentation/README.md)
  * [V1 Component Overview](miscellaneous/deprecated-documentation/component-overview/README.md)
    * [WildcatArchController.sol](miscellaneous/deprecated-documentation/component-overview/wildcatarchcontroller.sol.md)
    * [WildcatMarketControllerFactory.sol](miscellaneous/deprecated-documentation/component-overview/wildcatmarketcontrollerfactory.sol.md)
    * [WildcatMarketController.sol](miscellaneous/deprecated-documentation/component-overview/wildcatmarketcontroller.sol.md)
    * [Wildcat Market Overview](miscellaneous/deprecated-documentation/component-overview/wildcat-market-overview/README.md)
      * [WildcatMarket.sol](miscellaneous/deprecated-documentation/component-overview/wildcat-market-overview/wildcatmarket.sol.md)
      * [WildcatMarketBase.sol](miscellaneous/deprecated-documentation/component-overview/wildcat-market-overview/wildcatmarketbase.sol.md)
      * [WildcatMarketConfig.sol](miscellaneous/deprecated-documentation/component-overview/wildcat-market-overview/wildcatmarketconfig.sol.md)
      * [WildcatMarketToken.sol](miscellaneous/deprecated-documentation/component-overview/wildcat-market-overview/wildcatmarkettoken.sol.md)
      * [WildcatMarketWithdrawals.sol](miscellaneous/deprecated-documentation/component-overview/wildcat-market-overview/wildcatmarketwithdrawals.sol.md)
      * [Events](miscellaneous/deprecated-documentation/component-overview/wildcat-market-overview/events.md)
    * [WildcatSanctionsSentinel.sol](miscellaneous/deprecated-documentation/component-overview/wildcatsanctionssentinel.sol.md)
    * [WildcatSanctionsEscrow.sol](miscellaneous/deprecated-documentation/component-overview/wildcatsanctionsescrow.sol.md)
    * [Structs](miscellaneous/deprecated-documentation/component-overview/structs/README.md)
      * [Some Notes On Normalized versus Scaled Amounts](miscellaneous/deprecated-documentation/component-overview/structs/some-notes-on-normalized-versus-scaled-amounts.md)
  * [Protocol Gas Profile](miscellaneous/deprecated-documentation/protocol-gas-profile.md)
