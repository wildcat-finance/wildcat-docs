# WildcatMarketBase.sol

The `WildcatMarketBase` is the base contract containing core state mutation and computation logic as well as storage variables and immutable values.

#### sentinel

```solidity
address public immutable sentinel;
```

Address with blacklist control, used for blocking sanctioned addresses.

#### borrower

```solidity
address public immutable borrower;
```

Address with authority to borrow assets from the market.

#### feeRecipient

```solidity
address public immutable feeRecipient;
```

Address that receives protocol fees.

#### protocolFeeBips

```solidity
uint256 public immutable protocolFeeBips;
```

Protocol fee added to interest paid by borrower.

One protocol fee bip is 0.01% of an [APR bip](wildcatmarketconfig.sol.md#annualinterestbips).

#### delinquencyFeeBips

```solidity
uint256 public immutable delinquencyFeeBips;
```

Penalty fee added to interest earned by lenders, does not affect protocol fee.

#### delinquencyGracePeriod

```solidity
uint256 public immutable delinquencyGracePeriod;
```

Time after which delinquency incurs penalty fee.

#### controller

```solidity
address public immutable controller;
```

Address of the market controller.

#### asset

```solidity
address public immutable asset;
```

Address of the [underlying asset](wildcatmarketbase.sol.md#asset).

#### withdrawalBatchDuration

```solidity
uint256 public immutable withdrawalBatchDuration;
```

Time before withdrawal batches are processed.

#### decimals

```solidity
uint8 public immutable decimals;
```

Token decimals, derived from [underlying asset](wildcatmarketbase.sol.md).

#### name

```solidity
string public name;
```

Token name, derived from [underlying asset](wildcatmarketbase.sol.md#asset).

#### symbol

```solidity
string public symbol;
```

Token symbol, derived from [underlying asset](wildcatmarketbase.sol.md#asset).

#### coverageLiquidity

```solidity
function coverageLiquidity() external view nonReentrantView returns (uint256);
```

Liquidity required based on the [current market state](wildcatmarketbase.sol.md#currentstate).

Reverts if:

* the reentrancy lock is engaged.

#### scaleFactor

```solidity
function scaleFactor() external view nonReentrantView returns (uint256);
```

Scale factor based on the [current m](wildcatmarketbase.sol.md#currentstate)[arket state](wildcatmarketbase.sol.md#currentstate).

Reverts if:

* the reentrancy lock is engaged.

#### totalAssets

```solidity
function totalAssets() public view returns (uint256);
```

Total market balance of the [underlying asset](wildcatmarketbase.sol.md#asset).

#### borrowableAssets

```solidity
function borrowableAssets() external view nonReentrantView returns (uint256);
```

Amount of the [underlying asset](wildcatmarketbase.sol.md#asset) that may be borrowed based on the [current market state](wildcatmarketbase.sol.md#currentstate).

Reverts if:

* the reentrancy lock is engaged.

#### accruedProtocolFees

```solidity
function accruedProtocolFees() external view nonReentrantView returns (uint256);
```

Amount of accrued protocol fees based on the [current market state](wildcatmarketbase.sol.md#currentstate).

Reverts if:

* the reentrancy lock is engaged.

#### previousState

```solidity
function previousState() external view returns (MarketState memory);
```

Returns the state of the market from the last state update, performing no computation or mutations.

#### currentState

```solidity
function currentState() external view nonReentrantView returns (MarketState memory state);
```

Calculates the current market state by applying fees and accrued interest from the last update.

This function does not update the global state, all mutations and computations are performed on a cached version of the market and withdrawal state in memory.

Procedures:

* If the timestamp matches that of the most recent state update:
  * Return the market state as is, performing no additional computations
* Otherwise:
  * If a withdrawal batch has expired:
    * Update the market state with the expiry timestamp for:
      * fees
      * delinquency when applicable
      * scale factor
      * withdrawal batch state
  * Otherwise, continue
  * Update the market state with the current timestamp for the following:
    * fees
    * delinquency when applicable
    * scale factor

Reverts if:

* the reentrancy lock is engaged.

#### scaledTotalSupply

```solidity
function scaledTotalSupply() external view nonReentrantView returns (uint256);
```

Returns the total supply of the current market state scaled by the [scale factor](wildcatmarketbase.sol.md#scalefactor).

Reverts if:

* the reentrancy lock is engaged.

#### scaledBalanceOf

```solidity
function scaledBalanceOf(address account) external view nonReentrantView returns (uint256);
```

Returns the balance of an account scaled by the [scale factor](wildcatmarketbase.sol.md#scalefactor).

Reverts if:

* the reentrancy lock is engaged.
* the account is blacklisted.

#### effectiveBorrowerAPR

```solidity
function effectiveBorrowerAPR() external view returns (uint256);
```

Effective interest rate paid by the [borrower](wildcatmarketbase.sol.md#borrower), based on the [current market state](wildcatmarketbase.sol.md#currentstate).

The [borrower](wildcatmarketbase.sol.md#borrower) is responsible for base APR, protocol fee, and penalty APR in place.

#### effectiveLenderAPR

```solidity
function effectiveLenderAPR() external view returns (uint256);
```

Effective interest rate earned by the lenders, based on the [current market state](../../../security-measures/code-security-reviews.md#code4rena-crowdsourced-security-review).

The lender earns the base APR and any penalty APR in place.
