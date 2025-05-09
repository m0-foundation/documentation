# IProtocol
[Git Source](https://github.com/MZero-Labs/protocol/blob/45d6176ce6231b36efc0c52a2961774481e32ec1/src/interfaces/IProtocol.sol)

**Inherits:**
[IContinuousIndexing](/src/interfaces/IContinuousIndexing.sol/interface.IContinuousIndexing.md)


## Functions
### updateCollateral

\
|                                          External Interactive Functions                                          |
\*****************************************************************************************************************

Updates collateral for minters


```solidity
function updateCollateral(
    uint256 collateral,
    uint256[] calldata retrievalIds,
    bytes32 metadataHash,
    address[] calldata validators,
    uint256[] calldata timestamps,
    bytes[] calldata signatures
) external returns (uint256 minTimestamp_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`collateral`|`uint256`|The amount of collateral|
|`retrievalIds`|`uint256[]`|The list of active proposeRetrieval requests to close|
|`metadataHash`|`bytes32`|The hash of metadata of the collateral update, reserved for future informational use|
|`validators`|`address[]`|The list of validators|
|`timestamps`|`uint256[]`|The list of timestamps of validators' signatures|
|`signatures`|`bytes[]`|The list of signatures|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`minTimestamp_`|`uint256`|The minimum timestamp of all validators' signatures|


### proposeRetrieval

Proposes retrieval of minter's offchain collateral


```solidity
function proposeRetrieval(uint256 collateral) external returns (uint256 retrievalId);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`collateral`|`uint256`|The amount of collateral to retrieve|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`retrievalId`|`uint256`|The unique id of created retrieval proposal|


### proposeMint

Proposes minting of M tokens


```solidity
function proposeMint(uint256 amount, address destination) external returns (uint256 mintId);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`amount`|`uint256`|The amount of M tokens to mint|
|`destination`|`address`|The address to mint to|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`mintId`|`uint256`|The unique id of created mint proposal|


### mintM

Executes minting of M tokens


```solidity
function mintM(uint256 mintId) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`mintId`|`uint256`|The id of outstanding mint proposal for minter|


### burnM

Burns M tokens

*If the amount to burn is greater than minter's outstandingValue including penalties, burn all outstandingValue*


```solidity
function burnM(address minter, uint256 amount) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`minter`|`address`|The address of the minter to burn M tokens for|
|`amount`|`uint256`|The max amount of M tokens to burn|


### cancelMint

Cancels minting request for selected minter by the validator


```solidity
function cancelMint(address minter, uint256 mintId) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`minter`|`address`|The address of the minter to cancelMint minting request for|
|`mintId`|`uint256`|The id of outstanding mint request|


### freezeMinter

Freezes minter


```solidity
function freezeMinter(address minter) external returns (uint256 frozenUntil_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`minter`|`address`|The address of the minter to freeze|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`frozenUntil_`|`uint256`|The timestamp until which minter is frozen|


### activateMinter

Activate an approved minter.

*MUST revert if `minter` is not recorded as an approved minter in SPOG Registrar.*

*SHOULD revert if the minter is already active.*


```solidity
function activateMinter(address minter) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`minter`|`address`|The address of the minter to activate|


### deactivateMinter

Deactivates an active minter.

*MUST revert if the minter is not an approved minter.*

*SHOULD revert if the minter is not active.*


```solidity
function deactivateMinter(address minter) external returns (uint256 inactiveOwedM);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`minter`|`address`|The address of the minter to deactivate|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`inactiveOwedM`|`uint256`|The inactive owed M for the deactivated minter|


### ONE

\
|                                           External View/Pure Functions                                           |
\*****************************************************************************************************************

Descaler for variables in basis points. Effectively, 100% in basis points.


```solidity
function ONE() external pure returns (uint256);
```

### UPDATE_COLLATERAL_TYPEHASH

The EIP-712 typehash for the `updateCollateral` method.


```solidity
function UPDATE_COLLATERAL_TYPEHASH() external pure returns (bytes32);
```

### mToken

The address of M token


```solidity
function mToken() external view returns (address);
```

### spogRegistrar

The address of SPOG Registrar contract.


```solidity
function spogRegistrar() external view returns (address);
```

### spogVault

The address of SPOG Vault contract.


```solidity
function spogVault() external view returns (address);
```

### minterRate

The last saved value of Minter rate.


```solidity
function minterRate() external view returns (uint256);
```

### totalActiveOwedM

The total owed M for all active minters.


```solidity
function totalActiveOwedM() external view returns (uint256);
```

### totalInactiveOwedM

The total owed M for all inactive minters.


```solidity
function totalInactiveOwedM() external view returns (uint256);
```

### totalOwedM

The total owed M for all minters.


```solidity
function totalOwedM() external view returns (uint256);
```

### excessActiveOwedM

The difference between total active owed M and M token total supply.


```solidity
function excessActiveOwedM() external view returns (uint256);
```

### activeOwedMOf

The active owed M of minter.


```solidity
function activeOwedMOf(address minter) external view returns (uint256);
```

### maxAllowedActiveOwedMOf

The max allowed active owed M of minter taking into account collateral amount and retrieval proposals.


```solidity
function maxAllowedActiveOwedMOf(address minter_) external view returns (uint256);
```

### inactiveOwedMOf

The inactive owed M of deactivated minter.


```solidity
function inactiveOwedMOf(address minter) external view returns (uint256);
```

### collateralOf

The collateral of a given minter.


```solidity
function collateralOf(address minter) external view returns (uint256);
```

### collateralUpdateOf

The timestamp of the last collateral update of minter.


```solidity
function collateralUpdateOf(address minter) external view returns (uint256);
```

### collateralUpdateDeadlineOf

The timestamp of the deadline for the next collateral update of minter.


```solidity
function collateralUpdateDeadlineOf(address minter) external view returns (uint256);
```

### lastCollateralUpdateIntervalOf

The length of the last collateral interval for minter in case SPOG changes this parameter.


```solidity
function lastCollateralUpdateIntervalOf(address minter) external view returns (uint256);
```

### penalizedUntilOf

The timestamp until which minter is already penalized for missed collateral updates.


```solidity
function penalizedUntilOf(address minter) external view returns (uint256);
```

### getPenaltyForMissedCollateralUpdates

The penalty for missed collateral updates. Penalized once per missed interval.


```solidity
function getPenaltyForMissedCollateralUpdates(address minter) external view returns (uint256);
```

### mintProposalOf

The mint proposal of minters, only 1 active proposal per minter


```solidity
function mintProposalOf(address minter)
    external
    view
    returns (uint256 mintId, address destination, uint256 amount, uint256 createdAt);
```

### pendingCollateralRetrievalOf

The minter's proposeRetrieval proposal amount


```solidity
function pendingCollateralRetrievalOf(address minter, uint256 retrievalId) external view returns (uint256 collateral);
```

### totalPendingCollateralRetrievalsOf

The total amount of active proposeRetrieval requests per minter


```solidity
function totalPendingCollateralRetrievalsOf(address minter) external view returns (uint256);
```

### unfrozenTimeOf

The timestamp when minter becomes unfrozen after being frozen by validator.


```solidity
function unfrozenTimeOf(address minter) external view returns (uint256);
```

### isActiveMinter

Checks if minter was activated after approval by SPOG


```solidity
function isActiveMinter(address minter) external view returns (bool);
```

### isMinterApprovedBySPOG

Checks if minter was approved by SPOG


```solidity
function isMinterApprovedBySPOG(address minter_) external view returns (bool);
```

### isValidatorApprovedBySPOG

Checks if validator was approved by SPOG


```solidity
function isValidatorApprovedBySPOG(address validator_) external view returns (bool);
```

### mintDelay

The delay between mint proposal creation and its earliest execution.


```solidity
function mintDelay() external view returns (uint256);
```

### mintTTL

The time while mint request can still be processed before it is considered expired.


```solidity
function mintTTL() external view returns (uint256);
```

### minterFreezeTime

The freeze time for minter.


```solidity
function minterFreezeTime() external view returns (uint256);
```

### mintRatio

The allowed activeOwedM to collateral ratio.


```solidity
function mintRatio() external view returns (uint256);
```

### penaltyRate

The % that defines penalty amount for missed collateral updates or excessive owedM value


```solidity
function penaltyRate() external view returns (uint256);
```

### rateModel

The smart contract that defines the minter rate.


```solidity
function rateModel() external view returns (address);
```

### updateCollateralInterval

The interval that defines the required frequency of collateral updates.


```solidity
function updateCollateralInterval() external view returns (uint256);
```

### updateCollateralValidatorThreshold

The number of signatures required for successful collateral update.


```solidity
function updateCollateralValidatorThreshold() external view returns (uint256);
```

## Events
### CollateralUpdated
\
|                                                      Events                                                      |
\*****************************************************************************************************************

Emitted when a minter's collateral is updated.


```solidity
event CollateralUpdated(
    address indexed minter,
    uint256 collateral,
    uint256[] indexed retrievalIds,
    bytes32 indexed metadataHash,
    uint256 timestamp
);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`minter`|`address`|Address of the minter|
|`collateral`|`uint256`|The latest amount of collateral|
|`retrievalIds`|`uint256[]`|The list of outstanding proposeRetrieval requests to close|
|`metadataHash`|`bytes32`|The hash of metadata of the collateral update, reserved for future informational use|
|`timestamp`|`uint256`|The timestamp of the collateral update, minimum of given validators' signatures|

### MinterActivated
Emitted when a minter is activated.


```solidity
event MinterActivated(address indexed minter, address indexed caller);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`minter`|`address`|Address of the minter that was activated|
|`caller`|`address`|Address who called the function|

### MinterDeactivated
Emitted when a minter is deactivated.


```solidity
event MinterDeactivated(address indexed minter, uint256 inactiveOwedM, address indexed caller);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`minter`|`address`|Address of the minter that was deactivated|
|`inactiveOwedM`|`uint256`|Amount of M tokens owed by the minter|
|`caller`|`address`|Address who called the function|

### MinterFrozen
Emitted when a minter is frozen.


```solidity
event MinterFrozen(address indexed minter, uint256 frozenUntil);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`minter`|`address`|Address of the minter that was frozen|
|`frozenUntil`|`uint256`|Timestamp until the minter is frozen|

### MintProposed
Emitted when mint proposal is created.


```solidity
event MintProposed(uint256 indexed mintId, address indexed minter, uint256 amount, address indexed destination);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`mintId`|`uint256`|The id of mint proposal|
|`minter`|`address`|The address of the minter|
|`amount`|`uint256`|The amount of M tokens to mint|
|`destination`|`address`|The address to mint to|

### MintCanceled
Emitted when mint proposal is canceled.


```solidity
event MintCanceled(uint256 indexed mintId, address indexed canceller);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`mintId`|`uint256`|The id of mint proposal|
|`canceller`|`address`|The address of validator who cancelled the mint proposal|

### MintExecuted
Emitted when mint proposal is executed.


```solidity
event MintExecuted(uint256 indexed mintId);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`mintId`|`uint256`|The id of executed mint proposal|

### BurnExecuted
Emitted when M tokens are burned and minter's owed M balance decreased.


```solidity
event BurnExecuted(address indexed minter, uint256 amount, address indexed payer);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`minter`|`address`|The address of the minter|
|`amount`|`uint256`|The amount of M tokens to burn|
|`payer`|`address`|The address of the payer|

### PenaltyImposed
Emitted when penalty is imposed on minter.


```solidity
event PenaltyImposed(address indexed minter, uint256 amount);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`minter`|`address`|The address of the minter|
|`amount`|`uint256`|The amount of penalty charge|

### RetrievalCreated
Emitted when collateral retrieval proposal is created.


```solidity
event RetrievalCreated(uint256 indexed retrievalId, address indexed minter, uint256 amount);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`retrievalId`|`uint256`|The id of retrieval proposal|
|`minter`|`address`|The address of the minter|
|`amount`|`uint256`|The amount of collateral to retrieve|

## Errors
### AlreadyActiveMinter
\
|                                                      Errors                                                      |
\*****************************************************************************************************************

Emitted when calling `activeMinter` with an already active minter.


```solidity
error AlreadyActiveMinter();
```

### ExpiredMintProposal
Emitted when calling `mintM` with a proposal that was created more than `mintDelay + mintTTL` time ago.


```solidity
error ExpiredMintProposal(uint256 deadline);
```

### FrozenMinter
Emitted when calling `mintM` or `proposeMint` by a minter who was frozen by validator.


```solidity
error FrozenMinter();
```

### FutureTimestamp
Emitted when calling `updateCollateral` if validator timestamp is in the future.


```solidity
error FutureTimestamp();
```

### InvalidMintProposal
Emitted when calling `cancelMint` or `mintM` with invalid `mintId`.


```solidity
error InvalidMintProposal();
```

### InvalidSignatureOrder
Emitted when calling `updateCollateral` if `validators` addresses are not ordered in ascending order.


```solidity
error InvalidSignatureOrder();
```

### InactiveMinter
Emitted when calling `deactivateMinter` with an inactive minter.


```solidity
error InactiveMinter();
```

### NotApprovedMinter
Emitted when calling `activateMinter` if minter was not approved by SPOG.


```solidity
error NotApprovedMinter();
```

### NotApprovedValidator
Emitted when calling `cancelMint` or `freezeMinter` if validator was not approved by SPOG.


```solidity
error NotApprovedValidator();
```

### NotEnoughValidSignatures
Emitted when calling `updateCollateral` if `validatorThreshold` of signatures was not reached.


```solidity
error NotEnoughValidSignatures(uint256 validSignatures, uint256 requiredThreshold);
```

### PendingMintProposal
Emitted when calling `mintM` if `mintDelay` time has not passed yet.


```solidity
error PendingMintProposal(uint256 activeTimestamp);
```

### SignatureArrayLengthsMismatch
Emitted when calling `updateCollateral`
If `validators`, `signatures`, `timestamps` lengths do not match.


```solidity
error SignatureArrayLengthsMismatch();
```

### StaleCollateralUpdate
Emitted when calling `updateCollateral` if protocol has more fresh collateral update.


```solidity
error StaleCollateralUpdate(uint256 newTimestamp, uint256 lastCollateralUpdate);
```

### StillApprovedMinter
Emitted when calling `deactivateMinter` with a minter still approved in SPOG Registrar.


```solidity
error StillApprovedMinter();
```

### Undercollateralized
Emitted when calling `proposeMint`, `mintM`, `proposeRetrieval`
If minter position becomes undercollateralized.


```solidity
error Undercollateralized(uint256 activeOwedM, uint256 maxAllowedOwedM);
```

### ZeroMToken
Emitted in constructor if M Token is 0x0.


```solidity
error ZeroMToken();
```

### ZeroSpogRegistrar
Emitted in constructor if SPOG Registrar is 0x0.


```solidity
error ZeroSpogRegistrar();
```

### ZeroSpogVault
Emitted in constructor if SPOG Distribution Vault is set to 0x0 in SPOG Registrar.


```solidity
error ZeroSpogVault();
```

