# SphereX Protection

The Wildcat protocol contracts are protected on-chain by [SphereX](https://www.spherex.xyz/).

Without going into too much detail here, all external functions are wrapped in a modifier which sanity-checks any given transaction against a training set, reverting said transaction if it deviates too far from expected behaviour.

The net effect of this is that transactions which constitute exploits (in that they take a novel path through function calls, interact strangely with contract storage, utilise an abnormal amount of gas and so on) are not permitted to execute, with a report of the transaction being sent to an analytics engine in order to determine the root cause of the rejection.

In the event that the transaction is legitimate (e.g. follows a path that had not been covered by training data), the Wildcat team are capable of updating the reference set to permit that transaction - and others like it - to succeed going forwards.&#x20;

The nature of this protection means that access to Wildcat markets - and the wider protocol - is continuous even while under attack: deposits and withdrawals are be permitted as usual, whereas hostile transactions are rejected.

In the event that SphereX ceases to exist, the on-chain nature of the protection means that we would only lose access to the off-chain analytics engine and ability to update the reference set. In the worst case scenario, this would require a redeployment of the core Wildcat contracts, followed by encouraging all protocol participants to close and redeploy their extant markets.

It is worth noting however, that as with all security measures, the existence of SphereX within the Wildcat codebase does not _guarantee_ total safety. In the event that Wildcat's team is compromised, it is possible to update the reference set with a hostile transaction after it has first been identified and subsequently replay the transaction.

Shortly after launch, we will be calling upon trusted figures to act as the signers of a multisig wallet capable of pushing updates to the reference set. The existence of this multisig is an attack vector for the reasons specified in the previous paragraph, and therefore you should be aware of it and our efforts to mitigate this.
