# Some Notes On Normalized versus Scaled Amounts

The scaled amounts used within the protocol are for internal accounting, whereas normalized amounts represent underlying amounts that the borrower owes.

The scale factor is a ray multiplier that grows over time as interest accrues. You scale a normalized amount by dividing by the scale factor (via `rayDiv`) and normalize a scaled amount by multiplying (via `rayMul`).

`balanceOf(account)` is `state.scaleAmount(scaledBalanceOf(account))` - the normalized balance is a claim on eventually being repaid that amount of underlying by the borrower.

The normalized values are used for token balances, total supply and inputs to all the stateful functions - users specify things in terms of debt on underlying asset amounts.

#### Example

* Scale Factor = 1&#x20;
* Base APR = 10%

Alice deposits 100 USDC into a market, and receives 100 West Ham Capital USDC as market tokens in exchange.

* Alice's Scaled Balance = 100 (100 / 1).

A year passes, and now the scale factor is 1.1 due to the 10% base APR.

Alice's balance of scaled tokens - the internal accounting value, `scaledBalanceOf` - is still 100, but her balance of West Ham Capital USDC - her claim on borrower debt, `balanceOf` - is now 110 (100 \* 1.1).

Bob now deposits 110 USDC, receives 110 West Ham Capital USDC

* Bob's Scaled Balance = 100 (110 / 1.1)

Now `totalSupply = 220`, `scaledTotalSupply = 200`.

If another year passes, scale factor will be 1.21 (as interest compounds on every state update), and thereafter `totalSupply = 242`, `scaledTotalSupply = 200.`

Alice and Bob would both have a balance of 121 West Ham Capital USDC.
