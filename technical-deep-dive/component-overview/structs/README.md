---
description: The various complex datatypes used throughout the protocol.
---

# Structs

#### TemporaryReserveRatio

```solidity
struct TemporaryReserveRatio {
  uint128 reserveRatioBips;
  uint128 expiry;
}
```

#### TmpMarketParameterStorage

```solidity
struct TmpMarketParameterStorage {
  address asset;
  string namePrefix;
  string symbolPrefix;
  address feeRecipient;
  uint16 protocolFeeBips;
  uint128 maxTotalSupply;
  uint16 annualInterestBips;
  uint16 delinquencyFeeBips;
  uint32 withdrawalBatchDuration;
  uint16 reserveRatioBips;
  uint32 delinquencyGracePeriod;
}
```

#### TmpEscrowParams

```solidity
struct TmpEscrowParams {
    address borrower;
    address account;
    address asset;
  }
```

#### MarketParameters

```solidity
struct MarketParameters {
  address asset;
  string namePrefix;
  string symbolPrefix;
  address borrower;
  address controller;
  address feeRecipient;
  address sentinel;
  uint128 maxTotalSupply;
  uint16 protocolFeeBips;
  uint16 annualInterestBips;
  uint16 delinquencyFeeBips;
  uint32 withdrawalBatchDuration;
  uint16 reserveRatioBips;
  uint32 delinquencyGracePeriod;
}
```

#### MarketControllerParameters

```solidity
struct MarketControllerParameters {
  address archController;
  address borrower;
  address sentinel;
  address marketInitCodeStorage;
  uint256 marketInitCodeHash;
  uint32 minimumDelinquencyGracePeriod;
  uint32 maximumDelinquencyGracePeriod;
  uint16 minimumReserveRatioBips;
  uint16 maximumReserveRatioBips;
  uint16 minimumDelinquencyFeeBips;
  uint16 maximumDelinquencyFeeBips;
  uint32 minimumWithdrawalBatchDuration;
  uint32 maximumWithdrawalBatchDuration;
  uint16 minimumAnnualInterestBips;
  uint16 maximumAnnualInterestBips;
}
```

#### ProtocolFeeConfiguration

```solidity
struct ProtocolFeeConfiguration {
  address feeRecipient;
  address originationFeeAsset;
  uint80 originationFeeAmount;
  uint16 protocolFeeBips;
}
```

#### MarketParameterConstraints

```solidity
struct MarketParameterConstraints {
  uint32 minimumDelinquencyGracePeriod;
  uint32 maximumDelinquencyGracePeriod;
  uint16 minimumReserveRatioBips;
  uint16 maximumReserveRatioBips;
  uint16 minimumDelinquencyFeeBips;
  uint16 maximumDelinquencyFeeBips;
  uint32 minimumWithdrawalBatchDuration;
  uint32 maximumWithdrawalBatchDuration;
  uint16 minimumAnnualInterestBips;
  uint16 maximumAnnualInterestBips;
}
```

#### FIFOQueue

```solidity
struct FIFOQueue {
  uint128 startIndex;
  uint128 nextIndex;
  mapping(uint256 => uint32) data;
}
```

#### MarketState

```solidity
struct MarketState {
  bool isClosed;
  uint128 maxTotalSupply;
  uint128 accruedProtocolFees;
  // Underlying assets reserved for withdrawals which have been paid
  // by the borrower but not yet executed.
  uint128 normalizedUnclaimedWithdrawals;
  // Scaled token supply (divided by scaleFactor)
  uint104 scaledTotalSupply;
  // Scaled token amount in withdrawal batches that have not been
  // paid by borrower yet.
  uint104 scaledPendingWithdrawals;
  uint32 pendingWithdrawalExpiry;
  // Whether market is currently delinquent (liquidity under requirement)
  bool isDelinquent;
  // Seconds borrower has been delinquent
  uint32 timeDelinquent;
  // Annual interest rate accrued to lenders, in basis points
  uint16 annualInterestBips;
  // Percentage of outstanding balance that must be held in liquid reserves
  uint16 reserveRatioBips;
  // Ratio between internal balances and underlying token amounts
  uint112 scaleFactor;
  uint32 lastInterestAccruedTimestamp;
}
```

#### Account

```solidity
struct Account {
  AuthRole approval;
  uint104 scaledBalance;
}
```

#### WithdrawalBatch

```solidity
/**
 * Withdrawals are grouped together in batches with a fixed expiry.
 * Until a withdrawal is paid out, the tokens are not burned from the market
 * and continue to accumulate interest.
 */
struct WithdrawalBatch {
  // Total scaled amount of tokens to be withdrawn
  uint104 scaledTotalAmount;
  // Amount of scaled tokens that have been paid by borrower
  uint104 scaledAmountBurned;
  // Amount of normalized tokens that have been paid by borrower
  uint128 normalizedAmountPaid;
}
```

#### AccountWithdrawalStatus

```solidity
struct AccountWithdrawalStatus {
  uint104 scaledAmount;
  uint128 normalizedAmountWithdrawn;
}
```

#### WithdrawalData

```solidity
struct WithdrawalData {
  FIFOQueue unpaidBatches;
  mapping(uint32 => WithdrawalBatch) batches;
  mapping(uint256 => mapping(address => AccountWithdrawalStatus)) accountStatuses;
}
```

