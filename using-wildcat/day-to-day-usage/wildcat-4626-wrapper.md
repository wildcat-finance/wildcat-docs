# Wildcat 4626 Wrapper

## ERC-4626 Vault Wrappers

Wildcat market tokens rebase: your balance increases automatically as interest accrues. This is great for tracking what you are owed, but causes problems in certain situations — bridging to another chain, providing liquidity on most DEXs, or reconciling PnL for accounting purposes all work better with a stable token balance.

The ERC-4626 vault wrapper solves this. It converts your rebasing market token into a standard non-rebasing vault share that holds its balance steady while still appreciating in value over time.

> If you want to understand exactly why Wildcat market tokens rebase and how the underlying math works, see [The Scale Factor](../../technical-overview/security-developer-dives/the-scale-factor.md).

***

### What Changes and What Stays the Same

When you wrap your market tokens:

* Your **share balance stays fixed**. It does not tick upward every block the way a regular market token does.
* Your **shares increase in value** over time instead. Each share becomes redeemable for more market tokens as interest accrues.
* You are **still exposed to the same market**. The wrapper is a thin layer on top. The underlying credit risk, withdrawal process, and market parameters do not change.
* Your wrapped token will appear in wallets and interfaces as **v-\[marketSymbol]** (e.g. v-wctUSDC).

> For a deeper look at how Wildcat markets behave at the protocol level, including deposits, withdrawals, and interest accrual, see [Core Behaviour](../../technical-overview/security-developer-dives/core-behaviour.md).

***

### Who Can Deploy a Wrapper

Any registered Wildcat market can have a wrapper deployed for it. Either the borrower (at market deployment) or any lender (at any point afterwards) can deploy one. Only one wrapper can exist per market — if one already exists, you use that one rather than deploying a new one.

> Deployed wrapper factory addresses for mainnet and Sepolia can be found in Contract Deployments.

***

### How to Use the Wrapper

#### Wrapping (converting market tokens to vault shares)

1. Go to the market page for the market you hold tokens in.
2. Navigate to the wrapper section and select **Wrap**.
3. Enter the amount of market tokens you want to wrap.
4. Approve the wrapper contract to transfer your market tokens (one-time approval per market).
5. Confirm the transaction. You receive v-\[marketSymbol] shares in return.

> **Important:** Do not send market tokens directly to the wrapper contract address. This will not mint shares. Always use the wrap function in the app.

#### Unwrapping (converting vault shares back to market tokens)

1. On the same wrapper section, select **Unwrap**.
2. Enter the number of shares you want to redeem.
3. Confirm the transaction. You receive the corresponding market tokens.

Unwrapping gives you back your rebasing market tokens. It does not trigger a withdrawal from the Wildcat market or return USDC (or whatever the underlying asset is). To exit to the underlying asset, you still need to go through the standard Wildcat withdrawal process after unwrapping.

***

### Getting Back to the Underlying Asset

The wrapper sits one step removed from the withdrawal queue. The full exit path is:

**Unwrap shares → receive market tokens → submit withdrawal request → wait for batch expiry → claim underlying asset**

The wrapper does not shortcut this process. If you need USDC back, you need to complete all steps.

> For a full walkthrough of the withdrawal request and claim lifecycle, see [Lenders](lenders.md) and the [Terminology](../terminology.md) entries for Withdrawal Request and Claim.

***

### Key Things to Know

**Your interest does not stop accruing.** The wrapper does not affect how the underlying market works. Interest continues to build and is reflected in the increasing redemption value of your shares.

**Sanctions checks still apply.** The wrapper uses the same sanctions sentinel as the underlying market. Sanctioned addresses cannot deposit into or redeem from the wrapper. See [The Sentinel](the-sentinel.md) for more on how sanctions handling works.

**The market capacity limit still applies.** If the market is at maximum capacity, you cannot deposit additional market tokens into the wrapper even if you hold them.

**The share count you see is not the market token amount you are owed.** Your shares will always redeem for more market tokens than their face count, because interest has accrued since you wrapped. The app will show you the current redemption value alongside your share balance.

**Delinquency does not affect the wrapper directly.** If the underlying market becomes delinquent, your wrapper shares still represent your claim on market tokens. What changes is the recoverability of those tokens, which depends on borrower behaviour. See [Delinquency](../delinquency.md) for more detail.

***

### Frequently Asked Questions

**Does wrapping affect my withdrawal rights?** No. Your underlying position in the market is unchanged. You can unwrap at any time and then submit a withdrawal request as normal.&#x20;

**Can I wrap tokens from a market I did not originally deposit into?** Yes, as long as you hold the market tokens (e.g. if they were transferred to you) and you pass the market's access controls. See [Market Access](market-access-via-policies-hooks.md) Via Policies/Hooks for how access controls work.

**What happens to my wrapped shares if the market becomes delinquent?** The wrapper is unaffected by delinquency directly. Your shares continue to represent your claim on the underlying market tokens. What changes is the recoverability of those tokens, which depends on the borrower's behaviour — the same as for any lender in that market.&#x20;

**Is there a fee for wrapping or unwrapping?** No. The wrapper charges no additional fee beyond standard Ethereum gas costs. For details on Wildcat's protocol fees more broadly, see [Protocol Usage Fees](../protocol-usage-fees.md).

***

### For Developers and Integrators

If you are building on top of the wrapper or integrating it into a protocol, the full technical reference including function signatures, error codes, and exchange rate helpers is in the [developer documentation](../../technical-overview/security-developer-dives/wildcat-4626-wrapper.md).

Note the known rounding behaviour between preview functions and execution functions before using previews as exact assertions in routing or accounting logic.
