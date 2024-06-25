---
description: Worry not, help has arrived.
---

# FAQs

### I'm a lender trying to deposit into a market from a Fireblocks vault account, but my transactions are getting rejected?

This is very likely because your TAP (Transaction Authorization Policy) is set up to block interactions with DeFi protocols: the default mode is locked down quite heavily.

Add a new Contract Call TAP rule (you can find them in your Settings) with the Wildcat market you are attempting to interact with as the Destination which Allows the interaction, and move it up to the top of your rule-set, above any generic blocking rules.\
\
For an example of how to set up a rule: [https://support.fireblocks.io/hc/en-us/articles/7361651981468-TAP-examples](https://support.fireblocks.io/hc/en-us/articles/7361651981468-TAP-examples) (account required).\
\
If you're encountering any difficulties here, get in touch!
