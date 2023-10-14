# WildcatVaultController.sol

A `WildcatVaultController` contract is \[TODO]

#### archController

```solidity
 IWildcatArchController public immutable archController;
```



#### controllerFactory

```solidity
 IWildcatVaultControllerFactory public immutable controllerFactory;
```



#### borrower

```solidity
 address public immutable borrower;
```



#### sentinel

```solidity
 address public immutable sentinel;
```



#### vaultInitCodeStorage

```solidity
 address public immutable vaultInitCodeStorage;
```



#### vaultInitCodeHash

<pre class="language-solidity"><code class="lang-solidity"><strong> uint256 public immutable vaultInitCodeHash;
</strong></code></pre>



#### temporaryExcessReserveRatio

```solidity
 mapping(address => TemporaryReserveRatio) public temporaryExcessReserveRatio;
```



#### getAuthorizedLenders

```solidity
 function getAuthorizedLenders()
   external view returns (address[] memory);
   
 function getAuthorizedLenders(
    uint256 start,
    uint256 end
  ) external view returns (address[] memory arr);
```



#### getAuthorizedLendersCount

```solidity
 function getAuthorizedLendersCount()
   external view returns (uint256);
```



#### isAuthorizedLender

```solidity
 function isAuthorizedLender(address lender)
   external view virtual returns (bool);
```



#### authorizeLenders

```solidity
 function authorizeLenders(address[] memory lenders)
   external onlyBorrower;
```



#### deauthorizeLenders

```solidity
 function deauthorizeLenders(address[] memory lenders)
   external onlyBorrower;
```



#### updateLenderAuthorization

```solidity
   function updateLenderAuthorization(address lender, address[] memory vaults)
     external;
```



#### isControlledVault

```solidity
 function isControlledVault(address vault)
   external view returns (bool);
```



#### getControlledVaults

```solidity
 function getControlledVaults()
   external view returns (address[] memory);
   
 function getControlledVaults(
    uint256 start,
    uint256 end
  ) external view returns (address[] memory arr);
```



#### getControlledVaultsCount

<pre class="language-solidity"><code class="lang-solidity"><strong> function getControlledVaultsCount()
</strong><strong>   external view returns (uint256);
</strong></code></pre>



#### computeVaultAddress

```solidity
 function computeVaultAddress(
    address asset,
    string memory namePrefix,
    string memory symbolPrefix
  ) external view returns (address);
```



#### getVaultParameters

<pre class="language-solidity"><code class="lang-solidity"><strong> function getVaultParameters()
</strong>   external view returns (VaultParameters memory parameters);
</code></pre>



#### deployVault

```solidity
 function deployVault(
    address asset,
    string memory namePrefix,
    string memory symbolPrefix,
    uint128 maxTotalSupply,
    uint16 annualInterestBips,
    uint16 delinquencyFeeBips,
    uint32 withdrawalBatchDuration,
    uint16 reserveRatioBips,
    uint32 delinquencyGracePeriod
  ) external returns (address vault);
```



#### getParameterConstraints

```solidity
 function getParameterConstraints()
   external view returns (VaultParameterConstraints memory constraints);
```



#### setAnnualInterestBips

```solidity
 function setAnnualInterestBips(
    address vault,
    uint16 annualInterestBips
  ) external virtual onlyBorrower onlyControlledVault(vault);
```



#### resetReserveRatio

```solidity
 function resetReserveRatio(address vault)
   external virtual;
```

