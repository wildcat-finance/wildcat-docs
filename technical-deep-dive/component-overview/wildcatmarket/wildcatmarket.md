---
description: issa wildcat market innit
---

# WildcatMarket

The `WildcatMarket` is the final contract, containing all vault-related logic.

#### updateState

```solidity
function updateState() external;
```

Updates the vault state.

Procedures:

* If the timestamp is that of the last state update:
  * Return the vault state as is, performing no additional computations
* Otherwise:
  * If a withdrawal batch has expired:
    * Update the vault state with the expiry timestamp for:
      * fees
      * delinquency when applicable
      * scale factor
      * withdrawal batch state
    * Process the expired withdrawal batch
  * Otherwise, continue
  * If the block timestamp is still not that of the last state update:
    * Update the vault state with the expiry timestamp for:
      * fees
      * delinquency when applicable
      * scale factor
      * withdrawal batch state
  * Update the delinquency state

Logs:

* [ScaleFactorUpdated](events.md#scalefactorupdated)
* [StateUpdated](events.md#stateupdated)

#### depositUpTo

```solidity
function depositUpTo(uint256 amount) public virtual nonReentrant returns (uint256);
```

Deposits up to a given amount.

Procedures:

* [Update the vault state](wildcatmarket.md#updatestate)
* Reduce amount if it would exceed [total supply](wildcatmarkettoken.md#totalsupply)
* Scale the mint amount by the [scale factor](wildcatmarketbase.md#scalefactor)
* [Transfer](wildcatmarkettoken.md#transfer) deposit from the caller
* Increase the [total supply](wildcatmarkettoken.md#totalsupply)
* Update the delinquency state

Reverts if:

* the reentrancy guard is engaged.
* the scaled mint amount is zero.
* the caller is blacklisted.
* the caller is not authorized to deposit.

Logs:

* [Transfer](events.md#transfer)
* [Deposit](events.md#deposit)

#### deposit

```solidity
function deposit(uint256 amount) external virtual;
```

Calls [depositUpTo](wildcatmarket.md#depositupto) internally then checks the [total supply](wildcatmarkettoken.md#totalsupply) would have been exceeded.

Reverts if:

* amount would have exceeded the [total supply](wildcatmarkettoken.md#totalsupply).

#### collectFees

```solidity
function collectFees() external nonReentrant;
```

Collects protocol fees and [updates the vault state](wildcatmarket.md#updatestate).

Coverage for deposits takes precedence over fee revenue.

Reverts if:

* the reentrancy guard is engaged.
* the [total assets](wildcatmarketbase.md#totalassets) is less than the liquidity required for withdrawals.

Logs:

* [FeesCollected](events.md#feescollected)

#### borrow

```solidity
function borrow(uint256 amount) external onlyBorrower nonReentrant;
```

Borrows an amount from the vault and [updates the vault state](wildcatmarket.md#updatestate).

Reverts if:

* the reentrancy guard is engaged.
* the caller is not the [borrower](wildcatmarketbase.md#borrower).
* the amount is greater than the [borrowable assets](wildcatmarketbase.md#borrowableassets).

Logs:

* [Borrow](events.md#borrow)

#### closeVault

```solidity
function closeVault() external onlyController nonReentrant;
```

Sets the vault to 0% [APR](wildcatmarketconfig.md#annualinterestbips), [updates the vault state](wildcatmarket.md#updatestate), and [transfers](wildcatmarkettoken.md#transfer) the outstanding balance for full redemption.

Reverts if:

* the reentrancy guard is engaged.
* the caller is not the [controller](wildcatmarketbase.md#controller).

Logs:

* [VaultClosed](events.md#vaultclosed)
