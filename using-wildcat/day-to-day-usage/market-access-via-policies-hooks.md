# Market Access Via Policies/Hooks

When you first encounter a Wildcat market, you will very likely be prevented from depositing unless you meet certain requirements specified by the borrower, to make sure that they're not making use of funds sourced from Lazarus.

The way that this worked in Wildcat V1 was that the borrower had to perform due diligence on each would-be lender that approached them and subsequently add their address to a controller contract via an on-chain transaction. This was a huge friction point, and one of the primary reasons we built V2.

Wildcat V2 abstracts this away by putting the `deposit` function behind a 'hook' (a piece of code that needs to succeed before access to the function is granted). We've built this in a way that borrowers can select arbitrary mechanisms tailored to their preferences, but the most common examples we expect to see are:

* Addresses that are members of a pre-determined set,
* Addresses that have some form of NFT or soulbound token testifying to their identity, and
* Addresses that have a credential testifying to off-chain circumstances.

The first example is effectively the V1 model, but we didn't want to throw it in the bin: we just also didn't want it to be the _only_ way that people could access Wildcat. We plan to evolve this slightly, however: if a borrower is an entity that has a significant number of OTC counterparties, Wildcat can deploy a market which is accessed by providing proof that your address is in the Merkle tree of that set (ensuring that addresses of counterparties aren't exposed).

The second example accounts for on-chain solutions such as [Coinbase Verifications](https://www.coinbase.com/en-gb/onchain-verify) and [Binance Account Bound Tokens](https://www.binance.com/en-GB/babt), assuming that the borrower is comfortable piggybacking off of these. In this case, access credentials are granted by signing a transaction that verifies that your address is in fact in possession of whatever is being sought out (i.e. an NFT in your wallet with a certain timestamp).

The third example is one that extends off-chain. We make use of [Keyring Network](https://keyring.network) to enable borrowers to specify rule-sets that they require lenders to adhere to. Depending on whether a Keyring Pro or Keyring Connect policy is used, lenders may be required to upload KYC/KYB data to a third-party platform such as ComplyCube or ShuftiPro to establish jurisdiction, extract evidence of accredited investor status and so on. Keyring enables proofs of such compliance to be submitted on-chain to receive Wildcat credentials without leaking any identifiable data on-chain.

There is substantially more detail on the flexibility offered here in the [Keyring docs](https://docs.keyring.network/docs/end-users/how-to-onboard/kyc-onboarding).

For borrowers making use of Keyring Pro policies to gate access, they must create a profile on Keyring and either clone a template Wildcat policy that we provide, or construct their own: in either event, the borrower must own the policy that they are making use of. Wildcat covers the costs. For lenders, you will need to create a Keyring profile and potentially install an extension that witnesses data you receive via HTTPS and constructs proofs of its validity.

We'll be able to illustrate this in far more detail once we have some live policies and markets available, but the TL;DR is: in most cases, we expect you to be able to onboard yourself to Wildcat markets without ever having to reach out to a borrower via Telegram or email!

## Credential Durations

When you have acquired a credential granting you access to deposit into a Wildcat market, it's worth noting that it may eventually expire, depending on whether or not the borrower has set a 'Time-To-Live' limit on it. This is to reduce the risk of an address being compromised and funds being deposited from an entity that is not the party which initially received the credential (unlikely as this may be). Credentials can be refreshed, assuming that the provider/mechanism is still registered to the market.

Note also that any address that has historically received a credential and deposited permanently retains the ability to withdraw: it is for this reason that we encourage lenders to make use of hardware wallets or multisigs when depositing.
