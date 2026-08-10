# Proving You Are An Affected Lender in a Default

## Proving You Are An Affected Lender

If you loaned capital to a market that has gone into default, you can prove that you are one of its lenders by producing a signed claim at [juris.wildcat.finance](https://juris.wildcat.finance/) and sending the resulting *verification bundle* to the Wildcat Foundation. That same proof is how you ask for the borrower information collected during their KYC / KYB onboarding.

{% hint style="warning" %}
**Disclaimer:** The Foundation can only share information it is *actually allowed* to share. Producing a valid proof is what gets your request looked at. It is not a guarantee of what comes back. Be advised that Wildcat treats indications of bad-faith conduct seriously. Where Wildcat determines that a borrower has ceased to act in good faith, become unresponsive, abandoned its obligations, or engaged in conduct that may violate applicable law, Wildcat reserves the right to restrict that borrower's access to the Products, report the matter to the appropriate authorities, cooperate with regulatory or law-enforcement investigations, and take any other steps available to it under the Terms of Use and applicable law.
{% endhint %}

What the tool checks is one specific, protocol-observable condition: whether a market has been delinquent for longer than its grace period plus 90 days. That is the only kind of default it can see and validate from the outside, because it lives entirely in the protocol's own on-chain state. It is *not* the same as an Event of Default under a Master Loan Agreement. An MLA is a contract between you and the borrower, so any default defined there (which may trigger earlier, or on grounds the protocol never observes) is a matter for that agreement and your advisors, not something this tool can confirm. What the tool shows you is the protocol-level status on each market, so you can confirm *that much* with your own eyes before you sign anything.

### Before You Start

You will want two items to hand:

* **The borrower address** of the market you lent to. You can find this on the borrower's profile at [app.wildcat.finance](https://app.wildcat.finance). While you are there, the profile also carries the basics on who the borrower is (legal name, registered-address details and so on), which is worth a read.
* **The wallet you hold the relevant debt tokens in.** This matters: the proof attests to the address that holds your position, so connecting the wrong wallet produces a proof for the wrong lender.

### Producing Your Proof

Everything happens in one place, the Wildcat Lender Claim Intake tool at [juris.wildcat.finance](https://juris.wildcat.finance/). It walks you from finding your market through to a signed bundle in five steps.

1. **Find your market.** Paste the borrower address into *Borrower & Market* and hit **Find markets**. Pick your market from the list, and check that it shows as *in default* before you go any further.
2. **Connect your wallet.** Click **Connect wallet** and connect the wallet you lent with. This is the address the proof will vouch for, so make sure it is the right one.
3. **Check your eligibility.** The tool shows you the market, the borrower address, and the amount owed to your connected wallet. Have a look and make sure it matches the position you think you hold.
4. **Fill in your details.** Give your full name, a way to reach you (an email, or another contact method such as Telegram or Signal, at least one of the two), and your country.
5. **Sign and submit.** Tick the box confirming your details are accurate and that you intend to submit the proof as evidence of your eligibility, then click **Sign & submit claim** and sign in your wallet when prompted. This is a message signature, not an on-chain transaction, so there is no gas to pay. Your eligibility is re-checked at the moment you submit.

Once it goes through, the tool confirms the wallet, the amount owed, the market and the block it read, and then hands you the material below.

### Sending It To The Foundation

After you submit, the tool produces a section labelled **Verification bundle (send this to the Wildcat Foundation)**. That bundle is what we need: it carries the signed data, your signature, the address recovered from that signature, and the market, lender and amount owed as read back from the server. In other words, everything required to check that you are who you say you are.

To send it:

* Click **Copy verification bundle**, then paste it directly into the body of your email. Paste it exactly as copied, without editing it (a bundle that has been trimmed or reformatted may not verify).
* Do not send the bundle as an attachment. Paste the text straight into the email itself. Attachments (files, screenshots, documents) may not be opened, and a proof we cannot read is a proof we cannot act on.
* Email it to <contact@thewildcat.foundation>.
* Use the subject line `Default Lender - [Your wallet address]`.
* In the body, alongside the pasted bundle, tell us in a line or two what information you are requesting.

### What Happens Next

The Foundation will get back to you as soon as they reasonably can. Please give it some time, though: where a request touches sensitive information, that information may need to be legally reviewed and signed off before it can leave our hands. That review is not instant, and requests are often worked through in batches rather than one at a time, so it can take a while before you hear back.

Be aware that an email that does not contain a valid verification bundle *pasted into the body* from the correct lender wallet, a way to contact you, and a note on what you are asking for, will not get a reply. Bundles sent as attachments rather than pasted into the email count as incomplete. The Foundation cannot act on a request they cannot verify, so paste the complete bundle into the body before you send.

### The Part We Have To Repeat

We said it at the top and we will say it again here, because it is the part that matters most.

Anything the Foundation provides is subject at all times to applicable law, the [Wildcat Terms of Use](https://docs.wildcat.finance/legal/wildcat-terms-of-use), the [Privacy Policy](https://docs.wildcat.finance/legal/protocol-ui-privacy-policy), and any contractual restrictions that apply, including those arising from third-party KYC / KYB provider arrangements. Within those limits, the Foundation may pass on only the limited borrower-identifying information available to it that it considers reasonably necessary for you to evaluate and, if you choose, pursue whatever rights and remedies are open to you under the Master Loan Agreement, applicable law, or equity. The Foundation shares only what it is permitted to share, and weighs every request against those same constraints.

None of this is advice on whether or how to chase a claim, and the Foundation is not a party to your agreement with the borrower, does not enforce it, and is not on the hook for repayment, recovery or the outcome of any dispute. Those calls are yours and your advisors' to make.
