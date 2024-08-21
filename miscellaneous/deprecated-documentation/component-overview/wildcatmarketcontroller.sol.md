# WildcatMarketController.sol

A `WildcatMarketController` contract deploys markets and manages their configurable parameters (APR, reserve ratio) and maintains set of approved lenders.

#### archController

```solidity
 IWildcatArchController public immutable archController;
```



#### controllerFactory

```solidity
 IWildcatMarketControllerFactory public immutable controllerFactory;
```



#### borrower

```solidity
 address public immutable borrower;
```



#### sentinel

```solidity
 address public immutable sentinel;
```



#### marketInitCodeStorage

```solidity
 address public immutable marketInitCodeStorage;
```



#### marketInitCodeHash

<pre class="language-solidity"><code class="lang-solidity"><strong> uint256 public immutable marketInitCodeHash;
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
   function updateLenderAuthorization(address lender, address[] memory markets)
     external;
```



#### isControlledMarket

```solidity
 function isControlledMarket(address market)
   external view returns (bool);
```



#### getControlledMarkets

```solidity
 function getControlledMarkets()
   external view returns (address[] memory);
   
 function getControlledMarkets(
    uint256 start,
    uint256 end
  ) external view returns (address[] memory arr);
```



#### getControlledMarketsCount

<pre class="language-solidity"><code class="lang-solidity"><strong> function getControlledMarketsCount()
</strong><strong>   external view returns (uint256);
</strong></code></pre>



#### computeMarketAddress

```solidity
 function computeMarketAddress(
    address asset,
    string memory namePrefix,
    string memory symbolPrefix
  ) external view returns (address);
```



#### getMarketParameters

<pre class="language-solidity"><code class="lang-solidity"><strong> function getMarketParameters()
</strong>   external view returns (MarketParameters memory parameters);
</code></pre>



#### deployMarket

```solidity
 function deployMarket(
    address asset,
    string memory namePrefix,
    string memory symbolPrefix,
    uint128 maxTotalSupply,
    uint16 annualInterestBips,
    uint16 delinquencyFeeBips,
    uint32 withdrawalBatchDuration,
    uint16 reserveRatioBips,
    uint32 delinquencyGracePeriod
  ) external returns (address market);
```



#### getParameterConstraints

```solidity
 function getParameterConstraints()
   external view returns (MarketParameterConstraints memory constraints);
```



#### setAnnualInterestBips

```solidity
 function setAnnualInterestBips(
    address market,
    uint16 annualInterestBips
  ) external virtual onlyBorrower onlyControlledMarket(market);
```



#### resetReserveRatio

```solidity
 function resetReserveRatio(address market)
   external virtual;
```

