# IMinterGateway
[Git Source](https://github.com/MZero-Labs/protocol/blob/3382fb7336bbc7276e0c3f51da451c9fa6e0016f/src/interfaces/IMinterGateway.sol)

**Inherits:**
[IContinuousIndexing](/src/interfaces/IContinuousIndexing.sol/interface.IContinuousIndexing.md), IERC712

**Author:**
M^0 Labs


## Functions
### updateCollateral

Updates collateral for minters


```solidity
function updateCollateral(
    uint256 collateral,
    uint256[] calldata retrievalIds,
    bytes32 metadataHash,
    address[] calldata validators,
    uint256[] calldata timestamps,
    bytes[] calldata signatures
) external returns (uint40 minTimestamp);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`collateral`|`uint256`|  The amount of collateral|
|`retrievalIds`|`uint256[]`|The list of active proposeRetrieval requests to close|
|`metadataHash`|`bytes32`|The hash of metadata of the collateral update, reserved for future informational use|
|`validators`|`address[]`|  The list of validators|
|`timestamps`|`uint256[]`|  The list of timestamps of validators' signatures|
|`signatures`|`bytes[]`|  The list of signatures|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`minTimestamp`|`uint40`|The minimum timestamp of all validators' signatures|


### proposeRetrieval

Proposes retrieval of minter's offchain collateral


```solidity
function proposeRetrieval(uint256 collateral) external returns (uint48 retrievalId);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`collateral`|`uint256`| The amount of collateral to retrieve|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`retrievalId`|`uint48`|The unique id of created retrieval proposal|


### proposeMint

Proposes minting of M tokens


```solidity
function proposeMint(uint256 amount, address destination) external returns (uint48 mintId);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`amount`|`uint256`|     The amount of M tokens to mint|
|`destination`|`address`|The address to mint to|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`mintId`|`uint48`|     The unique id of created mint proposal|


### mintM

Executes minting of M tokens


```solidity
function mintM(uint256 mintId) external returns (uint112 principalAmount, uint240 amount);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`mintId`|`uint256`|         The id of outstanding mint proposal for minter|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`principalAmount`|`uint112`|The amount of principal of owed M minted.|
|`amount`|`uint240`|         The amount of M tokens minted.|


### burnM

Burns M tokens

*If the amount to burn is greater than the minter's owedM including penalties, burn all up to owedM.*


```solidity
function burnM(address minter, uint256 maxAmount) external returns (uint112 principalAmount, uint240 amount);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`minter`|`address`|         The address of the minter to burn M tokens for.|
|`maxAmount`|`uint256`|      The max amount of M tokens to burn.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`principalAmount`|`uint112`|The amount of principal of owed M burned.|
|`amount`|`uint240`|         The amount of M tokens burned.|


### burnM

Burns M tokens

*If the amount to burn is greater than the minter's owedM including penalties, burn all up to owedM.*


```solidity
function burnM(address minter, uint256 maxPrincipalAmount, uint256 maxAmount)
    external
    returns (uint112 principalAmount, uint240 amount);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`minter`|`address`|            The address of the minter to burn M tokens for.|
|`maxPrincipalAmount`|`uint256`|The max amount of principal of owed M to burn.|
|`maxAmount`|`uint256`|         The max amount of M tokens to burn.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`principalAmount`|`uint112`|   The amount of principal of owed M burned.|
|`amount`|`uint240`|            The amount of M tokens burned.|


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
function freezeMinter(address minter) external returns (uint40 frozenUntil);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`minter`|`address`|     The address of the minter to freeze|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`frozenUntil`|`uint40`|The timestamp until which minter is frozen|


### activateMinter

Activate an approved minter.

*MUST revert if `minter` is not recorded as an approved minter in TTG Registrar.*

*MUST revert if `minter` has been deactivated.*


```solidity
function activateMinter(address minter) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`minter`|`address`|The address of the minter to activate|


### deactivateMinter

Deactivates an active minter.

*MUST revert if the minter is still approved.*

*MUST revert if the minter is not active.*


```solidity
function deactivateMinter(address minter) external returns (uint240 inactiveOwedM);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`minter`|`address`|       The address of the minter to deactivate.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`inactiveOwedM`|`uint240`|The inactive owed M for the deactivated minter.|


### mToken

The address of M token


```solidity
function mToken() external view returns (address);
```

### ttgRegistrar

The address of TTG Registrar contract.


```solidity
function ttgRegistrar() external view returns (address);
```

### ttgVault

The address of TTG Vault contract.


```solidity
function ttgVault() external view returns (address);
```

### minterRate

The last saved value of Minter rate.


```solidity
function minterRate() external view returns (uint32);
```

### principalOfTotalActiveOwedM

The principal of total owed M for all active minters.


```solidity
function principalOfTotalActiveOwedM() external view returns (uint112);
```

### totalActiveOwedM

The total owed M for all active minters.


```solidity
function totalActiveOwedM() external view returns (uint240);
```

### totalInactiveOwedM

The total owed M for all inactive minters.


```solidity
function totalInactiveOwedM() external view returns (uint240);
```

### totalOwedM

The total owed M for all minters.


```solidity
function totalOwedM() external view returns (uint240);
```

### excessOwedM

The difference between total owed M and M token total supply.


```solidity
function excessOwedM() external view returns (uint240);
```

### principalOfActiveOwedMOf

The principal of active owed M of minter.


```solidity
function principalOfActiveOwedMOf(address minter_) external view returns (uint112);
```

### activeOwedMOf

The active owed M of minter.


```solidity
function activeOwedMOf(address minter) external view returns (uint240);
```

### maxAllowedActiveOwedMOf

The max allowed active owed M of minter taking into account collateral amount and retrieval proposals.

*This is the only present value that requires a `uint256` since it is the result of a multiplication
between a `uint240` and a value that has a max of `65,000` (the mint ratio).*


```solidity
function maxAllowedActiveOwedMOf(address minter) external view returns (uint256);
```

### inactiveOwedMOf

The inactive owed M of deactivated minter.


```solidity
function inactiveOwedMOf(address minter) external view returns (uint240);
```

### collateralOf

The collateral of a given minter.


```solidity
function collateralOf(address minter) external view returns (uint240);
```

### collateralUpdateTimestampOf

The timestamp of the last collateral update of minter.


```solidity
function collateralUpdateTimestampOf(address minter) external view returns (uint40);
```

### collateralPenaltyDeadlineOf

The timestamp after which an additional penalty for a missed update interval will be charged.


```solidity
function collateralPenaltyDeadlineOf(address minter) external view returns (uint40);
```

### collateralExpiryTimestampOf

The timestamp after which the minter's collateral is assumed to be 0 due to a missed update.


```solidity
function collateralExpiryTimestampOf(address minter) external view returns (uint40);
```

### penalizedUntilOf

The timestamp until which minter is already penalized for missed collateral updates.


```solidity
function penalizedUntilOf(address minter) external view returns (uint40);
```

### getPenaltyForMissedCollateralUpdates

The penalty for missed collateral updates. Penalized once per missed interval.


```solidity
function getPenaltyForMissedCollateralUpdates(address minter) external view returns (uint240);
```

### getUpdateCollateralDigest

Returns the EIP-712 digest for updateCollateral method.


```solidity
function getUpdateCollateralDigest(
    address minter,
    uint256 collateral,
    uint256[] calldata retrievalIds,
    bytes32 metadataHash,
    uint256 timestamp
) external view returns (bytes32);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`minter`|`address`|      The address of the minter.|
|`collateral`|`uint256`|  The amount of collateral.|
|`retrievalIds`|`uint256[]`|The list of outstanding collateral retrieval IDs to resolve.|
|`metadataHash`|`bytes32`|The hash of metadata of the collateral update, reserved for future informational use.|
|`timestamp`|`uint256`|   The timestamp of the collateral update.|


### mintProposalOf

The mint proposal of minters, only 1 active proposal per minter


```solidity
function mintProposalOf(address minter)
    external
    view
    returns (uint48 mintId, uint40 createdAt, address destination, uint240 amount);
```

### pendingCollateralRetrievalOf

The minter's proposeRetrieval proposal amount


```solidity
function pendingCollateralRetrievalOf(address minter, uint256 retrievalId) external view returns (uint240);
```

### totalPendingCollateralRetrievalOf

The total amount of active proposeRetrieval requests per minter


```solidity
function totalPendingCollateralRetrievalOf(address minter) external view returns (uint240);
```

### frozenUntilOf

The timestamp when minter becomes unfrozen after being frozen by validator.


```solidity
function frozenUntilOf(address minter) external view returns (uint40);
```

### isActiveMinter

Checks if minter was activated after approval by TTG


```solidity
function isActiveMinter(address minter) external view returns (bool);
```

### isDeactivatedMinter

Checks if minter was deactivated after removal by TTG


```solidity
function isDeactivatedMinter(address minter) external view returns (bool);
```

### isFrozenMinter

Checks if minter was frozen by validator


```solidity
function isFrozenMinter(address minter) external view returns (bool);
```

### isMinterApproved

Checks if minter was approved by TTG


```solidity
function isMinterApproved(address minter) external view returns (bool);
```

### isValidatorApprovedByTTG

Checks if validator was approved by TTG


```solidity
function isValidatorApprovedByTTG(address validator) external view returns (bool);
```

### mintDelay

The delay between mint proposal creation and its earliest execution.


```solidity
function mintDelay() external view returns (uint32);
```

### mintTTL

The time while mint request can still be processed before it is considered expired.


```solidity
function mintTTL() external view returns (uint32);
```

### minterFreezeTime

The freeze time for minter.


```solidity
function minterFreezeTime() external view returns (uint32);
```

### mintRatio

The allowed activeOwedM to collateral ratio.


```solidity
function mintRatio() external view returns (uint32);
```

### penaltyRate

The % that defines penalty amount for missed collateral updates or excessive owedM value


```solidity
function penaltyRate() external view returns (uint32);
```

### rateModel

The smart contract that defines the minter rate.


```solidity
function rateModel() external view returns (address);
```

### updateCollateralInterval

The interval that defines the required frequency of collateral updates.


```solidity
function updateCollateralInterval() external view returns (uint32);
```

### updateCollateralValidatorThreshold

The number of signatures required for successful collateral update.


```solidity
function updateCollateralValidatorThreshold() external view returns (uint256);
```

### ONE

Descaler for variables in basis points. Effectively, 100% in basis points.


```solidity
function ONE() external pure returns (uint16);
```

### MAX_MINT_RATIO

Mint ratio cap. 650% in basis points.


```solidity
function MAX_MINT_RATIO() external pure returns (uint32);
```

### UPDATE_COLLATERAL_TYPEHASH

The EIP-712 typehash for the `updateCollateral` method.


```solidity
function UPDATE_COLLATERAL_TYPEHASH() external pure returns (bytes32);
```

## Events
### BurnExecuted
Emitted when M tokens are burned and an inactive minter's owed M balance decreased.


```solidity
event BurnExecuted(address indexed minter, uint240 amount, address indexed payer);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`minter`|`address`|The address of the minter.|
|`amount`|`uint240`|The amount of M tokens burned.|
|`payer`|`address`| The address of the payer.|

### BurnExecuted
Emitted when M tokens are burned and an active minter's owed M balance decreased.


```solidity
event BurnExecuted(address indexed minter, uint112 principalAmount, uint240 amount, address indexed payer);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`minter`|`address`|         The address of the minter.|
|`principalAmount`|`uint112`|The principal amount of M tokens burned.|
|`amount`|`uint240`|         The amount of M tokens burned.|
|`payer`|`address`|          The address of the payer.|

### CollateralUpdated
Emitted when a minter's collateral is updated.


```solidity
event CollateralUpdated(
    address indexed minter,
    uint240 collateral,
    uint240 totalResolvedCollateralRetrieval,
    bytes32 indexed metadataHash,
    uint40 timestamp
);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`minter`|`address`|                          Address of the minter|
|`collateral`|`uint240`|                      The latest amount of collateral|
|`totalResolvedCollateralRetrieval`|`uint240`|The total collateral amount of outstanding retrievals resolved.|
|`metadataHash`|`bytes32`|                    The hash of some metadata reserved for future informational use.|
|`timestamp`|`uint40`|                       The timestamp of the collateral update, minimum of given validators' signatures.|

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
event MinterDeactivated(address indexed minter, uint240 inactiveOwedM, address indexed caller);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`minter`|`address`|       Address of the minter that was deactivated.|
|`inactiveOwedM`|`uint240`|Amount of M tokens owed by the minter (in an inactive state).|
|`caller`|`address`|       Address who called the function.|

### MinterFrozen
Emitted when a minter is frozen.


```solidity
event MinterFrozen(address indexed minter, uint40 frozenUntil);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`minter`|`address`|     Address of the minter that was frozen|
|`frozenUntil`|`uint40`|Timestamp until the minter is frozen|

### MintCanceled
Emitted when mint proposal is canceled.


```solidity
event MintCanceled(uint48 indexed mintId, address indexed canceller);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`mintId`|`uint48`|   The id of mint proposal.|
|`canceller`|`address`|The address of validator who cancelled the mint proposal.|

### MintExecuted
Emitted when mint proposal is executed.


```solidity
event MintExecuted(uint48 indexed mintId, uint112 principalAmount, uint240 amount);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`mintId`|`uint48`|         The id of executed mint proposal.|
|`principalAmount`|`uint112`|The principal amount of M tokens minted.|
|`amount`|`uint240`|         The amount of M tokens minted.|

### MintProposed
Emitted when mint proposal is created.


```solidity
event MintProposed(uint48 indexed mintId, address indexed minter, uint240 amount, address indexed destination);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`mintId`|`uint48`|     The id of mint proposal.|
|`minter`|`address`|     The address of the minter.|
|`amount`|`uint240`|     The amount of M tokens to mint.|
|`destination`|`address`|The address to mint to.|

### PenaltyImposed
Emitted when penalty is imposed on minter.


```solidity
event PenaltyImposed(address indexed minter, uint112 principalAmount, uint240 amount);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`minter`|`address`|         The address of the minter.|
|`principalAmount`|`uint112`|The principal amount of penalty charge.|
|`amount`|`uint240`|         The present amount of penalty charge.|

### RetrievalCreated
Emitted when a collateral retrieval proposal is created.


```solidity
event RetrievalCreated(uint48 indexed retrievalId, address indexed minter, uint240 amount);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`retrievalId`|`uint48`|The id of retrieval proposal.|
|`minter`|`address`|     The address of the minter.|
|`amount`|`uint240`|     The amount of collateral to retrieve.|

### RetrievalResolved
Emitted when a collateral retrieval proposal is resolved.


```solidity
event RetrievalResolved(uint48 indexed retrievalId, address indexed minter);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`retrievalId`|`uint48`|The id of retrieval proposal.|
|`minter`|`address`|     The address of the minter.|

## Errors
### DeactivatedMinter
Emitted when calling `activateMinter` with a minter who was previously deactivated.


```solidity
error DeactivatedMinter();
```

### ExceedsMaxRepayAmount
Emitted when repay will burn more M than the repay specified.


```solidity
error ExceedsMaxRepayAmount(uint240 amount, uint240 maxAmount);
```

### ExpiredMintProposal
Emitted when calling `mintM` with a proposal that was created more than `mintDelay + mintTTL` time ago.


```solidity
error ExpiredMintProposal(uint40 deadline);
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

### InactiveMinter
Emitted when calling a function only allowed for active minters.


```solidity
error InactiveMinter();
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

### NotApprovedMinter
Emitted when calling `activateMinter` if minter was not approved by TTG.


```solidity
error NotApprovedMinter();
```

### NotApprovedValidator
Emitted when calling `cancelMint` or `freezeMinter` if validator was not approved by TTG.


```solidity
error NotApprovedValidator();
```

### NotEnoughValidSignatures
Emitted when calling `updateCollateral` if `validatorThreshold` of signatures was not reached.


```solidity
error NotEnoughValidSignatures(uint256 validSignatures, uint256 requiredThreshold);
```

### OverflowsPrincipalOfTotalOwedM
Emitted when principal of total owed M (active and inactive) will overflow a `type(uint112).max`.


```solidity
error OverflowsPrincipalOfTotalOwedM();
```

### PendingMintProposal
Emitted when calling `mintM` if `mintDelay` time has not passed yet.


```solidity
error PendingMintProposal(uint40 activeTimestamp);
```

### RetrievalsExceedCollateral
Emitted when calling `proposeRetrieval` if sum of all outstanding retrievals
Plus new proposed retrieval amount is greater than collateral.


```solidity
error RetrievalsExceedCollateral(uint240 totalPendingRetrievals, uint240 collateral);
```

### SignatureArrayLengthsMismatch
Emitted when calling `updateCollateral`
If `validators`, `signatures`, `timestamps` lengths do not match.


```solidity
error SignatureArrayLengthsMismatch();
```

### StaleCollateralUpdate
Emitted when calling `updateCollateral` if Minter Gateway has more fresh collateral update.


```solidity
error StaleCollateralUpdate(uint40 newTimestamp, uint40 lastCollateralUpdate);
```

### StillApprovedMinter
Emitted when calling `deactivateMinter` with a minter still approved in TTG Registrar.


```solidity
error StillApprovedMinter();
```

### Undercollateralized
Emitted when calling `proposeMint`, `mintM`, `proposeRetrieval`
If minter position becomes undercollateralized.

*`activeOwedM` is a `uint256` because it may represent some resulting owed M from computations.*


```solidity
error Undercollateralized(uint256 activeOwedM, uint256 maxAllowedOwedM);
```

### ZeroBurnAmount
Emitted when calling `burnM` if amount is 0.


```solidity
error ZeroBurnAmount();
```

### ZeroMToken
Emitted in constructor if M Token is 0x0.


```solidity
error ZeroMToken();
```

### ZeroMintAmount
Emitted when calling `proposeMint` if amount is 0.


```solidity
error ZeroMintAmount();
```

### ZeroMintDestination
Emitted when calling `proposeMint` if destination is 0x0.


```solidity
error ZeroMintDestination();
```

### ZeroRetrievalAmount
Emitted when calling `proposeRetrieval` if collateral is 0.


```solidity
error ZeroRetrievalAmount();
```

### ZeroTTGRegistrar
Emitted in constructor if TTG Registrar is 0x0.


```solidity
error ZeroTTGRegistrar();
```

### ZeroTTGVault
Emitted in constructor if TTG Distribution Vault is set to 0x0 in TTG Registrar.


```solidity
error ZeroTTGVault();
```

### ZeroTimestamp
Emitted when calling `updateCollateral` if validator timestamp is 0.


```solidity
error ZeroTimestamp();
```

