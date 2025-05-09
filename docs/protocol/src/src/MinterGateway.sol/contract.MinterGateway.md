# MinterGateway
[Git Source](https://github.com/MZero-Labs/protocol/blob/3382fb7336bbc7276e0c3f51da451c9fa6e0016f/src/MinterGateway.sol)

**Inherits:**
[IMinterGateway](/src/interfaces/IMinterGateway.sol/interface.IMinterGateway.md), [ContinuousIndexing](/src/abstract/ContinuousIndexing.sol/abstract.ContinuousIndexing.md), ERC712Extended

**Author:**
M^0 Labs

Minting Gateway of M Token for all approved by TTG and activated minters.


## State Variables
### ONE
Descaler for variables in basis points. Effectively, 100% in basis points.


```solidity
uint16 public constant ONE = 10_000;
```


### MAX_MINT_RATIO
Mint ratio cap. 650% in basis points.


```solidity
uint32 public constant MAX_MINT_RATIO = 65_000;
```


### UPDATE_COLLATERAL_TYPEHASH
The EIP-712 typehash for the `updateCollateral` method.

*keccak256("UpdateCollateral(address minter,uint256 collateral,uint256[] retrievalIds,bytes32 metadataHash,uint256 timestamp)")*


```solidity
bytes32 public constant UPDATE_COLLATERAL_TYPEHASH = 0x22b57ca54bd15c6234b29e87aa1d76a0841b6e65e63d7acacef989de0bc3ff9e;
```


### ttgRegistrar
The address of TTG Registrar contract.


```solidity
address public immutable ttgRegistrar;
```


### ttgVault
The address of TTG Vault contract.


```solidity
address public immutable ttgVault;
```


### mToken
The address of M token


```solidity
address public immutable mToken;
```


### totalInactiveOwedM
The total owed M for all inactive minters.


```solidity
uint240 public totalInactiveOwedM;
```


### principalOfTotalActiveOwedM
The principal of total owed M for all active minters.


```solidity
uint112 public principalOfTotalActiveOwedM;
```


### _mintNonce
*Nonce used to generate unique mint proposal IDs.*


```solidity
uint48 internal _mintNonce;
```


### _retrievalNonce
*Nonce used to generate unique retrieval proposal IDs.*


```solidity
uint48 internal _retrievalNonce;
```


### _minterStates
*The state of each minter, their collaterals, relevant timestamps, and total pending retrievals.*


```solidity
mapping(address minter => MinterState state) internal _minterStates;
```


### _mintProposals
*The mint proposals of minter (mint ID, creation timestamp, destination, amount).*


```solidity
mapping(address minter => MintProposal proposal) internal _mintProposals;
```


### _rawOwedM
*The owed M of active and inactive minters (principal of active, inactive).*


```solidity
mapping(address minter => uint240 rawOwedM) internal _rawOwedM;
```


### _pendingCollateralRetrievals
*The pending collateral retrievals of minter (retrieval ID, amount).*


```solidity
mapping(address minter => mapping(uint48 retrievalId => uint240 amount)) internal _pendingCollateralRetrievals;
```


## Functions
### onlyActiveMinter

Only allow active minter to call function.


```solidity
modifier onlyActiveMinter(address minter_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`minter_`|`address`|The address of the minter to check.|


### onlyApprovedValidator

Only allow approved validator in TTG to call function.


```solidity
modifier onlyApprovedValidator();
```

### onlyUnfrozenMinter

Only allow unfrozen minter to call function.


```solidity
modifier onlyUnfrozenMinter();
```

### constructor

Constructor.


```solidity
constructor(address ttgRegistrar_, address mToken_) ContinuousIndexing() ERC712Extended("MinterGateway");
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`ttgRegistrar_`|`address`|The address of the TTG Registrar contract.|
|`mToken_`|`address`|       The address of the M Token.|


### updateCollateral

Updates collateral for minters


```solidity
function updateCollateral(
    uint256 collateral_,
    uint256[] calldata retrievalIds_,
    bytes32 metadataHash_,
    address[] calldata validators_,
    uint256[] calldata timestamps_,
    bytes[] calldata signatures_
) external onlyActiveMinter(msg.sender) returns (uint40 minTimestamp_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`collateral_`|`uint256`||
|`retrievalIds_`|`uint256[]`||
|`metadataHash_`|`bytes32`||
|`validators_`|`address[]`||
|`timestamps_`|`uint256[]`||
|`signatures_`|`bytes[]`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`minTimestamp_`|`uint40`|minTimestamp The minimum timestamp of all validators' signatures|


### proposeRetrieval

Proposes retrieval of minter's offchain collateral


```solidity
function proposeRetrieval(uint256 collateral_) external onlyActiveMinter(msg.sender) returns (uint48 retrievalId_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`collateral_`|`uint256`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`retrievalId_`|`uint48`|retrievalId The unique id of created retrieval proposal|


### proposeMint

Proposes minting of M tokens


```solidity
function proposeMint(uint256 amount_, address destination_)
    external
    onlyActiveMinter(msg.sender)
    onlyUnfrozenMinter
    returns (uint48 mintId_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`amount_`|`uint256`||
|`destination_`|`address`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`mintId_`|`uint48`|mintId      The unique id of created mint proposal|


### mintM

Executes minting of M tokens


```solidity
function mintM(uint256 mintId_)
    external
    onlyActiveMinter(msg.sender)
    onlyUnfrozenMinter
    returns (uint112 principalAmount_, uint240 amount_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`mintId_`|`uint256`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`principalAmount_`|`uint112`|principalAmount The amount of principal of owed M minted.|
|`amount_`|`uint240`|amount          The amount of M tokens minted.|


### burnM

Burns M tokens

*If the amount to burn is greater than minter's owedM including penalties, burn all up to owedM.*


```solidity
function burnM(address minter_, uint256 maxAmount_) external returns (uint112 principalAmount_, uint240 amount_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`minter_`|`address`||
|`maxAmount_`|`uint256`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`principalAmount_`|`uint112`|principalAmount The amount of principal of owed M burned.|
|`amount_`|`uint240`|amount          The amount of M tokens burned.|


### burnM

Burns M tokens

*If the amount to burn is greater than minter's owedM including penalties, burn all up to owedM.*


```solidity
function burnM(address minter_, uint256 maxPrincipalAmount_, uint256 maxAmount_)
    public
    returns (uint112 principalAmount_, uint240 amount_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`minter_`|`address`||
|`maxPrincipalAmount_`|`uint256`||
|`maxAmount_`|`uint256`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`principalAmount_`|`uint112`|principalAmount The amount of principal of owed M burned.|
|`amount_`|`uint240`|amount          The amount of M tokens burned.|


### cancelMint

Cancels minting request for selected minter by the validator


```solidity
function cancelMint(address minter_, uint256 mintId_) external onlyApprovedValidator;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`minter_`|`address`||
|`mintId_`|`uint256`||


### freezeMinter

Freezes minter


```solidity
function freezeMinter(address minter_) external onlyApprovedValidator returns (uint40 frozenUntil_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`minter_`|`address`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`frozenUntil_`|`uint40`|frozenUntil The timestamp until which minter is frozen|


### activateMinter

Activate an approved minter.

*MUST revert if `minter` is not recorded as an approved minter in TTG Registrar.*


```solidity
function activateMinter(address minter_) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`minter_`|`address`||


### deactivateMinter

Deactivates an active minter.

*MUST revert if the minter is still approved.*


```solidity
function deactivateMinter(address minter_) external onlyActiveMinter(minter_) returns (uint240 inactiveOwedM_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`minter_`|`address`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`inactiveOwedM_`|`uint240`|inactiveOwedM The inactive owed M for the deactivated minter.|


### updateIndex

Updates the latest index and latest accrual time in storage.


```solidity
function updateIndex() public override(IContinuousIndexing, ContinuousIndexing) returns (uint128 index_);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`index_`|`uint128`|index The new stored index for computing present amounts from principal amounts.|


### totalActiveOwedM

The total owed M for all active minters.


```solidity
function totalActiveOwedM() public view returns (uint240);
```

### totalOwedM

The total owed M for all minters.


```solidity
function totalOwedM() external view returns (uint240);
```

### excessOwedM

The difference between total owed M and M token total supply.


```solidity
function excessOwedM() public view returns (uint240 excessOwedM_);
```

### minterRate

The last saved value of Minter rate.


```solidity
function minterRate() external view returns (uint32);
```

### isActiveMinter

Checks if the minter was activated after approval by TTG


```solidity
function isActiveMinter(address minter_) external view returns (bool);
```

### isDeactivatedMinter

Checks if minter was deactivated after removal by TTG


```solidity
function isDeactivatedMinter(address minter_) external view returns (bool);
```

### isFrozenMinter

Checks if the minter was frozen by validator


```solidity
function isFrozenMinter(address minter_) external view returns (bool);
```

### principalOfActiveOwedMOf

The principal of active owed M of minter.


```solidity
function principalOfActiveOwedMOf(address minter_) public view returns (uint112);
```

### activeOwedMOf

The active owed M of minter.


```solidity
function activeOwedMOf(address minter_) public view returns (uint240);
```

### maxAllowedActiveOwedMOf

The max allowed active owed M of minter taking into account collateral amount and retrieval proposals.

*This is the only present value that requires a `uint256` since it is the result of a multiplication
between a `uint240` and a value that has a max of `65,000` (the mint ratio).*


```solidity
function maxAllowedActiveOwedMOf(address minter_) public view returns (uint256);
```

### inactiveOwedMOf

The inactive owed M of deactivated minter.


```solidity
function inactiveOwedMOf(address minter_) public view returns (uint240);
```

### collateralOf

The collateral of a given minter.


```solidity
function collateralOf(address minter_) public view returns (uint240);
```

### collateralUpdateTimestampOf

The timestamp of the last collateral update of minter.


```solidity
function collateralUpdateTimestampOf(address minter_) external view returns (uint40);
```

### collateralPenaltyDeadlineOf

The timestamp after which an additional penalty for a missed update interval will be charged.


```solidity
function collateralPenaltyDeadlineOf(address minter_) external view returns (uint40);
```

### collateralExpiryTimestampOf

The timestamp after which the minter's collateral is assumed to be 0 due to a missed update.


```solidity
function collateralExpiryTimestampOf(address minter_) public view returns (uint40);
```

### penalizedUntilOf

The timestamp until which minter is already penalized for missed collateral updates.


```solidity
function penalizedUntilOf(address minter_) external view returns (uint40);
```

### getPenaltyForMissedCollateralUpdates

The penalty for missed collateral updates. Penalized once per missed interval.


```solidity
function getPenaltyForMissedCollateralUpdates(address minter_) external view returns (uint240);
```

### getUpdateCollateralDigest

Returns the EIP-712 digest for updateCollateral method.


```solidity
function getUpdateCollateralDigest(
    address minter_,
    uint256 collateral_,
    uint256[] calldata retrievalIds_,
    bytes32 metadataHash_,
    uint256 timestamp_
) external view returns (bytes32);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`minter_`|`address`||
|`collateral_`|`uint256`||
|`retrievalIds_`|`uint256[]`||
|`metadataHash_`|`bytes32`||
|`timestamp_`|`uint256`||


### mintProposalOf

The mint proposal of minters, only 1 active proposal per minter


```solidity
function mintProposalOf(address minter_)
    external
    view
    returns (uint48 mintId_, uint40 createdAt_, address destination_, uint240 amount_);
```

### pendingCollateralRetrievalOf

The minter's proposeRetrieval proposal amount


```solidity
function pendingCollateralRetrievalOf(address minter_, uint256 retrievalId_) external view returns (uint240);
```

### totalPendingCollateralRetrievalOf

The total amount of active proposeRetrieval requests per minter


```solidity
function totalPendingCollateralRetrievalOf(address minter_) external view returns (uint240);
```

### frozenUntilOf

The timestamp when minter becomes unfrozen after being frozen by validator.


```solidity
function frozenUntilOf(address minter_) external view returns (uint40);
```

### isMinterApproved

Checks if minter was approved by TTG


```solidity
function isMinterApproved(address minter_) public view returns (bool);
```

### isValidatorApprovedByTTG

Checks if validator was approved by TTG


```solidity
function isValidatorApprovedByTTG(address validator_) public view returns (bool);
```

### updateCollateralInterval

The interval that defines the required frequency of collateral updates.


```solidity
function updateCollateralInterval() public view returns (uint32);
```

### updateCollateralValidatorThreshold

The number of signatures required for successful collateral update.


```solidity
function updateCollateralValidatorThreshold() public view returns (uint256);
```

### mintRatio

The allowed activeOwedM to collateral ratio.


```solidity
function mintRatio() public view returns (uint32);
```

### mintDelay

The delay between mint proposal creation and its earliest execution.


```solidity
function mintDelay() public view returns (uint32);
```

### mintTTL

The time while mint request can still be processed before it is considered expired.


```solidity
function mintTTL() public view returns (uint32);
```

### minterFreezeTime

The freeze time for minter.


```solidity
function minterFreezeTime() public view returns (uint32);
```

### penaltyRate

The % that defines penalty amount for missed collateral updates or excessive owedM value


```solidity
function penaltyRate() public view returns (uint32);
```

### rateModel

The smart contract that defines the minter rate.


```solidity
function rateModel() public view returns (address);
```

### currentIndex

The current index that would be written to storage if `updateIndex` is called.


```solidity
function currentIndex() public view override(ContinuousIndexing, IContinuousIndexing) returns (uint128);
```

### _imposePenalty

*Imposes penalty on an active minter. Calling this for an inactive minter will break accounting.*


```solidity
function _imposePenalty(address minter_, uint152 principalOfPenaltyBase_) internal;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`minter_`|`address`|                The address of the minter.|
|`principalOfPenaltyBase_`|`uint152`|The principal of the base for penalization.|


### _imposePenaltyIfMissedCollateralUpdates

*Imposes penalty if minter missed collateral updates.*


```solidity
function _imposePenaltyIfMissedCollateralUpdates(address minter_) internal;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`minter_`|`address`|The address of the minter.|


### _imposePenaltyIfUndercollateralized

*Imposes penalty if minter is undercollateralized.*


```solidity
function _imposePenaltyIfUndercollateralized(address minter_) internal;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`minter_`|`address`|The address of the minter|


### _repayForActiveMinter

*Repays active minter's owed M.*


```solidity
function _repayForActiveMinter(address minter_, uint112 maxPrincipalAmount_, uint240 maxAmount_)
    internal
    returns (uint112 principalAmount_, uint240 amount_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`minter_`|`address`|            The address of the minter.|
|`maxPrincipalAmount_`|`uint112`|The maximum principal amount of active owed M to repay.|
|`maxAmount_`|`uint240`|         The maximum amount of active owed M to repay.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`principalAmount_`|`uint112`|   The principal amount of active owed M that was actually repaid.|
|`amount_`|`uint240`|            The amount of active owed M that was actually repaid.|


### _repayForInactiveMinter

*Repays inactive minter's owed M.*


```solidity
function _repayForInactiveMinter(address minter_, uint240 maxAmount_) internal returns (uint240 amount_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`minter_`|`address`|   The address of the minter.|
|`maxAmount_`|`uint240`|The maximum amount of inactive owed M to repay.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`amount_`|`uint240`|   The amount of inactive owed M that was actually repaid.|


### _resolvePendingRetrievals

*Resolves the collateral retrieval IDs and updates the total pending collateral retrieval amount.*


```solidity
function _resolvePendingRetrievals(address minter_, uint256[] calldata retrievalIds_)
    internal
    returns (uint240 totalResolvedCollateralRetrieval_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`minter_`|`address`|                          The address of the minter.|
|`retrievalIds_`|`uint256[]`|                    The list of outstanding collateral retrieval IDs to resolve.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`totalResolvedCollateralRetrieval_`|`uint240`|The total amount of collateral retrieval resolved.|


### _updateCollateral

*Updates the collateral amount and update timestamp for the minter.*


```solidity
function _updateCollateral(address minter_, uint240 amount_, uint40 newTimestamp_) internal;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`minter_`|`address`|      The address of the minter.|
|`amount_`|`uint240`|      The amount of collateral.|
|`newTimestamp_`|`uint40`|The timestamp of the collateral update.|


### _getMissedCollateralUpdateParameters

*Returns the penalization base and the penalized until timestamp.*


```solidity
function _getMissedCollateralUpdateParameters(
    uint40 lastUpdateTimestamp_,
    uint40 lastPenalizedUntil_,
    uint32 updateInterval_
) internal view returns (uint40 missedIntervals_, uint40 missedUntil_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`lastUpdateTimestamp_`|`uint40`|The last timestamp at which the minter updated their collateral.|
|`lastPenalizedUntil_`|`uint40`| The timestamp before which the minter shouldn't be penalized for missed updates.|
|`updateInterval_`|`uint32`|     The update collateral interval.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`missedIntervals_`|`uint40`|    The number of missed update intervals.|
|`missedUntil_`|`uint40`|        The timestamp until which `missedIntervals_` covers, even if `missedIntervals_` is 0.|


### _getPenaltyPrincipalForMissedCollateralUpdates

*Returns the principal penalization base for a minter's missed collateral updates.*


```solidity
function _getPenaltyPrincipalForMissedCollateralUpdates(address minter_) internal view returns (uint112);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`minter_`|`address`|The address of the minter.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint112`|The penalty principal.|


### _getPresentAmount

*Returns the present amount (rounded up) given the principal amount, using the current index.
All present amounts are rounded up in favor of the protocol, since they are owed.*


```solidity
function _getPresentAmount(uint112 principalAmount_) internal view returns (uint240);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`principalAmount_`|`uint112`|The principal amount.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint240`|The present amount.|


### _getUpdateCollateralDigest

*Returns the EIP-712 digest for updateCollateral method.*


```solidity
function _getUpdateCollateralDigest(
    address minter_,
    uint256 collateral_,
    uint256[] calldata retrievalIds_,
    bytes32 metadataHash_,
    uint256 timestamp_
) internal view returns (bytes32);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`minter_`|`address`|      The address of the minter.|
|`collateral_`|`uint256`|  The amount of collateral.|
|`retrievalIds_`|`uint256[]`|The list of outstanding collateral retrieval IDs to resolve.|
|`metadataHash_`|`bytes32`|The hash of metadata of the collateral update, reserved for future informational use.|
|`timestamp_`|`uint256`|   The timestamp of the collateral update.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bytes32`|The EIP-712 digest.|


### _rate

*Returns the current rate from the rate model contract.*


```solidity
function _rate() internal view override returns (uint32 rate_);
```

### _revertIfFrozenMinter

*Reverts if minter is frozen by validator.*


```solidity
function _revertIfFrozenMinter(address minter_) internal view;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`minter_`|`address`|The address of the minter|


### _revertIfInactiveMinter

*Reverts if minter is inactive.*


```solidity
function _revertIfInactiveMinter(address minter_) internal view;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`minter_`|`address`|The address of the minter|


### _revertIfNotApprovedValidator

*Reverts if validator is not approved.*


```solidity
function _revertIfNotApprovedValidator(address validator_) internal view;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`validator_`|`address`|The address of the validator|


### _revertIfUndercollateralized

*Reverts if minter position will be undercollateralized after changes.*


```solidity
function _revertIfUndercollateralized(address minter_, uint240 additionalOwedM_) internal view;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`minter_`|`address`|         The address of the minter|
|`additionalOwedM_`|`uint240`|The amount of additional owed M the action will add to minter's position|


### _verifyValidatorSignatures

*Checks that enough valid unique signatures were provided.*


```solidity
function _verifyValidatorSignatures(
    address minter_,
    uint256 collateral_,
    uint256[] calldata retrievalIds_,
    bytes32 metadataHash_,
    address[] calldata validators_,
    uint256[] calldata timestamps_,
    bytes[] calldata signatures_
) internal view returns (uint40 minTimestamp_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`minter_`|`address`|      The address of the minter.|
|`collateral_`|`uint256`|  The amount of collateral.|
|`retrievalIds_`|`uint256[]`|The list of outstanding collateral retrieval IDs to resolve.|
|`metadataHash_`|`bytes32`|The hash of metadata of the collateral update, reserved for future informational use.|
|`validators_`|`address[]`|  The list of validators.|
|`timestamps_`|`uint256[]`|  The list of validator timestamps for the collateral update signatures.|
|`signatures_`|`bytes[]`|  The list of signatures.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`minTimestamp_`|`uint40`|The minimum timestamp across all valid timestamps with valid signatures.|


## Structs
### MintProposal
Mint proposal struct.


```solidity
struct MintProposal {
    uint48 id;
    uint40 createdAt;
    address destination;
    uint240 amount;
}
```

**Properties**

|Name|Type|Description|
|----|----|-----------|
|`id`|`uint48`|         The unique ID of the mint proposal.|
|`createdAt`|`uint40`|  The timestamp at which the mint proposal was created.|
|`destination`|`address`|The address to mint M to.|
|`amount`|`uint240`|     The amount of M to mint.|

### MinterState
Minter state struct.


```solidity
struct MinterState {
    bool isActive;
    bool isDeactivated;
    uint240 collateral;
    uint240 totalPendingRetrievals;
    uint40 updateTimestamp;
    uint40 penalizedUntilTimestamp;
    uint40 frozenUntilTimestamp;
}
```

**Properties**

|Name|Type|Description|
|----|----|-----------|
|`isActive`|`bool`|               Whether the minter is active or not.|
|`isDeactivated`|`bool`|          Whether the minter is deactivated or not.|
|`collateral`|`uint240`|             The amount of collateral the minter has.|
|`totalPendingRetrievals`|`uint240`| The total amount of pending retrievals.|
|`updateTimestamp`|`uint40`|        The timestamp at which the minter last updated their collateral.|
|`penalizedUntilTimestamp`|`uint40`|The timestamp until which the minter is penalized.|
|`frozenUntilTimestamp`|`uint40`|   The timestamp until which the minter is frozen.|

