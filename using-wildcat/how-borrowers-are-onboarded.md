# How borrowers are onboarded

## How Borrowers Are Onboarded

Every borrower on Wildcat is a real, registered legal entity that has passed an automated KYB check (legal existence, ownership, control, and AML/sanctions screening) using Sumsub and has had their Ethereum address written on-chain before they can deploy a single market. This page walks through how that happens, what we ask for, and which information on a borrower profile we have actually verified versus which is supplied by the borrower themselves.

Two points to get out of the way first, because we keep harping on about them and it bears repeating:

* **We do not underwrite anyone.** KYB establishes who a borrower is: that the entity exists, who owns it, and who controls it. It is not an assessment of creditworthiness or repayment capacity, and Wildcat does not insure against defaults. As a lender you shoulder the counterparty risk.
* **Only part of a profile is checked.** The legal-identity fields come out of KYB and are checked. The marketing copy, the links, the pitch: those are supplied by the borrower and are not verified or monitored. If you think a borrower is misrepresenting themselves you can reach out to <contact@thewildcat.foundation>.

### The Process at a Glance

| Step             | Who runs it                          | What happens                                                   |
| ---------------- | ------------------------------------ | -------------------------------------------------------------- |
| 1. First contact | You + Wildcat                        | You approach us directly, or through one of the outreach forms |
| 2. Intro call    | Wildcat                              | We explain what Wildcat is; you explain what you do            |
| 3. Handover      | Wildcat                              | We introduce you to our compliance service provider            |
| 4. KYB check     | Compliance service provider + Sumsub | You complete a Sumsub KYB check via a secure link              |
| 5. Registration  | Wildcat                              | Your Ethereum address is written to the archcontroller         |
| 6. Deployment    | You                                  | You deploy whatever markets you like                           |
| 7. Profile       | You                                  | You supply your profile details and market descriptions        |

### Step 1: You Get In Touch

There are two doors in. You either come to us directly, or you find us through one of the outreach forms on the Wildcat websites. Either is fine.

We ask for no documents and no identity data at this stage. This is just first contact.

### Step 2: The Intro Call

Before any compliance machinery starts turning, Wildcat will usually jump on a call with you. The call covers two topics:

* **What Wildcat actually is.** An undercollateralised, non-custodial lending protocol where you set the terms of your markets and we stay out of the way. We don't intermediate the loan and we don't underwrite it.
* **What you actually do.** Your business, what you want to borrow, and what you'd use the markets for.

The call carries no commitment on either side.

### Step 3: Handover to Compliance

Once there's genuine interest on both sides, we hand you over to our compliance service provider, who owns the onboarding process from here on. The handover goes out by email and introduces you to the operations team running it. That email also tells you what's coming: a Sumsub KYB link, on-chain registration of your address once the check clears, and a heads-up about which of your details will be made public.

### Step 4: The KYB Check (via Sumsub)

The compliance service provider sends you a link to complete the KYB check, which it conducts using Sumsub, a specialist verification platform. It is an automated corporate due diligence check of borrower-submitted material: legal existence, ownership and control structure, identity of directors and shareholders at 10% or more ownership of the entity, document authenticity, and selected automated AML and sanctions screening.&#x20;

#### What we'll ask you for

Where you genuinely can't provide one of these for reasons tied to your jurisdiction or entity type, an equivalent document is accepted in its place, so don't panic if the exact wording doesn't match your filing cabinet.

