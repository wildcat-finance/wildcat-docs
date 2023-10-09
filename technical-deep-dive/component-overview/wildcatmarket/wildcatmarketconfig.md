---
description: issa wildcat market config innit
---

# WildcatMarketConfig

The `WildcatMarketConfig` is the configuration contract containing configuration and authorization logic.

#### maximumDeposit

```solidity
function maximumDeposit() external view returns (uint256);
```

Maximum amount that may be deposited into the market, based on the [current vault state](wildcatmarketbase.md#currentstate).

#### maxTotalSupply

```solidity
function maxTotalSupply() external view returns (uint256);
```

Maximum supply the market can reach via deposits (does not apply to interest accrual).

#### annualInterestBips

```solidity
function annualInterestBips() external view returns (uint256);
```

Returns the APR earned by lenders in bips.

One annual APR bip is 0.01% interest per year.

#### liquidityCoverageRatio

```solidity
function liquidityCoverageRatio() external view returns (uint256);
```

Percentage of outstanding balance that must be held in liquid reserves.

#### revokeAccountAuthorization

```solidity
function revokeAccountAuthorization(address _account) external onlyController nonReentrant;
```

Revokes an account's authorization to deposit assets and [updates the vault state](wildcatmarket.md#updatestate).

Reverts if:

* the caller is not the [controller](wildcatmarketbase.md#controller).
* the reentrancy lock is engaged.
* the account is blacklisted.

Logs:

* [AuthorizationStatusUpdated](events.md#authorizationstatusupdated)

#### grantAccountAuthorization

```solidity
function grantAccountAuthorization(address _account) external onlyController nonReentrant;
```

Restores an account's authorization to deposit assets and [updates the vault state](wildcatmarket.md#updatestate).

Cannot be used to restore a blacklisted account's status.

Reverts if:

* the caller is not the [controller](wildcatmarketbase.md#controller).
* the reentrancy lock is engaged.
* the account is blacklisted.

Logs:

* [AuthorizationStatusUpdated](events.md#authorizationstatusupdated)

#### nukeFromOrbit

```solidity
function nukeFromOrbit(address _account) external onlySentinel;
```

Block an account from interacting with the market, deletes its [balance](wildcatmarkettoken.md#balanceof), and [updates the vault state](wildcatmarket.md#updatestate).

Reverts if:

* the caller is not the [sentinel](wildcatmarketbase.md#sentinel).

Logs:

* [Transfer](events.md#transfer)
* [AuthorizationStatusUpdated](events.md#authorizationstatusupdated)

#### setMaxTotalSupply

```solidity
function setMaxTotalSupply(uint256 _maxTotalSupply) external onlyController nonReentrant;
```

Sets the [maximum total supply](wildcatmarketconfig.md#maxtotalsupply) and [updates the vault state](wildcatmarket.md#updatestate). This only limits deposits and does not affect interest accrual.

Reverts if:

* the caller is not the [controller](wildcatmarketbase.md#controller).
* the reentrancy lock is engaged.
* the new [maximum total supply](wildcatmarketconfig.md#maxtotalsupply) is less than the [total supply](wildcatmarkettoken.md#totalsupply).

Logs:

* [MaxTotalSupplyUpdated](events.md#maxtotalsupplyupdated)

#### setAnnualInterestBips

```solidity
function setAnnualInterestBips(uint16 _annualInterestBips) public onlyController nonReentrant;
```

Sets the [annual interest bips](wildcatmarketconfig.md#annualinterestbips) and [updates the vault state](wildcatmarket.md#updatestate).

Reverts if:

* the caller is not the [controller](wildcatmarketbase.md#controller).
* the reentrancy lock is engaged.
* the new annual interest bips is greater than the max bip size.

Logs:

* [AnnualInterestBipsUpdated](events.md#annualinterestbipsupdated)

#### setLiquidityCoverageRatio

```solidity
function setLiquidityCoverageRatio(uint16 _liquidityCoverageRatio) public onlyController nonReentrant;
```

Sets the [liquidity coverage ratio](wildcatmarketconfig.md#liquiditycoverageratio) and [updates the vault state](wildcatmarket.md#updatestate).

Reverts if:

* the caller is not the [controller](wildcatmarketbase.md#controller).
* the reentrancy lock is engaged.
* the new [liquidity coverage ratio](wildcatmarketconfig.md#liquiditycoverageratio) is greater than the max bip size.
* the new [liquidity required](wildcatmarketbase.md#coverageliquidity) is greater than the [total assets](wildcatmarketbase.md#totalassets).

Logs:

* [LiquidityCoverageRatioUpdated](events.md#liquiditycoverageratioupdated)
