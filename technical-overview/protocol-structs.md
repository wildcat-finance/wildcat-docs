# Protocol Structs

This page includes details of the structs used within Wildcat V2.

Note: you can generate this yourself via the `calculate_structs.py` Python script in the `/scripts` directory of the repository.

## File: /src/HooksFactory.sol

### &#x20; Struct: TmpMarketParameterStorage

&#x20;   address borrower

&#x20;   address asset

&#x20;   address feeRecipient

&#x20;   uint16 protocolFeeBips

&#x20;   uint128 maxTotalSupply

&#x20;   uint16 annualInterestBips

&#x20;   uint16 delinquencyFeeBips

&#x20;   uint32 withdrawalBatchDuration

&#x20;   uint16 reserveRatioBips

&#x20;   uint32 delinquencyGracePeriod

&#x20;   bytes32 packedNameWord0

&#x20;   bytes32 packedNameWord1

&#x20;   bytes32 packedSymbolWord0

&#x20;   bytes32 packedSymbolWord1

&#x20;   uint8 decimals

&#x20;   HooksConfig hooks // note: type HooksConfig is uint256;\


## File: /src/IHooksFactory.sol

### &#x20; Struct: HooksTemplate

&#x20;   /// @dev Asset used to pay origination fee

&#x20; address originationFeeAsset

&#x20;   /// @dev Amount of \`originationFeeAsset\` paid to deploy a new market using

&#x20; ///      an instance of this template.

&#x20; uint80 originationFeeAmount

&#x20;   /// @dev Basis points paid on interest for markets deployed using hooks

&#x20; ///      based on this template

&#x20; uint16 protocolFeeBips

&#x20;   /// @dev Whether the template exists

&#x20; bool exists

&#x20;   /// @dev Whether the template is enabled

&#x20; bool enabled

&#x20;   /// @dev Index of the template address in the array of hooks templates

&#x20; uint24 index

&#x20;   /// @dev Address to pay origination and interest fees

&#x20; address feeRecipient

&#x20;   /// @dev Name of the template

&#x20; string name



## File: /src/types/LenderStatus.sol

### &#x20; Struct: LenderStatus

&#x20;   bool isBlockedFromDeposits

&#x20;   bool hasEverDeposited

&#x20;   address lastProvider

&#x20;   bool canRefresh

&#x20;   uint32 lastApprovalTimestamp\


## File: /src/access/MarketConstraintHooks.sol

### &#x20; Struct: TemporaryReserveRatio

&#x20;   uint16 originalAnnualInterestBips

&#x20;   uint16 originalReserveRatioBips

&#x20;   uint32 expiry



## File: /src/libraries/MarketState.sol

### &#x20; Struct: MarketState

&#x20;   bool isClosed

&#x20;   uint128 maxTotalSupply

&#x20;   uint128 accruedProtocolFees

&#x20;   // Underlying assets reserved for withdrawals which have been paid

&#x20; // by the borrower but not yet executed.

&#x20; uint128 normalizedUnclaimedWithdrawals

&#x20;   // Scaled token supply (divided by scaleFactor)

&#x20; uint104 scaledTotalSupply

&#x20;   // Scaled token amount in withdrawal batches that have not been

&#x20; // paid by borrower yet.

&#x20; uint104 scaledPendingWithdrawals

&#x20;   uint32 pendingWithdrawalExpiry

&#x20;   // Whether market is currently delinquent (liquidity under requirement)

&#x20; bool isDelinquent

&#x20;   // Seconds borrower has been delinquent

&#x20; uint32 timeDelinquent

&#x20;   // Annual interest rate accrued to lenders, in basis points

&#x20; uint16 annualInterestBips

&#x20;   // Percentage of outstanding balance that must be held in liquid reserves

&#x20; uint16 reserveRatioBips

&#x20;   // Ratio between internal balances and underlying token amounts

&#x20; uint112 scaleFactor

&#x20; uint32 lastInterestAccruedTimestamp



### &#x20; Struct: Account

&#x20;   uint104 scaledBalance



## File: /src/libraries/Withdrawal.sol

### &#x20; Struct: WithdrawalBatch

&#x20;   // Total scaled amount of tokens to be withdrawn

&#x20; uint104 scaledTotalAmount

&#x20;   // Amount of scaled tokens that have been paid by borrower

&#x20; uint104 scaledAmountBurned

&#x20;   // Amount of normalized tokens that have been paid by borrower

