# WildcatVaultControllerFactory.sol

A `WildcatVaultControllerFactory` is: TODO

#### archController

```solidity
 IWildcatArchController public immutable archController;
```



#### sentinel

```solidity
 address public immutable sentinel;
```

Address with blacklist control, used for blocking sanctioned addresses.

#### vaultInitCodeStorage

```solidity
 address public immutable vaultInitCodeStorage;
```



#### vaultInitCodeHash

```solidity
 uint256 public immutable vaultInitCodeHash;
```



#### controllerInitCodeStorage

```solidity
 address public immutable controllerInitCodeStorage;
```



#### isDeployedController

```solidity
 function isDeployedController(address controller)
   external view returns (bool);
```



#### getDeployedControllersCount

```solidity
 function getDeployedControllersCount()
   external view returns (uint256);
```



#### getDeployedControllers

```solidity
 function getDeployedControllers()
   external view returns (address[] memory);
   
 function getDeployedControllers(
    uint256 start,
    uint256 end
  ) external view returns (address[] memory arr);
```



#### getProtocolFeeConfiguration

```solidity
 function getProtocolFeeConfiguration()
   external
   view
   returns (
     address feeRecipient,
     address originationFeeAsset,
     uint80 originationFeeAmount,
     uint16 protocolFeeBips
   );
```



#### setProtocolFeeConfiguration

```solidity
 function setProtocolFeeConfiguration(
   address feeRecipient,
   address originationFeeAsset,
   uint80 originationFeeAmount,
   uint16 protocolFeeBips
  ) external onlyArchControllerOwner;
```



#### getParameterConstraints

```solidity
 function getParameterConstraints()
   external view
    returns (VaultParameterConstraints memory constraints);
```



#### getVaultParameterParameters

```solidity
 function getVaultControllerParameters()
   external view virtual
    returns (VaultControllerParameters memory parameters);
```



#### deployController

```solidity
 function deployController()
   public returns (address controller);
```



#### deployControllerAndVault

```solidity
 function deployControllerAndVault(
   string memory namePrefix,
   string memory symbolPrefix,
   address asset,
   uint128 maxTotalSupply,
   uint16 annualInterestBips,
   uint16 delinquencyFeeBips,
   uint32 withdrawalBatchDuration,
   uint16 reserveRatioBips,
   uint32 delinquencyGracePeriod
  ) external returns (address controller, address vault);
```



#### computeControllerAddress

```solidity
 function computeControllerAddress(address borrower)
   external view returns (address);
```

