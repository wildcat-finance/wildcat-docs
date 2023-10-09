---
description: issa wildcat vault factory innit
---

# WildcatVaultFactory

The Vault Factory, `WildcatMarketFactory`, is responsible for deploying new `WildcatMarket` vaults.

#### VaultInitCodeHash

```solidity
bytes32 public immutable VaultInitCodeHash = keccak256(type(WildcatMarket).creationCode);
```

Initialization code hash for the WildcatMarket.

#### vaults

```solidity
address[] public vaults;
```

Array of vault addresses.

#### getVaultsCount

```solidity
function getVaultsCount() external view returns (uint256);
```

Number of [vaults](wildcatvaultfactory.md#vaults) deployed.

#### getVaults

```solidity
function getVaults(uint256 start, uint256 length) external view returns (address[] memory);
```

A slice of the [vault address array](wildcatvaultfactory.md#vaults), given a start and length.

#### getVaultParameters

```solidity
function getVaultParameters() external view returns (VaultParameters memory);
```

Vault parameters, a transient variable containing parameters for an active vault deployment.

#### deployVault

```solidity
function deployVault(VaultParameters memory vaultParameters) external returns (address vault);
```

Deploys a new vault with the `create2` opcode given some [vault parameters](wildcatvaultfactory.md#getvaultparameters).

Logs:

* [VaultDeployed](../wildcatmarket/events.md#vaultdeployed)

#### computeVaultAddress

```solidity
function computeVaultAddress(
    address controller,
    address deployer,
    address asset
) external view returns (address);
```

Helper function to pre-computes the address that the `create2` would return for a given [controller](../wildcatmarket/wildcatmarketbase.md#controller), deployer, and [asset](../wildcatmarket/wildcatmarketbase.md#asset).
