---
description: Worry not, help has arrived.
---

# FAQs

### I'm a lender trying to deposit into a market from a Fireblocks vault account, but my transactions are getting rejected?

This is very likely because your TAP (Transaction Authorization Policy) is set up to block interactions with DeFi protocols: the default mode is locked down quite heavily.

Add a new Contract Call TAP rule (you can find them in your Settings) with the Wildcat market you are attempting to interact with as the Destination which Allows the interaction, and move it up to the top of your rule-set, above any generic blocking rules.\
\
For an example of how to set up a rule: [https://support.fireblocks.io/hc/en-us/articles/7361651981468-TAP-examples](https://support.fireblocks.io/hc/en-us/articles/7361651981468-TAP-examples) (account required).

***

### I've placed a withdrawal request but I can't claim my assets yet?

This is because when you placed your withdrawal request, you either started a new withdrawal cycle or joined an existing one. That withdrawal cycle needs to conclude before any assets set aside within it can be claimed - the length of which is dependent on the market itself.

Check the Lender Withdrawal Requests tables within the market that you placed the withdrawal request from: you'll be able to see when the cycle ends and you can claim funds that have been made available for you from your request.

***



If you're encountering any difficulties, get in touch!

Two questions in the FAQ doesn't seem like much, but the point of an FAQ is to answer the questions we hear a lot!
