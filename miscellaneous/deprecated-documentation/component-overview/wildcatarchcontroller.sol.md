# WildcatArchController.sol

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

Events:

* BorrowerAdded

#### removeBorrower

```solidity
function removeBorrower(address borrower)
  external onlyOwner; 
```

Prevents a borrower `address` from deploying any further controllers or markets.

Reverts if:

* Not called by the owner of the archcontroller.

Events:

* BorrowerRemoved

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

Registers a new market controller factory smart contract, allowing borrowers to deploy new controllers and markets through it.

Reverts if:

* The controller factory has already been registered.

Events:

* ControllerFactoryAdded

#### removeControllerFactory

```solidity
function removeControllerFactory(address factory)
  external onlyOwner
```

Removes a market controller factory, preventing borrowers from deploying any further controllers and markets through it.

Reverts if:

* The controller factory address does not exist or has been removed.

Events:

* ControllerFactoryRemoved

#### isRegisteredControllerFactory

```solidity
function isRegisteredControllerFactory(address factory)
  external view returns (bool)
```



#### getRegisteredControllerFactories

```solidity
function getRegisteredControllerFactories()
  external view returns (address[] memory);
  
function getRegisteredControllerFactories(
    uint256 start,
    uint256 end
  ) external view returns (address[] memory arr);
```



#### getRegisteredControllerFactoriesCount

```solidity
function getRegisteredControllerFactoriesCount()
  external view returns (uint256);
```



#### registerController

```solidity
function registerController(address controller)
  external onlyControllerFactory;
```



#### removeController

```solidity
function removeController(address controller)
  external onlyOwner;
```



#### isRegisteredController

```solidity
function isRegisteredController(address controller)
  external view returns (bool);
```



#### getRegisteredControllers

```solidity
 function getRegisteredControllers()
   external view returns (address[] memory);
   
 function getRegisteredControllers(
    uint256 start,
    uint256 end
  ) external view returns (address[] memory arr);
```



#### getRegisteredControllersCount

```solidity
 function getRegisteredControllersCount()
   external view returns (uint256);
```



#### registerMarket

```solidity
 function registerMarket(address market)
   external onlyController;
```



#### removeMarket

```solidity
function removeMarket(address market)
  external onlyOwner;
```



#### isRegisteredMarket

```solidity
function isRegisteredMarket(address market)
  external view returns (bool);
```



#### getRegisteredMarkets

```solidity
 function getRegisteredMarkets()
   external view returns (address[] memory);
 
 function getRegisteredMarkets(
    uint256 start,
    uint256 end
  ) external view returns (address[] memory arr);
```



#### getRegisteredMarketsCount

<pre class="language-solidity"><code class="lang-solidity"><strong> function getRegisteredMarketsCount()
</strong><strong>   external view returns (uint256);
</strong></code></pre>

