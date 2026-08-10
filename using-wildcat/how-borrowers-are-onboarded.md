---
description: How borrowers move from first contact with Wildcat Labs through Foundation-managed KYB and registration, then deploy markets and maintain their profiles.
---

# How borrowers are onboarded

## The borrower onboarding process

Every borrower on Wildcat is a real, registered legal entity. Before it can deploy a market, the borrower must pass an automated Sumsub KYB check covering legal existence, ownership, control and AML/sanctions screening, then have its Ethereum address written on-chain by the Wildcat Foundation. This page explains the process, what you will be asked for, and which parts of a borrower profile have actually been checked.

Two points to get out of the way first, because they bear repeating:

* **Neither Wildcat Labs nor the Wildcat Foundation underwrites any borrower.** KYB establishes who a borrower is: that the entity exists, who owns it, and who controls it. It is not an assessment of creditworthiness or repayment capacity. Neither entity insures against defaults. As a lender, you bear the counterparty risk.
* **Only part of a profile is checked.** The legal-identity fields come out of the Foundation's KYB process. The marketing copy, links and pitch come from the borrower; neither Wildcat Labs nor the Foundation verifies or monitors them. If you think a borrower is misrepresenting itself, contact the Foundation at <contact@thewildcat.foundation>.

### The process at a glance

| Step             | Who runs it                                               | What happens                                                                |
| ---------------- | --------------------------------------------------------- | --------------------------------------------------------------------------- |
| 1. First contact | You + Wildcat Labs                                        | You contact Wildcat Labs directly or through an outreach form               |
| 2. Intro call    | Wildcat Labs                                              | Labs explains Wildcat; you explain what you do                              |
| 3. Handover      | Wildcat Labs + Wildcat Foundation                         | Labs introduces you to the Foundation, which takes over onboarding          |
| 4. KYB check     | Wildcat Foundation + its compliance provider using Sumsub | You complete a Sumsub KYB check through the Foundation's compliance process |
| 5. Registration  | Wildcat Foundation                                        | The Foundation writes your Ethereum address to the archcontroller           |
| 6. Deployment    | You                                                       | You deploy whatever markets you like                                        |
| 7. Profile       | You                                                       | You supply your profile details and market descriptions                     |

### Step 1: You get in touch

There are two doors in. You can contact Wildcat Labs directly or use one of the outreach forms on the Wildcat websites. Either is fine.

Wildcat Labs asks for no documents or identity data at this stage. This is only the first contact.

### Step 2: The intro call

Before the compliance machinery starts turning, Wildcat Labs will usually arrange a call with you. It covers two things:

* **What Wildcat actually is.** Labs explains the undercollateralised, non-custodial lending protocol: you set the terms of your markets, and neither Wildcat Labs nor the Wildcat Foundation intermediates or underwrites the loan.
* **What you actually do.** Your business, what you want to borrow, and what you'd use the markets for.

The call creates no commitment for you or Wildcat Labs.

### Step 3: Handover to compliance

Once there is genuine interest on both sides, Wildcat Labs hands you over to the Wildcat Foundation. From there, the Foundation runs onboarding and compliance through its compliance service provider. The handover goes out by email and introduces you to the operations team running the process. It also tells you what is coming: a Sumsub KYB link, registration of your address on-chain by the Foundation once the check clears, and a heads-up about which details will be made public.

### Step 4: The KYB check (via Sumsub)

The Foundation's compliance service provider sends you a secure link and conducts the KYB check using Sumsub, a specialist verification platform. This automated corporate due diligence covers borrower-submitted material: legal existence, ownership and control structure, the identity of directors and shareholders with 10% or more of the entity, document authenticity, and selected automated AML and sanctions screening.&#x20;

#### What you will be asked for

Where you genuinely cannot provide one of these items because of your jurisdiction or entity type, the Foundation's compliance provider will accept an equivalent document. Do not panic if the wording does not quite match your filing cabinet.

