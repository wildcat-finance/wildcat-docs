# WildcatSanctionsSentinel.sol

The `WildcatSanctionsSentinel` contract interfaces with Chainalysis, allows borrowers to override lenders' sanction statuses and deploys escrows.&#x20;

#### WildcatSanctionsEscrowInitcodeHash

```solidity
 bytes32 public constant override WildcatSanctionsEscrowInitcodeHash;
```



#### chainalysisSanctionsList

```solidity
 address public immutable override chainalysisSanctionsList;
```



#### archController

```solidity
 address public immutable override archController;
```



#### tmpEscrowParams

```solidity
 TmpEscrowParams public override tmpEscrowParams;
```



#### sanctionOverrides

```solidity
 mapping(address borrower =>
           mapping(address account => bool sanctionOverride))
   public override sanctionOverrides;
```



#### isSanctioned

```solidity
 function isSanctioned(address borrower, address account)
   public view override returns (bool);
```



#### overrideSanction

```solidity
 function overrideSanction(address account)
   public override;
```

Yes, anyone can 'file an override' because it's a public function - no, it doesn't work for the purpose of releasing assets from an escrow contract unless `msg.sender` is a borrower for a market that invoked `nukeFromOrbit`.

Don't waste the gas, this isn't the gotcha you're thinking of.

#### removeSanctionOverride

```solidity
 function removeSanctionOverride(address account)
   public override;
```

See above.

#### getEscrowAddress

```solidity
 function getEscrowAddress(
    address borrower,
    address account,
    address asset
  ) public view override returns (address escrowAddress);
```



#### createEscrow

```solidity
 function createEscrow(
    address borrower,
    address account,
    address asset
  ) public override returns (address escrowContract);
```



