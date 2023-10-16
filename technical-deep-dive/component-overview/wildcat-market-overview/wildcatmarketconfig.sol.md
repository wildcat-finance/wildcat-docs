# WildcatMarketConfig.sol

The `WildcatMarketConfig` is the configuration contract containing configuration and authorization logic.

#### maximumDeposit

```solidity
function maximumDeposit() external view returns (uint256);
```

Maximum amount that may be deposited into the market, based on the current market state.

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

Revokes an account's authorization to deposit assets and updates the market state.

Reverts if:

* the caller is not the [controller](wildcatmarketbase.sol.md#controller).
* the reentrancy lock is engaged.
* the account is blacklisted.

Logs:

* [AuthorizationStatusUpdated](events.md#authorizationstatusupdated)

#### grantAccountAuthorization

```solidity
function grantAccountAuthorization(address _account) external onlyController nonReentrant;
```

Restores an account's authorization to deposit assets and updates the market state.

Cannot be used to restore a blacklisted account's status.

Reverts if:

* the caller is not the [controller](wildcatmarketbase.sol.md#controller).
* the reentrancy lock is engaged.
* the account is blacklisted.

Logs:

* [AuthorizationStatusUpdated](events.md#authorizationstatusupdated)

#### nukeFromOrbit

```solidity
function nukeFromOrbit(address _account) external onlySentinel;
```

Block an account from interacting with the market, deletes its [balance](wildcatmarkettoken.sol.md#balanceof), and updates the market state.

Reverts if:

* the caller is not the [sentinel](wildcatmarketbase.sol.md#sentinel).

Logs:

* [Transfer](events.md#transfer)
* [AuthorizationStatusUpdated](events.md#authorizationstatusupdated)

#### stunningReversal

```solidity
function stunningReversal(address accountAddress) external nonReentrant 
```

Removes the blocked status from an account, setting it to Null instead.

Reverts if:

* The account was not blocked, with error `AccountNotBlocked`.
* The account is still flagged as sanctioned according to the [sentinel](wildcatmarketbase.sol.md#sentinel), with error `NotReversedOrStunning`.

Logs:

* AuthorizationStatusUpdated

#### setMaxTotalSupply

```solidity
function setMaxTotalSupply(uint256 _maxTotalSupply) external onlyController nonReentrant;
```

Sets the [maximum total supply](wildcatmarketconfig.sol.md#maxtotalsupply) and updates the market state. This only limits deposits and does not affect interest accrual.

Reverts if:

* the caller is not the [controller](wildcatmarketbase.sol.md#controller).
* the reentrancy lock is engaged.
* the new [maximum total supply](wildcatmarketconfig.sol.md#maxtotalsupply) is less than the [total supply](wildcatmarkettoken.sol.md#totalsupply).

Logs:

* [MaxTotalSupplyUpdated](events.md#maxtotalsupplyupdated)

#### setAnnualInterestBips

```solidity
function setAnnualInterestBips(uint16 _annualInterestBips) public onlyController nonReentrant;
```

Sets the [annual interest bips](wildcatmarketconfig.sol.md#annualinterestbips) and updates the market state.

Reverts if:

* the caller is not the [controller](wildcatmarketbase.sol.md#controller).
* the reentrancy lock is engaged.
* the new annual interest bips is greater than the max bip size.

Logs:

* [AnnualInterestBipsUpdated](events.md#annualinterestbipsupdated)

#### setLiquidityCoverageRatio

```solidity
function setLiquidityCoverageRatio(uint16 _liquidityCoverageRatio) public onlyController nonReentrant;
```

Sets the [liquidity coverage ratio](wildcatmarketconfig.sol.md#liquiditycoverageratio) and updates the market state.

Reverts if:

* the caller is not the [controller](wildcatmarketbase.sol.md#controller).
* the reentrancy lock is engaged.
* the new [liquidity coverage ratio](wildcatmarketconfig.sol.md#liquiditycoverageratio) is greater than the max bip size.
* the new [liquidity required](wildcatmarketbase.sol.md#coverageliquidity) is greater than the [total assets](wildcatmarketbase.sol.md#totalassets).

Logs:

* [LiquidityCoverageRatioUpdated](events.md#liquiditycoverageratioupdated)