&#x20; uint128 normalizedAmountPaid



### &#x20; Struct: AccountWithdrawalStatus

&#x20;   uint104 scaledAmount

&#x20;   uint128 normalizedAmountWithdrawn



### &#x20; Struct: WithdrawalData

&#x20;   FIFOQueue unpaidBatches

&#x20;   mapping(uint32 => WithdrawalBatch) batches

&#x20;   mapping(uint256 => mapping(address => AccountWithdrawalStatus)) accountStatuses



## File: /src/libraries/FIFOQueue.sol

### &#x20; Struct: FIFOQueue

&#x20;   uint128 startIndex

&#x20;   uint128 nextIndex

&#x20;   mapping(uint256 => uint32) data



## File: /src/spherex/ISphereXEngine.sol

### &#x20; Struct: ModifierLocals

&#x20;   bytes32\[] storageSlots

&#x20;   bytes32\[] valuesBefore

&#x20;   uint256 gas

&#x20;   address engine



## File: /src/interfaces/IWildcatSanctionsSentinel.sol

### &#x20; Struct: TmpEscrowParams

&#x20;   address borrower

&#x20;   address account

&#x20;   address asset\


## File: /src/interfaces/WildcatStructsAndEnums.sol

### &#x20; Struct: MarketParameters

&#x20;   address asset

&#x20;   uint8 decimals

&#x20;   bytes32 packedNameWord0

&#x20;   bytes32 packedNameWord1

&#x20;   bytes32 packedSymbolWord0

&#x20;   bytes32 packedSymbolWord1

&#x20;   address borrower

&#x20;   address feeRecipient

&#x20;   address sentinel

&#x20;   uint128 maxTotalSupply

&#x20;   uint16 protocolFeeBips

&#x20;   uint16 annualInterestBips

&#x20;   uint16 delinquencyFeeBips

&#x20;   uint32 withdrawalBatchDuration

&#x20;   uint16 reserveRatioBips

&#x20;   uint32 delinquencyGracePeriod

&#x20;   address archController

&#x20;   address sphereXEngine

&#x20;   HooksConfig hooks\


### &#x20; Struct: DeployMarketInputs

&#x20;   address asset

&#x20;   string namePrefix

&#x20;   string symbolPrefix

&#x20;   uint128 maxTotalSupply

&#x20;   uint16 annualInterestBips

&#x20;   uint16 delinquencyFeeBips

&#x20;   uint32 withdrawalBatchDuration

&#x20;   uint16 reserveRatioBips

&#x20;   uint32 delinquencyGracePeriod

&#x20;   HooksConfig hooks



### &#x20; Struct: MarketControllerParameters

&#x20;   address archController

&#x20;   address borrower

&#x20;   address sentinel

&#x20;   address marketInitCodeStorage

&#x20;   uint256 marketInitCodeHash

&#x20;   uint32 minimumDelinquencyGracePeriod

&#x20;   uint32 maximumDelinquencyGracePeriod

&#x20;   uint16 minimumReserveRatioBips

&#x20;   uint16 maximumReserveRatioBips

&#x20;   uint16 minimumDelinquencyFeeBips

&#x20;   uint16 maximumDelinquencyFeeBips

&#x20;   uint32 minimumWithdrawalBatchDuration

&#x20;   uint32 maximumWithdrawalBatchDuration

&#x20;   uint16 minimumAnnualInterestBips

&#x20;   uint16 maximumAnnualInterestBips

&#x20;   address sphereXEngine



### &#x20; Struct: ProtocolFeeConfiguration

&#x20;   address feeRecipient

&#x20;   address originationFeeAsset

&#x20;   uint80 originationFeeAmount

&#x20;   uint16 protocolFeeBips



### &#x20; Struct: MarketParameterConstraints

&#x20;   uint32 minimumDelinquencyGracePeriod

&#x20;   uint32 maximumDelinquencyGracePeriod

&#x20;   uint16 minimumReserveRatioBips

&#x20;   uint16 maximumReserveRatioBips

&#x20;   uint16 minimumDelinquencyFeeBips

&#x20;   uint16 maximumDelinquencyFeeBips

&#x20;   uint32 minimumWithdrawalBatchDuration

&#x20;   uint32 maximumWithdrawalBatchDuration

&#x20;   uint16 minimumAnnualInterestBips

&#x20;   uint16 maximumAnnualInterestBips
