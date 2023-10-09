---
description: issa wildcat market withdrawals innit
---

# WildcatMarketWithdrawals

The `WildcatMarketWithdrawals` is the withdrawal-related logic contract containing function to handle withdrawal queueing, processing, executing, and viewing.

#### getUnpaidBatchExpiries

```solidity
function getUnpaidBatchExpiries() external view nonReentrantView returns (uint32[] memory);
```

Gets the unpaid, expired withdrawals.

Reverts if:

* the reentrancy lock is engaged.

#### getWithdrawalBatch

```solidity
function getWithdrawalBatch(uint32 expiry)
    external
    view
    nonReentrantView
    returns (WithdrawalBatch memory);
```

Gets a withdrawal for a given expiry based on the [current state](wildcatmarketbase.md#currentstate).

Reverts if:

* the reentrancy lock is engaged.

#### getAccountWithdrawalStatus

```solidity
function getAccountWithdrawalStatus(address accountAddress, uint32 expiry)
    external
    view
    nonReentrantView
    returns (AccountWithdrawalStatus memory);
```

Gets an account's withdrawal status for a given expiry.

Reverts if:

* the reentrancy lock is engaged.

#### getAvailableWithdrawalAmount

```solidity
function getAvailableWithdrawalAmount(address accountAddress, uint32 expiry)
    external
    view
    nonReentrantView
    returns (uint256);
```

Gets the amount available for an account to withdrawal for a given expiry based on the [current state](wildcatmarketbase.md#currentstate).

Reverts if:

* the reentrancy lock is engaged.
* the expiry is greater than the current timestamp.

#### queueWithdrawal

```solidity
function queueWithdrawal(uint256 amount) external nonReentrant;
```

Queues a withdrawal.

Procedures:

* [Update the vault state](wildcatmarket.md#updatestate)
* Scale the amount by the [scale factor](wildcatmarketbase.md#scalefactor)
* [Transfer](wildcatmarkettoken.md#transfer) the caller's vault tokens to the vault
* If there is a pending withdrawal batch:
  * Queue the withdrawal
* Otherwise:
  * Create a new withdrawal batch
  * Queue the withdrawal
* If the pool contains enough liquidity to cover the withdrawal:
  * Process withdrawal payment
* Otherwise:
  * Process as much of the withdrawal as possible and leave the rest to the queue

Reverts if:

* the reentrancy lock is engaged.
* the caller is blacklisted.
* the caller is not authorized to withdraw.
* the caller's [balance](wildcatmarkettoken.md#balanceof) is less than the amount.
* the scaled amount is zero.

Logs:

* [Transfer](events.md#transfer)
* [WithdrawalBatchCreated](events.md#withdrawalbatchcreated)
* [WithdrawalBatchPayment](events.md#withdrawalbatchpayment)

#### executeWithdrawal

```solidity
function executeWithdrawal(address accountAddress, uint32 expiry)
    external
    nonReentrant
    returns (uint256);
```

Executes a withdrawal for an account with a given expiry.

Procedures:

* [Update the vault state](wildcatmarket.md#updatestate)
* Update the withdrawal queue
* Update the account status
* Transfers the underlying asset to the account
* Return the amount scaled by the [scale factor](wildcatmarketbase.md#scalefactor)

Reverts if:

* the reentrancy lock is engaged.
* the expiry is greater than the current timestamp.

Logs:

* [WithdrawalExecuted](events.md#withdrawalexecuted)

#### processUnpaidWithdrawalBatch

```solidity
function processUnpaidWithdrawalBatch() external nonReentrant;
```

Processes the first unpaid withdrawal batch in the queue.

Procedures:

* [Update the vault state](wildcatmarket.md#updatestate)
* Apply withdrawal batch payment
* Remove the batch if fully paid

Reverts if:

* the reentrancy lock is engaged.
* the withdrawal batch queue is empty.

Logs:

* [WithdrawalBatchClosed](events.md#withdrawalbatchclosed)
* [WithdrawalBatchPayment](events.md#withdrawalbatchpayment)