* **Proof of legal existence:** documentation such as a certificate of incorporation or registration.
* **Company structure:** the whole corporate picture, subsidiaries and parent companies included. Org charts are not required, although some entities do provide one.
* **Registry of directors:** a full list, with proof of identity and proof of address for each individual. The KYC policy only requires obtaining KYC for a minimum of two directors where there are more than two on the register, in line with CIMA's AML Regulations.
* **Registry of shareholders:** the list, with proof of identity, proof of address and selfie verification for anyone holding 10% or more.
* **Intended use case:** a short blurb on what you plan to use your Wildcat markets for. The Foundation keeps this in an internal compliance log rather than publishing it, so you can be plain about it.
* **Corporate identity details:** legal name, registration number, jurisdiction of incorporation, registered office address, and a notice email. These feed the legal agreements later.
* **Blockchain address:** an Ethereum mainnet deployment address. Smart-contract and MPC wallets are fine here (Safe, Fireblocks, Fordefi, and so on). Use a multisig or MPC setup rather than a single-key EOA: this address controls your markets and your borrowing capacity.

#### How the check works

The process follows Sumsub's Full KYB methodology: automated checks, cross-referencing against corporate registries, and actual humans reading the documents. Between them, they establish:

* **That the entity legally exists, and its details.** Sumsub pulls the name, registration number, legal form, address and incorporation date from your documents, then cross-checks them against government corporate registries and independent databases where available.
* **Who owns and controls it.** The documents and registries establish the directors, shareholders and Ultimate Beneficial Owners; the individuals in those roles then complete a KYC identity check.
* **That the documents aren't forged.** Sumsub scans every document for tampering and graphic-editor trickery, then a human checks for internal inconsistencies, odd deviations from standard templates, and missing data.
* **That nobody's on a list they shouldn't be.** Sumsub screens the entity and its associated parties against automated sanctions lists, PEP lists and watchlists. The process does not include automated on-chain AML analytics.

{% hint style="info" %} One honest caveat on registry data: coverage and depth vary by jurisdiction. Where a registry exists and can be queried, Sumsub pulls and cross-checks company data directly from it; where a registry is thin, holds limited detail, or doesn't expose ownership information at all, the submitted corporate documents and manual review carry more of the weight and certified copies are often requested. Registry data alone rarely reveals the full ownership picture, which is exactly why the document package above is requested alongside it. {% endhint %}

For a full description of the methodology, see Sumsub's own documentation: [How Business Verification works](https://docs.sumsub.com/docs/business-verification).

A passed profile leaves the Foundation with the applicant record and status, completed verification checklist, documents on file, mapped-out company structure, registry-verified company data, individual checks (email, IP, corporate registry), and automated AML/sanctions screening results. That is the paper trail behind every verified borrower.

The KYB check is a point-in-time verification performed during the Foundation's onboarding process. The Foundation does not regularly re-run the check or continuously monitor a borrower's corporate status afterwards.

#### How long it takes

It depends entirely on the complexity of your structure and how quickly you send the documents over. A clean single-entity structure clears fast. A Russian-doll ownership chain, where the intermediate holding companies must be checked as well, takes longer, because of course it does. The Foundation and its compliance provider do not quote a fixed turnaround before seeing the structure; you will get a realistic estimate for your specific case once they have.

### Step 5: You get written on-chain

Once the KYB check passes, the Wildcat Foundation asks for the Ethereum mainnet address you want to use and registers it on the archcontroller, the registry and permission gate that decides who may deploy hooks and markets. Before the Foundation registers your address, you cannot create markets. Afterwards, you have free rein to deploy whatever you like from it.

{% hint style="info" %} If you also want to deploy on Plasma, tell the Foundation during onboarding so that it can register your address there as well. {% endhint %}

### Step 6: You deploy markets

