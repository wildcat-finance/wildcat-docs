---
description: "How to consume the Wildcat docs as an AI agent — Markdown endpoints, llms.txt, the ?ask API, and the Wildcat skill."
---

# For AI Agents & LLMs

This documentation is built to be machine-readable. If you're an AI agent — or building one — here's how to consume it efficiently.

## Markdown and indexes

* [**/llms.txt**](https://docs.wildcat.finance/llms.txt) — a curated, sectioned index of the entire documentation, with a short description of every page. Start here to navigate.
* [**/llms-full.txt**](https://docs.wildcat.finance/llms-full.txt) — the full text of the documentation concatenated into a single file, for wholesale ingestion.
* **Markdown for any page** — append `.md` to any page URL to get clean Markdown without site chrome (for example, [terminology.md](../using-wildcat/terminology.md)).

## Ask the docs a question

Any page can be queried in natural language by adding the `ask` parameter:

```
GET https://docs.wildcat.finance/using-wildcat/terminology.md?ask=How does a withdrawal cycle work?
```

The response contains a direct answer plus the relevant excerpts and sources.

## The Wildcat skill

For agents that need a single, self-contained briefing on the protocol — concepts and terminology, borrower and lender workflows, contract internals and addresses, and security/legal pointers — load the Wildcat skill (`SKILL.md`) maintained in the documentation repository under `skills/wildcat-protocol/`.

## Where to start

* New to Wildcat? Read [The Elevator Pitch](introduction.md), then [Terminology](../using-wildcat/terminology.md).
* Using the protocol? See [Borrowers](../using-wildcat/day-to-day-usage/borrowers.md) and [Lenders](../using-wildcat/day-to-day-usage/lenders.md).
* Auditing or integrating? See [Security/Developer Dives](../technical-overview/security-developer-dives/README.md) and [Contract Deployments](../technical-overview/contract-deployments.md).
