---
description: How to make use of the Wildcat protocol.
---

# Onboarding

Wildcat is a permissioned protocol where both borrowers and lenders must meet specific criteria to participate. The onboarding process and permissions differ for each role, as outlined below.

## Borrowers

Borrowers interested in using Wildcat are encouraged to contact the Wildcat Foundation through the [landing page](https://wildcat.finance) or by emailing [contact@thewildcat.foundation](mailto:contact@thewildcat.foundation).

#### Eligibility:

Currently, only registered legal entities are accepted as borrowers. In the future, individual retail borrowers may be allowed.

#### Verification Process:

The Wildcat Foundation performs a KYB/C verification similar to centralised exchanges. This includes verifying certificates of incumbency, proofs of address, and the identities of directors and individuals with significant control. After verification, borrowers provide an Ethereum address that is registered on-chain via the [**archcontroller**](terminology.md#archcontroller)**,** enabling them to deploy hooks instances and create markets.

#### Permissions:

Borrowers have the authority to determine which categories of lenders can interact with their markets.&#x20;

## Lenders

Wildcat does not directly onboard lenders; instead, each borrower sets their own criteria for lender participation.

#### Onboarding Process:

The process to obtain lending credentials varies depending on the borrower’s [policies](terminology.md#policy). Examples include:

* Confirming the lender is not subject to sanctions.
* Requiring explicit whitelist approval from the borrower.
* Verifying jurisdiction and accreditation through a third-party KYC/B check.
* Accepting credentials like [Coinbase Verification](https://www.coinbase.com/en-gb/onchain-verify) or [Binance Account Bound Tokens](https://www.binance.com/en-GB/babt) (with future hook integrations planned).

#### Access and Credentials:

* Lenders obtain deposit credentials through market hook instances, which act as gatekeepers.
* Credentials are typically issued without needing direct contact with the borrower, though that option remains available.
* Credentials may expire and need periodic renewal.
* Addresses that have previously deposited assets or received market tokens with a valid deposit credential can still make withdrawal requests even if the credential has expired.
* For security, lenders should use a hardware wallet or multisig when interacting with Wildcat.

#### Compliance and Restrictions

Wildcat does not dictate borrower requirements for lender onboarding. Each borrower is responsible for compliance based on their location, risk tolerance, and objectives.

Borrower profile pages on the protocol UI provide contact information (email, Telegram, Twitter), and each market displays its credential requirements.

Addresses flagged as sanctioned by the [Chainalysis oracle contract](https://go.chainalysis.com/chainalysis-oracle-docs.html) are automatically blocked from interacting with the protocol.&#x20;
