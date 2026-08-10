---
description: How affected lenders use Juris to prove their position after a protocol-level default and ask the Wildcat Foundation for permitted borrower information.
---

# Proving You Are an Affected Lender in a Default

## Proving Your Lender Position

If you lent capital to a market that has gone into default, [Juris](https://juris.wildcat.finance/) can produce a signed claim proving that you are one of its lenders. Wildcat Labs built and hosts Juris. The data you submit through it goes to the Wildcat Foundation, which handles the claim from that point on. Send the resulting *verification bundle* to the Foundation; the same proof supports any request for borrower information collected during KYC / KYB onboarding.

{% hint style="warning" %}
**Disclaimer:** The Foundation can share only information it is *actually permitted* to share. A valid proof gets your request reviewed; it does not guarantee that anything comes back. The Foundation treats indications of bad-faith conduct seriously. If it determines that a borrower has ceased to act in good faith, become unresponsive, abandoned its obligations, or engaged in conduct that may violate applicable law, it may restrict that borrower's access to the Products, report the matter to the appropriate authorities, cooperate with regulatory or law-enforcement investigations, and take any other steps available under the Terms of Use and applicable law.
{% endhint %}

Juris checks one narrow, protocol-observable condition: whether a market has been delinquent for longer than its grace period plus 90 days. That is the only kind of default it can validate from on-chain state. It is *not* the same thing as an Event of Default under a Master Loan Agreement. An MLA is a contract between you and the borrower; a default under it may occur earlier, or for reasons the protocol never sees at all. That is a matter for the agreement and your advisors, not something Juris can confirm. Juris shows the protocol-level status of each market so you can at least confirm that much with your own eyes before signing anything.

### Before You Start

You will want two things to hand:

* **The borrower address** of the market you lent to. You can find it on the borrower's profile at [app.wildcat.finance](https://app.wildcat.finance). The profile also carries the basics on the borrower, including its legal name and registered-address details, so have a read while you are there.
* **The wallet you hold the relevant debt tokens in.** This matters: the proof attests to the address that holds your position, so connecting the wrong wallet produces a proof for the wrong lender.

### Producing Your Proof

Wildcat Labs hosts Juris at [juris.wildcat.finance](https://juris.wildcat.finance/). Everything from finding the market to producing the signed bundle happens there, in five steps.

1. **Find your market.** Paste the borrower address into *Borrower & Market* and hit **Find markets**. Pick your market from the list, and check that it shows as *in default* before you go any further.
2. **Connect your wallet.** Click **Connect wallet** and connect the wallet you lent with. This is the address the proof will vouch for, so make sure it is the right one.
3. **Check your eligibility.** Juris shows you the market, the borrower address, and the amount owed to your connected wallet. Have a look and make sure it matches the position you think you hold.
4. **Fill in your details.** Give your full name, a way to reach you (an email, or another contact method such as Telegram or Signal, at least one of the two), and your country.
5. **Sign and submit.** Tick the box confirming that your details are accurate and that you intend to submit the proof as evidence of your eligibility. Click **Sign & submit claim**, then sign in your wallet when prompted. This is a message signature, not an on-chain transaction, so there is no gas to pay. Juris checks your eligibility again at submission and sends the claim data to the Wildcat Foundation.

Once it goes through, Juris confirms the wallet, amount owed, market and block it read, then generates the verification bundle.

### Sending It to the Foundation

After submission, Juris produces a section labelled **Verification bundle (send this to the Wildcat Foundation)**. This is what the Foundation needs to verify your request: the signed data, your signature, the address recovered from it, and the market, lender and amount owed as read back from the server. Taken together, those show that you control the lender address behind the claim.

To send it:

* Click **Copy verification bundle**, then paste it directly into the body of your email. Paste it exactly as copied, without editing it (a bundle that has been trimmed or reformatted may not verify).
* Do not send the bundle as an attachment. Paste the text straight into the email itself. The Foundation may not open files, screenshots or documents, and cannot act on a proof it cannot read.
* Email it to <contact@thewildcat.foundation>.
* Use the subject line `Default Lender - [Your wallet address]`.
* Alongside the pasted bundle, tell the Foundation in a line or two what information you want.

### What Happens Next

The Foundation will reply as soon as it reasonably can. Give it some time, though: sensitive information may need legal review and sign-off before it can leave the Foundation's hands. Legal review is not instant, and requests are often worked through in batches rather than one at a time.

An email without a valid verification bundle *pasted into the body* from the correct lender wallet, a way to contact you, and a note explaining what you want will not get a reply. A bundle sent as an attachment counts as incomplete. The Foundation cannot act on a request it cannot verify, so paste the complete bundle into the email before sending it.

### The Bit That Bears Repeating

Anything the Foundation provides remains subject to applicable law, the [Wildcat Terms of Use](https://docs.wildcat.finance/legal/wildcat-terms-of-use), the [Privacy Policy](https://docs.wildcat.finance/legal/protocol-ui-privacy-policy), and any contractual restrictions, including those arising from third-party KYC / KYB provider arrangements. Within those limits, it may pass on only the limited borrower-identifying information available to it that it considers reasonably necessary for you to evaluate and, if you choose, pursue any rights and remedies open to you under the Master Loan Agreement, applicable law, or equity. The Foundation weighs every request against those same constraints.

None of this is advice on whether or how to pursue a claim. The Foundation is not a party to your agreement with the borrower, does not enforce it, and is not responsible for repayment, recovery or the outcome of a dispute. Those calls are for you and your advisors to make.
