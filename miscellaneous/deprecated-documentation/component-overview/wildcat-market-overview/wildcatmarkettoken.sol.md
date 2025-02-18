# WildcatMarketToken.sol

The `WildcatMarketToken` is the token-related logic contract containing functions for transfers and approvals.

#### allowance

```solidity
mapping(address => mapping(address => uint256)) public allowance;
```

Amount of the market token that a spender may transfer on behalf of another owner.

#### balanceOf

```solidity
function balanceOf(address account) public view virtual nonReentrantView returns (uint256);
```

Balance of an account based on the [current market state](wildcatmarketbase.sol.md#currentstate) scaled by the [scale factor](wildcatmarketbase.sol.md#scalefactor).

Reverts if:

* the reentrancy lock is engaged.

#### totalSupply

```solidity
function totalSupply() external view virtual nonReentrantView returns (uint256);
```

Total supply of the market token based on the [current market state](wildcatmarketbase.sol.md#currentstate) scaled by the [scale factor](wildcatmarketbase.sol.md#scalefactor).

Reverts if:

* the reentrancy lock is engaged.

#### approve

```solidity
function approve(address spender, uint256 amount) external virtual nonReentrant returns (bool);
```

Sets the [allowance](wildcatmarkettoken.sol.md#allowance) of the caller for the given spender to [transfer](wildcatmarkettoken.sol.md#transfer) on their behalf.

Reverts if:

* the reentrancy lock is engaged.

Logs:

* [Approval](events.md#approval)

#### transfer

```solidity
function transfer(address to, uint256 amount) external virtual nonReentrant returns (bool);
```

Transfers an amount of the market token from the caller to another account and [updates the market state](wildcatmarket.sol.md#updatestate).

Reverts if:

* the reentrancy lock is engaged.
* the caller's scaled [balance](wildcatmarkettoken.sol.md#balanceof) is less than the scaled transfer amount.
* the caller is blacklisted.
* the receiver is blacklisted.

Logs:

* [Transfer](events.md#transfer)

#### transferFrom

```solidity
function transferFrom(
    address from,
    address to,
    uint256 amount
) external virtual nonReentrant returns (bool);
```

Transfers an amount of the market token from one account to another, decreases the [allowance](wildcatmarkettoken.sol.md#allowance) by the amount if applicable, and [updates the market state](wildcatmarket.sol.md#updatestate).

Reverts if:

* the reentrancy lock is engaged.
* the caller's [allowance](wildcatmarkettoken.sol.md#allowance) for the sender is less than the amount.
* the caller's scaled [balance](wildcatmarkettoken.sol.md#balanceof) is less than the scaled transfer amount.
* the caller is blacklisted.
* the receiver is blacklisted.

Logs:

* [Transfer](events.md#transfer)
* [Approval](events.md#approval)
