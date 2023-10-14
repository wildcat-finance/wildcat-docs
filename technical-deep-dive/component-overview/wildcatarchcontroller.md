# WildcatArchController

The `WildcatArchcontroller` is the contract that determines which addresses are capable of deploying controllers (and thereafter markets through these controllers).&#x20;

Controllers must be deployed through a controller factory, which must be registered with the archcontroller.

The addresses of all deployed controllers, factories and markets are logged by the archcontroller in its capacity as a registry: these are used for access control.&#x20;

#### registerBorrower

```solidity
function registerBorrower(address borrower)
  external onlyOwner;
```

Permits a borrower `address` to deploy controllers and markets.

Reverts if:

* Not called by the owner of the archcontroller.

#### removeBorrower

```solidity
function removeBorrower(address borrower)
  external onlyOwner; 
```

Prevents a borrower `address` from deploying any further controllers or markets.

Reverts if:

* Not called by the owner of the archcontroller.

#### isRegisteredBorrower

```solidity
function isRegisteredBorrower(address borrower)
  external view returns (bool);
```

Boolean lookup for whether an address is currently a registered borrower.

#### getRegisteredBorrowers

```solidity
function getRegisteredBorrowers() 
   external view returns (address[] memory);

function getRegisteredBorrowers(
    uint256 start,
    uint256 end
  ) external view returns (address[] memory arr);
```

Returns either the entire array of currently registered borrower addresses, or a slice of the array given start and end indices.

#### registerControllerFactory

```solidity
function registerControllerFactory(address factory)
  external onlyOwner;
```

TODO

#### removeControllerFactory

```solidity
function removeControllerFactory(address factory)
  external onlyOwner
```

TODO

#### isRegisteredControllerFactory

```solidity
function isRegisteredControllerFactory(address factory)
  external view returns (bool)
```

TODO

#### getRegisteredControllerFactories

```solidity
function getRegisteredControllerFactories()
  external view returns (address[] memory);
  
function getRegisteredControllerFactories(
    uint256 start,
    uint256 end
  ) external view returns (address[] memory arr);
```

TODO

#### getRegisteredControllerFactoriesCount

```solidity
function getRegisteredControllerFactoriesCount()
  external view returns (uint256);
```

TODO

#### registerController

```solidity
function registerController(address controller)
  external onlyControllerFactory;
```

TODO

#### removeController

```solidity
function removeController(address controller)
  external onlyOwner;
```

TODO

#### isRegisteredController

```solidity
function isRegisteredController(address controller)
  external view returns (bool);
```

TODO

#### getRegisteredControllers

```solidity
 function getRegisteredControllers()
   external view returns (address[] memory);
   
 function getRegisteredControllers(
    uint256 start,
    uint256 end
  ) external view returns (address[] memory arr);
```

TODO

#### getRegisteredControllersCount

```solidity
 function getRegisteredControllersCount()
   external view returns (uint256);
```

TODO

#### registerVault

```solidity
 function registerVault(address vault)
   external onlyController;
```

TODO

#### removeVault

```solidity
function removeVault(address vault)
  external onlyOwner;
```

TODO

#### isRegisteredVault

```solidity
function isRegisteredVault(address vault)
  external view returns (bool);
```

TODO

#### getRegisteredVaults

```solidity
 function getRegisteredVaults()
   external view returns (address[] memory);
 
 function getRegisteredVaults(
    uint256 start,
    uint256 end
  ) external view returns (address[] memory arr);
```

TODO

#### getRegisteredVaultsCount

<pre class="language-solidity"><code class="lang-solidity"><strong> function getRegisteredVaultsCount()
</strong><strong>   external view returns (uint256);
</strong></code></pre>

TODO
