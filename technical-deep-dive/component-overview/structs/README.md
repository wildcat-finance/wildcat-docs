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

## The Data Within Withdrawal Structs

The Wildcat approach to handling withdrawals is novel, so it's worth quickly digging into what the various values within the structs refer to. For more details on normalized versus scaled amounts, see [this subpage](some-notes-on-normalized-versus-scaled-amounts.md).

### **Withdrawal Data In** `MarketState`

* `uint128 normalizedUnclaimedWithdrawals` - amount of underlying assets paid to batches but not yet claimed in `executeWithdrawal`
* `uint104 scaledPendingWithdrawals` - sum of unpaid amounts for all withdrawal batches
* `uint32 pendingWithdrawalExpiry` - expiry timestamp of the current unexpired withdrawal batch.

`scaledPendingWithdrawals` is tracked because borrowers are obligated to honour 100% of pending withdrawals and the reserve ratio for the rest of the total supply to avoid delinquency.

### **The `WithdrawalData` Struct**

* `FIFOQueue unpaidBatches` - first-in-first-out queue of timestamps (identifiers) for `WithdrawalBatch`es that have expired but have not been fully honoured (i.e. `scaledAmountBurned` < `scaledTotalAmount`). Expiries are popped off the front of the list as the batches are completely paid off.
* `mapping(uint32 => WithdrawalBatch) batches` - mapping of withdrawal batches using their expiry timestamps as keys
* `mapping(uint256 => mapping(address => AccountWithdrawalStatus)) accountStatuses` - mapping of account withdrawal statuses by expiry and address.

### **The `WithdrawalBatch` Struct**

* `scaledTotalAmount` - sum of scaledAmount for all `AccountWithdrawalStatus` in the batch
* `scaledAmountBurned` - scaled tokens burned to pay for the batch - increases when `_applyWithdrawalBatchPayment` reduces `scaledTotalSupply`
* `normalizedAmountPaid` - total amount of underlying assets set aside to honour the batch's withdrawals.

### **The `AccountWithdrawalStatus` Struct**

* `uint104 scaledAmount` - scaled withdrawal amount subtracted from lender's balance when they call `queueWithdrawal`.
* `uint128 normalizedAmountWithdrawn` - amount of underlying assets the lender has already claimed

**Notes:** Scaled amounts are the original amounts lenders sent to the market when they queued a withdrawal.

Until their requests are honoured (assets reserved for the batch), they continue accruing interest, hence the distinction between scaled/normalized amounts in batches.

The normalized amount is the value their tokens had at the time they were actually paid by the borrower and made available for lenders to redeem.

In `_applyWithdrawalBatchPayment`, some `normalizedAmount` of underlying is removed from the market's available liquidity and reserved to pay for the batch (added to `batch.normalizedAmountPaid` and `state.normalizedUnclaimedWithdrawals`).

The corresponding `scaledAmount` is added to `batch.scaledAmountBurned` and subtracted from `state.scaledTotalSupply` and `state.scaledPendingWithdrawals`.

The normalized amount set aside for the batch can only be used to execute withdrawal requests for this batch - the market's balance in the underlying assets can never go below `normalizedUnclaimedWithdrawals`.

Just as borrowers can make multiple partial payments toward a batch over time, lenders can execute multiple partial redemptions.

Lenders are always entitled to a pro-rata share of the total underlying assets that have been paid toward a batch at any given time. `normalizedAmountWithdrawn` is tracked per lender so that it can be subtracted from their total claim on the batch's reserved assets if they have to do multiple partial redemptions.

As lenders redeem assets, their statuses' withdrawn amounts are increased and the market's `state.normalizedUnclaimedWithdrawals` is reduced.
