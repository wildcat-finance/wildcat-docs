---
description: How affected lenders can use Juris to prove their position after a protocol-level default and request permitted borrower information from the Wildcat Foundation.
---

# Proving You Are an Affected Lender in a Default

## Proving You Are an Affected Lender

If you loaned capital to a market that has gone into default, you can prove that you are one of its lenders by producing a signed claim through [Juris](https://juris.wildcat.finance/). Juris is a lender-claim tool built and hosted by Wildcat Labs.

For this process, Wildcat Labs provides the Juris tool, while the Wildcat Foundation receives the data submitted through Juris and handles affected lenders' requests. After submitting a claim, you should send the resulting *verification bundle* to the Foundation. The same proof allows you to ask the Foundation for borrower information collected during the borrower's KYC / KYB onboarding.

{% hint style="warning" %}
**Disclaimer:** The Foundation can share only information that it is *actually permitted* to share. Producing a valid proof allows the Foundation to review your request; it does not guarantee that the Foundation will disclose any information. The Foundation treats indications of bad-faith conduct seriously. If the Foundation determines that a borrower has ceased to act in good faith, become unresponsive, abandoned its obligations, or engaged in conduct that may violate applicable law, the Foundation reserves the right to restrict that borrower's access to the Products, report the matter to the appropriate authorities, cooperate with regulatory or law-enforcement investigations, and take any other steps available to it under the Terms of Use and applicable law.
{% endhint %}

Juris checks one specific, protocol-observable condition: whether a market has been delinquent for longer than its grace period plus 90 days. This is the only kind of default Juris can validate from the protocol's on-chain state. It is *not* the same as an Event of Default under a Master Loan Agreement. An MLA is a contract between you and the borrower, so any default defined in that agreement—which may occur earlier or on grounds that the protocol never observes—is a matter for you, the borrower and your respective advisors. Juris cannot confirm it. Juris displays each market's protocol-level status so that you can review that status before signing anything.

### Before You Start

You will want two items to hand:

* **The borrower address** of the market you lent to. You can find this on the borrower's profile at [app.wildcat.finance](https://app.wildcat.finance). While you are there, the profile also carries the basics on who the borrower is (legal name, registered-address details and so on), which is worth a read.
* **The wallet you hold the relevant debt tokens in.** This matters: the proof attests to the address that holds your position, so connecting the wrong wallet produces a proof for the wrong lender.

### Producing Your Proof

Wildcat Labs hosts the Juris lender-claim tool at [juris.wildcat.finance](https://juris.wildcat.finance/). Juris guides you from finding your market to producing a signed bundle in five steps.

1. **Find your market.** Paste the borrower address into *Borrower & Market* and hit **Find markets**. Pick your market from the list, and check that it shows as *in default* before you go any further.
2. **Connect your wallet.** Click **Connect wallet** and connect the wallet you lent with. This is the address the proof will vouch for, so make sure it is the right one.
3. **Check your eligibility.** The tool shows you the market, the borrower address, and the amount owed to your connected wallet. Have a look and make sure it matches the position you think you hold.
4. **Fill in your details.** Give your full name, a way to reach you (an email, or another contact method such as Telegram or Signal, at least one of the two), and your country.
5. **Sign and submit.** Tick the box confirming your details are accurate and that you intend to submit the proof as evidence of your eligibility, then click **Sign & submit claim** and sign in your wallet when prompted. This is a message signature, not an on-chain transaction, so there is no gas to pay. Juris re-checks your eligibility when you submit the claim and sends the submitted claim data to the Wildcat Foundation.

Once the submission succeeds, Juris confirms the wallet, the amount owed, the market and the block it read. It then generates the verification bundle described below.

### Sending It To The Foundation

After you submit, Juris produces a section labelled **Verification bundle (send this to the Wildcat Foundation)**. The Foundation needs this bundle to verify your request. It contains the signed data, your signature, the address recovered from that signature, and the market, lender and amount owed as read back from the server. In other words, it contains the information the Foundation needs to verify that you control the lender address associated with the claim.

To send it:

* Click **Copy verification bundle**, then paste it directly into the body of your email. Paste it exactly as copied, without editing it (a bundle that has been trimmed or reformatted may not verify).
* Do not send the bundle as an attachment. Paste the text straight into the email itself. The Foundation may not open attachments such as files, screenshots or documents, and it cannot act on a proof it cannot read.
* Email it to <contact@thewildcat.foundation>.
* Use the subject line `Default Lender - [Your wallet address]`.
* In the body, alongside the pasted bundle, tell the Foundation in a line or two what information you are requesting.

### What Happens Next

The Foundation will respond as soon as reasonably practicable. Where a request concerns sensitive information, the information may require legal review and approval before the Foundation can disclose it. That review is not immediate, and the Foundation may process requests in batches, so it may take some time to receive a response.

The Foundation will not respond to an email that does not contain a valid verification bundle *pasted into the body* from the correct lender wallet, a way to contact you, and a note explaining what you are requesting. A bundle sent as an attachment rather than pasted into the email counts as incomplete. The Foundation cannot act on a request it cannot verify, so paste the complete bundle into the body before sending the email.

### Important Limitations

Anything the Foundation provides is subject at all times to applicable law, the [Wildcat Terms of Use](https://docs.wildcat.finance/legal/wildcat-terms-of-use), the [Privacy Policy](https://docs.wildcat.finance/legal/protocol-ui-privacy-policy), and any contractual restrictions that apply, including those arising from third-party KYC / KYB provider arrangements. Within those limits, the Foundation may pass on only the limited borrower-identifying information available to the Foundation that it considers reasonably necessary for you to evaluate and, if you choose, pursue whatever rights and remedies are open to you under the Master Loan Agreement, applicable law, or equity. The Foundation shares only what it is permitted to share and assesses every request against those constraints.

None of this is advice on whether or how to pursue a claim. The Foundation is not a party to your agreement with the borrower, does not enforce that agreement, and is not responsible for repayment, recovery or the outcome of any dispute. Those decisions are for you and your advisors to make.
