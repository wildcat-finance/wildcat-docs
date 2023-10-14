# Events

#### Transfer

```solidity
event Transfer(address indexed from, address indexed to, uint256 value);
```

Logs the transfer of the vault token.

#### Approval

```solidity
event Approval(address indexed owner, address indexed spender, uint256 value);
```

Logs changes in allowance with the vault token.

#### MaxTotalSupplyUpdated

```solidity
event MaxTotalSupplyUpdated(uint256 assets);
```

Logs changes to the maximum total supply of the vault token.

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

Logs deposits to the vault.

#### Borrow

```solidity
event Borrow(uint256 assetAmount);
```

Logs borrows from the vault.

#### VaultClosed

```solidity
event VaultClosed(uint256 timestamp);
```

Logs the closure of a vault.

#### FeesCollected

```solidity
event FeesCollected(uint256 assets);
```

Logs the collection of fees.

#### StateUpdated

```solidity
event StateUpdated(uint256 scaleFactor, bool isDelinquent);
```

Logs changes to the vault state.

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

Logs withdrawal batch expiration on vault state changes.

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

#### VaultDeployed

```solidity
event VaultDeployed(address indexed controller, address indexed underlying, address vault)
```

Logs the deployment of a new vault.