* **Proof of legal existence:** documentation such as a certificate of incorporation or registration.
* **Company structure:** the whole corporate picture, subsidiaries and parent companies included. Org charts are not a required document, although some entities do provide one.
* **Registry of directors:** a full list, with proof of identity and proof of address for each individual. The KYC policy only requires obtaining KYC for a minimum of two directors where there are more than two on the register, in line with CIMA's AML Regulations.
* **Registry of shareholders:** the list, with proof of identity, proof of address and selfie verification for anyone holding 10% or more.
* **Intended use case:** a short blurb on what you plan to use your Wildcat markets for. This one is kept as an internal compliance log, not published, so you can be plain about it.
* **Corporate identity details:** legal name, registration number, jurisdiction of incorporation, registered office address, and a notice email. These feed the legal agreements later.
* **Blockchain address:** an Ethereum mainnet deployment address. Smart-contract and MPC wallets are all fine here (Safe, Fireblocks, Fordefi, and so on). We strongly recommend a multisig or MPC setup over a single-key EOA: this address controls your markets and your borrowing capacity.

#### How the check verifies it

The check follows Sumsub's Full KYB methodology: a mix of automated checks, cross-referencing against corporate registries, and actual humans reading the documents. Between them, the process establishes and verifies:

* **That the entity legally exists, and its details.** Name, registration number, legal form, address, incorporation date: pulled from your documents and cross-checked against government corporate registries and independent databases where these are available.
* **Who owns and controls it.** Directors, shareholders, and Ultimate Beneficial Owners are established from the documents and registries, and the individuals in those roles complete a KYC identity check.
* **That the documents aren't forged.** Every document is scanned automatically for tampering and graphic-editor trickery, then eyeballed manually for internal inconsistencies, odd deviations from standard templates, and missing data.
* **That nobody's on a list they shouldn't be.** The entity and its associated parties are screened against automated sanctions lists, PEP lists and watchlists. No automated on-chain AML analytics are performed.

{% hint style="info" %} One honest caveat on registry data: coverage and depth vary by jurisdiction. Where a registry exists and can be queried, Sumsub pulls and cross-checks company data directly from it; where a registry is thin, holds limited detail, or doesn't expose ownership information at all, the submitted corporate documents and manual review carry more of the weight and certified copies are often requested. Registry data alone rarely reveals the full ownership picture, which is exactly why the document package above is requested alongside it. {% endhint %}

For a full description of the methodology, see Sumsub's own documentation: [How Business Verification works](https://docs.sumsub.com/docs/business-verification).

The upshot is that a passed profile carries the applicant record and status, the completed verification checklist, the documents on file, the mapped-out company structure, registry-verified company data, the individual checks (email, IP, corporate registry), and the automated AML/sanctions screening results. That's the paper trail sitting behind every verified borrower.

The KYB check is a point-in-time verification performed at onboarding. Wildcat does not re-run it regularly or continuously monitor a borrower's corporate status afterwards.

#### How long it takes

Depends entirely on how complicated you are and how quickly you send documents over. A clean single-entity structure clears fast. A Russian-doll ownership chain where the intermediate holding companies have to be verified too will take longer, because of course it will. We deliberately don't quote a fixed turnaround here; you'll get a realistic estimate for your specific case once your structure has been seen.

### Step 5: You Get Written On-Chain

Once the KYB check passes, we ask for the Ethereum mainnet address you want to use and register it on the archcontroller: the registry and permission gate that decides who is allowed to deploy hooks and markets. Before your address is on it, you can't create markets. After it, you have free rein to deploy whatever you like.

{% hint style="info" %} Also want to be on Plasma? Let us know during onboarding so your address can be registered there too, rather than discovering the gap later. {% endhint %}

### Step 6: You Deploy Markets

