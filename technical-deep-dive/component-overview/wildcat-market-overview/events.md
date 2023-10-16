# Events

#### Transfer

```solidity
event Transfer(address indexed from, address indexed to, uint256 value);
```

Logs the transfer of the market token.

#### Approval

```solidity
event Approval(address indexed owner, address indexed spender, uint256 value);
```

Logs changes in allowance with the market token.

#### MaxTotalSupplyUpdated

```solidity
event MaxTotalSupplyUpdated(uint256 assets);
```

Logs changes to the maximum total supply of the market token.

#### AnnualInterestBipsUpdated

```solidity
event AnnualInterestBipsUpdated(uint256 annualInterestBipsUpdated);
```

Logs changes to the APR bips.

#### LiquidityCoverageRatioUpdated

```solidity
event LiquidityCoverageRatioUpdated(uint256 liquidityCoverageRatioUpdated);
```

Logs changes to the liquidity coverage ratio

#### Deposit

```solidity
event Deposit(address indexed account, uint256 assetAmount, uint256 scaledAmount);
```

Logs deposits to the market.

#### Borrow

```solidity
event Borrow(uint256 assetAmount);
```

Logs borrows from the market.

#### MarketClosed

```solidity
event MarketClosed(uint256 timestamp);
```

Logs the closure of a market.

#### FeesCollected

```solidity
event FeesCollected(uint256 assets);
```

Logs the collection of fees.

#### StateUpdated

```solidity
event StateUpdated(uint256 scaleFactor, bool isDelinquent);
```

Logs changes to the market state.

#### ScaleFactorUpdated

```solidity
event ScaleFactorUpdated(
    uint256 scaleFactor,
    uint256 baseInterestRay,
    uint256 delinquencyFeeRay,
    uint256 protocolFee
);
```

Logs changes to the scale factor.

#### AuthorizationStatusUpdated

```solidity
event AuthorizationStatusUpdated(address indexed account, AuthRole role);
```

Logs changes to an account's authorization.

#### WithdrawalBatchExpired

```solidity
event WithdrawalBatchExpired(
    uint256 expiry,
    uint256 scaledTotalAmount,
    uint256 scaledAmountBurned,
    uint256 normalizedAmountPaid
);
```

Logs withdrawal batch expiration on market state changes.

#### WithdrawalBatchCreated

```solidity
event WithdrawalBatchCreated(uint256 expiry);
```

Logs the creation of a withdrawal batch.

#### WithdrawalBatchClosed

```solidity
event WithdrawalBatchClosed(uint256 expiry);
```

Logs the closure of a withdrawal batch.

#### WithdrawalBatchPayment

```solidity
event WithdrawalBatchPayment(
    uint256 expiry,
    uint256 scaledAmountBurned,
    uint256 normalizedAmountPaid
);
```

Logs the payment of a withdrawal batch.

#### WithdrawalQueued

```solidity
event WithdrawalQueued(uint256 expiry, address account, uint256 scaledAmount);
```

Logs queued withdrawals.

#### WithdrawalExecuted

```solidity
event WithdrawalExecuted(uint256 expiry, address account, uint256 normalizedAmount);
```

Logs the execution of a withdrawal.

#### MarketDeployed

```solidity
event MarketDeployed(address indexed controller, address indexed underlying, address market)
```

Logs the deployment of a new market.