With your address registered, you sign the Terms of Use (if you haven't already), flip the app over to the Borrower side, and start deploying. Every knob is yours to set:

* Underlying asset and the market token name
* Base APR, capacity, and reserve ratio
* Grace period, penalty APR, and withdrawal cycle duration
* Access policy: lenders self-onboard, or you operate an allowlist
* Whether the market carries a Master Loan Agreement

Wildcat Labs has documentation for each of these choices and is around to talk you through the how. Neither Labs nor the Foundation will pick your parameters or find lenders for you; those bits are yours.

{% hint style="warning" %} **On the MLA:** If you select the Wildcat template, you pre-sign it at market creation and lenders countersign before depositing. If you decline it, the app still requires a signature to record that choice. MLAs cannot be added retroactively, and lenders may reasonably ask why you did not offer one. {% endhint %}

### Step 7: You own your profile

After registration, your public profile is yours to maintain. You can edit the description, contact methods, socials and market descriptions directly from your registered borrower address whenever you like. The same goes for your alias or trading name: it appears exactly as you supply it, unverified. Your legal identity is different; changing that requires a fresh KYB check through the Foundation, for reasons that should be obvious.

### What's public, and what has actually been checked

Lenders: this is your bit. A borrower profile puts two kinds of information next to each other, and only the legal-identity side has been checked through the Foundation's onboarding process. Read with that in mind.

#### Checked through the Foundation's KYB process

These facts about the legal entity come straight out of the Sumsub check:

* Legal name
* Borrower Ethereum address
* Headquarters (the registered office established during KYB)
* Entity legal form
* Founded (year)

#### Not checked (borrower-supplied)

The borrower supplies these fields. Neither Wildcat Labs nor the Foundation claims that they are accurate or endorses any link you follow from them:

* Alias / trading name
* Profile description
* Outgoing links (contact details, social channels)
* Market descriptions

Treat these as leads for your own diligence, not as facts: check a trading name against the verified legal name, verify links independently before trusting them, and take questions about the business to the borrower directly through their listed contact methods.

#### What signing up makes public

By going through the KYB check, you accept that the following go onto your front-facing profile: year founded, legal name, jurisdiction, and legal nature of the entity.

The Foundation asks for your physical (registered office) address during onboarding for quasi-public use. That means it is not shown on the open profile by default; it pre-populates the on-chain Master Loan Agreement for any market where you offer one, so the lenders who countersign that agreement will see it. If you are not comfortable with that, the profile can instead show "Physical Address Withheld."

### Collections are not a Wildcat function

Once you deploy a market, the borrower-lender relationship belongs to you and your lenders. Neither Wildcat Labs nor the Wildcat Foundation is a lender, intermediary, agent, advisor, servicer, custodian, collection agent, or enforcement party. Neither controls or manages markets, intermediates transactions through the Protocol, or takes responsibility for repayment, collection, enforcement, recovery, market performance, or the outcome of a borrower-lender dispute.

If a borrower defaults, any rights and remedies belong to the relevant lender or other non-defaulting party under the applicable market terms, Master Loan Agreement (if any), Terms of Use, applicable law, or equity. Neither Wildcat Labs nor the Foundation collects on behalf of lenders, directs lenders on whether or how to pursue claims, or participates in recovery, enforcement, liquidation, legal proceedings, or settlement activity.

Where appropriate, the Foundation may provide the limited borrower-identifying information reasonably necessary for a lender to evaluate and, if it chooses, pursue its own rights and remedies. It weighs each disclosure against applicable law, the Wildcat Terms of Use, the Wildcat Privacy Policy, and any applicable contractual restrictions. Sharing that information does not make Wildcat Labs or the Foundation responsible for the lender's decision, the borrower's repayment, or the outcome of any proceedings.

### The short version, by audience

**If you're a borrower:** it starts with a call with Wildcat Labs. Labs then hands you to the Wildcat Foundation, which runs the Sumsub KYB process through its compliance provider and registers your address on-chain once you pass. Your legal identity becomes public; your physical address can be withheld if you prefer.

**If you're a lender:** every borrower has passed the Foundation's KYB process as a verified legal entity, and that carries real weight. Treat the legal name, Ethereum address, headquarters, entity legal form and founding year as verified. Treat trading names, descriptions, links and market copy as borrower-supplied material to check for yourself. Verification confirms identity, not creditworthiness; neither Wildcat Labs nor the Foundation underwrites a single borrower or market.

### Anything else?

Direct KYB and onboarding questions to the Wildcat Foundation at <contact@thewildcat.foundation>. Direct product and deployment questions to Wildcat Labs.