With your address registered, you sign the Terms of Use (if you haven't already), flip the app over to the Borrower side, and start deploying. Every knob is yours to set:

* Underlying asset and the market token name
* Base APR, capacity, and reserve ratio
* Grace period, penalty APR, and withdrawal cycle duration
* Access policy: lenders self-onboard, or you operate an allowlist
* Whether the market carries a Master Loan Agreement

We have solid documentation walking through every one of these choices, and we're around to talk you through the how whenever you want. What we won't do is pick the parameters for you or go find your lenders: those are yours.

{% hint style="warning" %} **On the MLA:** pick the Wildcat template and you pre-sign it at market creation, with lenders countersigning before they deposit. Decline it and we still make you sign, purely to log that you explicitly said no. MLAs can't be bolted on retroactively, and lenders may reasonably ask why you didn't offer one, so have an answer ready. {% endhint %}

### Step 7: You Own Your Profile

After registration your public profile is yours to maintain: your description, contact methods, socials and market descriptions can be edited directly from your registered borrower address, whenever you like. Your alias or trading name is likewise yours: it is displayed as you supply it, unverified. What cannot be changed by anyone except through a fresh KYB check is your legal identity, for reasons that should be obvious.

### What's Public, and What We've Actually Checked

Lenders: this is your section. A borrower profile shows two kinds of information sitting right next to each other, and only one of them has been checked by us. Read accordingly.

#### Checked by Wildcat (straight out of KYB)

These are facts about the legal entity, drawn from the Sumsub check:

* Legal name
* Borrower Ethereum address
* Headquarters (the registered office established during KYB)
* Entity legal form
* Founded (year)

#### Not checked by Wildcat (borrower-supplied)

These fields are supplied by the borrower. We make no claim they're accurate, and we don't endorse any link you click through to:

* Alias / trading name
* Profile description
* Outgoing links (contact details, social channels)
* Market descriptions

Treat these as leads for your own diligence, not as facts: check a trading name against the verified legal name, verify links independently before trusting them, and take questions about the business to the borrower directly through their listed contact methods.

#### What signing up makes public

By going through the KYB check, you accept that the following go onto your front-facing profile: year founded, legal name, jurisdiction, and legal nature of the entity.

Your physical (registered office) address is requested to be made quasi-public. Quasi-public means it isn't broadcast on the open profile by default; it's used to pre-populate the on-chain Master Loan Agreement for any market where you offer one, and is therefore visible to the lenders who countersign that agreement. If you're not comfortable with the address being displayed, the profile can instead show "Physical Address Withheld."

### Collections Are Not a Wildcat Function

Once you deploy a market, the borrower-lender relationship is yours. Wildcat is not a lender, intermediary, agent, advisor, servicer, custodian, collection agent, or enforcement party. We do not control or manage markets, do not intermediate transactions through the Protocol, and do not assume responsibility for repayment, collection, enforcement, recovery, market performance, or the outcome of any borrower-lender dispute.

If a borrower defaults, any rights and remedies belong to the relevant lender or other non-defaulting party under the applicable market terms, Master Loan Agreement (if any), Terms of Use, applicable law, or equity. Wildcat does not collect on behalf of lenders, direct lenders on whether or how to pursue claims, or participate in recovery, enforcement, liquidation, legal proceedings, or settlement activity.

Where appropriate, Wildcat may provide limited borrower-identifying information that is reasonably necessary for a lender to evaluate and, if it chooses, pursue its own rights and remedies. Any such disclosure is evaluated under applicable law, the Wildcat Terms of Use, the Wildcat Privacy Policy, and any applicable contractual restrictions. That does not make Wildcat responsible for the lender's decision, the borrower's repayment, or the outcome of any proceedings.

### The Short Version, By Audience

**If you're a borrower:** a call with Wildcat, a handover to our compliance service provider, a full Sumsub KYB check, then your address goes on-chain and the rest is yours. Your legal identity becomes public; your physical address can be withheld if you'd prefer.

**If you're a lender:** every borrower here is a KYB-verified legal entity, and that carries real weight. Treat legal name, Ethereum address, headquarters, entity legal form and founded year as verified. Treat trading names, descriptions, links and market copy as borrower-supplied material to check for yourself, not as verified facts. And remember the drum we keep banging: verification confirms identity, not creditworthiness, and we don't underwrite a single one of these markets.

### Anything Else?

KYB and onboarding questions go to <contact@thewildcat.foundation>. Product and deployment questions can come to the Wildcat team directly. Any issues, questions or concerns with any of the above, let us know. We're trying to enable a better way of doing this than what came before.
