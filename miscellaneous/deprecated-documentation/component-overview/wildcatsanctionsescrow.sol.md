# WildcatSanctionsEscrow.sol

A `WildcatSanctionsEscrow` contract holds assets for a particular account until it is removed from the Chainalysis sanctions list or until the borrower overrides the account's sanction status.

#### sentinel

```solidity
 address public immutable override sentinel;
```

#### borrower

```solidity
 address public immutable override borrower;
```

#### account

```solidity
 address public immutable override account;
```

#### balance

```solidity
 function balance()
   public view override returns (uint256);
```

#### canReleaseEscrow

```solidity
 function canReleaseEscrow()
   public view override returns (bool);
```

#### escrowedAsset

```solidity
 function escrowedAsset()
   public view override returns (address, uint256);
```

#### releaseEscrow

<pre class="language-solidity"><code class="lang-solidity"><strong> function releaseEscrow()
</strong><strong>   public override;
</strong></code></pre>

