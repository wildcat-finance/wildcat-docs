# AccessControlHooks.sol

## Functions:

addRoleProvider(address,uint32) 0xea5b13bd

blockFromDeposits(address) 0x064ed53b

borrower() 0x7df1f1b9

config() 0x79502c55

factory() 0xc45a0155

getHookedMarket(address) 0x2ccf4667

getLenderStatus(address) 0x22a4a19f

getParameterConstraints() 0xa11ef067

getPreviousLenderStatus(address) 0xb037096d

getPullProviders() 0x8f8ef419

getRoleProvider(address) 0xbfd269be

grantRole(address,uint32) 0x6b2b369b

grantRoles(address\[],uint32\[]) 0x9d2a76fe

isKnownLenderOnMarket(address,address) 0xa9ff2dbf

onBorrow(uint256,(bool,uint128,uint128,uint128,uint104,uint104,uint32,bool,uint32,uint16,uint16,uint16,uint112,uint32),bytes) 0xb1cfda0d

onCloseMarket((bool,uint128,uint128,uint128,uint104,uint104,uint32,bool,uint32,uint16,uint16,uint16,uint112,uint32),bytes) 0x9ecc64e6

onCreateMarket(address,address,(address,string,string,uint128,uint16,uint16,uint32,uint16,uint32,uint256),bytes) 0x28fd0307

onDeposit(address,uint256,(bool,uint128,uint128,uint128,uint104,uint104,uint32,bool,uint32,uint16,uint16,uint16,uint112,uint32),bytes) 0x5aeb713f

onExecuteWithdrawal(address,uint128,(bool,uint128,uint128,uint128,uint104,uint104,uint32,bool,uint32,uint16,uint16,uint16,uint112,uint32),bytes) 0x2970403d

onNukeFromOrbit(address,(bool,uint128,uint128,uint128,uint104,uint104,uint32,bool,uint32,uint16,uint16,uint16,uint112,uint32),bytes) 0x8b3ce9b3

onQueueWithdrawal(address,uint32,uint256,(bool,uint128,uint128,uint128,uint104,uint104,uint32,bool,uint32,uint16,uint16,uint16,uint112,uint32),bytes) 0x3521cccc

onRepay(uint256,(bool,uint128,uint128,uint128,uint104,uint104,uint32,bool,uint32,uint16,uint16,uint16,uint112,uint32),bytes) 0x83d9e1eb

onSetAnnualInterestAndReserveRatioBips(uint16,uint16,(bool,uint128,uint128,uint128,uint104,uint104,uint32,bool,uint32,uint16,uint16,uint16,uint112,uint32),bytes) 0xcc452642

onSetMaxTotalSupply(uint256,(bool,uint128,uint128,uint128,uint104,uint104,uint32,bool,uint32,uint16,uint16,uint16,uint112,uint32),bytes) 0x849da129

onSetProtocolFeeBips(uint16,(bool,uint128,uint128,uint128,uint104,uint104,uint32,bool,uint32,uint16,uint16,uint16,uint112,uint32),bytes) 0x03473d8d

onTransfer(address,address,address,uint256,(bool,uint128,uint128,uint128,uint104,uint104,uint32,bool,uint32,uint16,uint16,uint16,uint112,uint32),bytes) 0xa018f90e

removeRoleProvider(address) 0x8adfe0f8

revokeRole(address) 0x80e52e3f

setMinimumDeposit(address,uint128) 0x1c4b3694

temporaryExcessReserveRatio(address) 0xfeb368e2

unblockFromDeposits(address) 0xaa948689

version() 0x54fd4d50

## Events:

AccountAccessGranted(address,address,uint32) 0xa04eb478

AccountAccessRevoked(address) 0x47695aa9

AccountBlockedFromDeposits(address) 0x25b0d183

AccountMadeFirstDeposit(address) 0x69da6af3

AccountUnblockedFromDeposits(address) 0x7201a401

MinimumDepositUpdated(address,uint128) 0x4e39f532

RoleProviderAdded(address,uint32,uint24) 0xbe2909d8

RoleProviderRemoved(address,uint24) 0x096f563e

RoleProviderUpdated(address,uint32,uint24) 0x0c641c0a

TemporaryExcessReserveRatioActivated(address,uint256,uint256,uint256) 0x16f9a191

TemporaryExcessReserveRatioCanceled(address) 0x2045c970

TemporaryExcessReserveRatioExpired(address) 0x145c143a

TemporaryExcessReserveRatioUpdated(address,uint256,uint256,uint256) 0xf813e17e
