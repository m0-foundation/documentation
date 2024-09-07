# Protocol
[Git Source](https://github.com/MZero-Labs/protocol/blob/45d6176ce6231b36efc0c52a2961774481e32ec1/src/Protocol.sol)

**Inherits:**
[IProtocol](/src/interfaces/IProtocol.sol/interface.IProtocol.md), [ContinuousIndexing](/src/ContinuousIndexing.sol/abstract.ContinuousIndexing.md), ERC712

**Author:**
M^ZERO LABS_

Core protocol of M^ZERO ecosystem.
Minting Gateway of M Token for all approved by SPOG and activated minters.


## State Variables
### ONE
\
|                                                    Variables                                                     |
\*****************************************************************************************************************


```solidity
uint256 public constant ONE = 10_000;
```


### UPDATE_COLLATERAL_TYPEHASH

```solidity
bytes32 public constant UPDATE_COLLATERAL_TYPEHASH = 0x22b57ca54bd15c6234b29e87aa1d76a0841b6e65e63d7acacef989de0bc3ff9e;
```


### spogRegistrar
The address of SPOG Registrar contract.


```solidity
address public immutable spogRegistrar;
```


### spogVault
The address of SPOG Vault contract.


```solidity
address public immutable spogVault;
```


### mToken
The address of M Token.


```solidity
address public immutable mToken;
```


### _mintNonce
Nonce used to generate unique mint proposal IDs.


```solidity
uint256 internal _mintNonce;
```


### _retrievalNonce
Nonce used to generate unique retrieval proposal IDs.


```solidity
uint256 internal _retrievalNonce;
```


### _totalPrincipalOfActiveOwedM
The total principal amount of active M


```solidity
uint256 internal _totalPrincipalOfActiveOwedM;
```


### _totalInactiveOwedM
The total amount of inactive M, sum of all inactive minter's owed M


```solidity
uint256 internal _totalInactiveOwedM;
```


### _isActiveMinter

```solidity
mapping(address minter => bool isActiveMinter) internal _isActiveMinter;
```


### _mintProposals

```solidity
mapping(address minter => MintProposal proposal) internal _mintProposals;
```


### _inactiveOwedM

```solidity
mapping(address minter => uint256 amount) internal _inactiveOwedM;
```


### _principalOfActiveOwedM

```solidity
mapping(address minter => uint256 principal) internal _principalOfActiveOwedM;
```


### _collaterals

```solidity
mapping(address minter => uint256 collateral) internal _collaterals;
```


### _lastUpdateIntervals

```solidity
mapping(address minter => uint256 updateInterval) internal _lastUpdateIntervals;
```


### _lastCollateralUpdates

```solidity
mapping(address minter => uint256 timestamp) internal _lastCollateralUpdates;
```


### _penalizedUntilTimestamps

```solidity
mapping(address minter => uint256 timestamp) internal _penalizedUntilTimestamps;
```


### _totalPendingCollateralRetrievals

```solidity
mapping(address minter => uint256 collateral) internal _totalPendingCollateralRetrievals;
```


### _pendingCollateralRetrievals

```solidity
mapping(address minter => mapping(uint256 retrievalId => uint256 amount)) internal _pendingCollateralRetrievals;
```


### _unfrozenTimestamps

```solidity
mapping(address minter => uint256 timestamp) internal _unfrozenTimestamps;
```


## Functions
### onlyActiveMinter

\
|                                            Modifiers and Constructor                                             |
\*****************************************************************************************************************

Only allow active minter to call function.


```solidity
modifier onlyActiveMinter();
```

### onlyApprovedValidator

Only allow approved validator in SPOG to call function.


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
constructor(address spogRegistrar_, address mToken_) ContinuousIndexing ERC712("Protocol");
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`spogRegistrar_`|`address`|The address of the SPOG Registrar contract.|
|`mToken_`|`address`|The address of the M Token.|


### updateCollateral

\
|                                          External Interactive Functions                                          |
\*****************************************************************************************************************


```solidity
function updateCollateral(
    uint256 collateral_,
    uint256[] calldata retrievalIds_,
    bytes32 metadataHash_,
    address[] calldata validators_,
    uint256[] calldata timestamps_,
    bytes[] calldata signatures_
) external onlyActiveMinter returns (uint256 minTimestamp_);
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
|`minTimestamp_`|`uint256`|The minimum timestamp of all validators' signatures|


### proposeRetrieval

Proposes retrieval of minter's offchain collateral


```solidity
function proposeRetrieval(uint256 collateral_) external onlyActiveMinter returns (uint256 retrievalId_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`collateral_`|`uint256`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`retrievalId_`|`uint256`|retrievalId The unique id of created retrieval proposal|


### proposeMint

Proposes minting of M tokens


```solidity
function proposeMint(uint256 amount_, address destination_)
    external
    onlyActiveMinter
    onlyUnfrozenMinter
    returns (uint256 mintId_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`amount_`|`uint256`||
|`destination_`|`address`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`mintId_`|`uint256`|mintId The unique id of created mint proposal|


### mintM

Executes minting of M tokens


```solidity
function mintM(uint256 mintId_) external onlyActiveMinter onlyUnfrozenMinter;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`mintId_`|`uint256`||


### burnM

Burns M tokens

*If the amount to burn is greater than the minter's outstandingValue including penalties, burn all outstandingValue*


```solidity
function burnM(address minter_, uint256 maxAmount_) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`minter_`|`address`||
|`maxAmount_`|`uint256`||


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
function freezeMinter(address minter_) external onlyApprovedValidator returns (uint256 frozenUntil_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`minter_`|`address`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`frozenUntil_`|`uint256`|The timestamp until which minter is frozen|


### activateMinter

Activate an approved minter.

*MUST revert if `minter` is not recorded as an approved minter in SPOG Registrar.*


```solidity
function activateMinter(address minter_) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`minter_`|`address`||


### deactivateMinter

Deactivates an active minter.

*MUST revert if the minter is not an approved minter.*


```solidity
function deactivateMinter(address minter_) external returns (uint256 inactiveOwedM_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`minter_`|`address`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`inactiveOwedM_`|`uint256`|inactiveOwedM The inactive owed M for the deactivated minter|


### updateIndex

Updates the latest index and latest accrual time in storage.


```solidity
function updateIndex() public override(IContinuousIndexing, ContinuousIndexing) returns (uint256 index_);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`index_`|`uint256`|index The new stored index for computing present values from principal values.|


### totalActiveOwedM

\
|                                           External View/Pure Functions                                           |
\*****************************************************************************************************************


```solidity
function totalActiveOwedM() public view returns (uint256 totalActiveOwedM_);
```

### totalInactiveOwedM

The total owed M for all inactive minters.


```solidity
function totalInactiveOwedM() public view returns (uint256 totalInactiveOwedM_);
```

### totalOwedM

The total owed M for all minters.


```solidity
function totalOwedM() external view returns (uint256 totalOwedM_);
```

### excessActiveOwedM

The difference between total active owed M and M token total supply.


```solidity
function excessActiveOwedM() public view returns (uint256 getExcessOwedM_);
```

### minterRate

The last saved value of the Minter rate.


```solidity
function minterRate() external view returns (uint256 minterRate_);
```

### activeOwedMOf

The active owed M of the minter.


```solidity
function activeOwedMOf(address minter_) public view returns (uint256 activeOwedM_);
```

### maxAllowedActiveOwedMOf

The max allowed active owed M of minter taking into account collateral amount and retrieval proposals.


```solidity
function maxAllowedActiveOwedMOf(address minter_) public view returns (uint256 maxAllowedOwedM_);
```

### inactiveOwedMOf

The inactive owed M of deactivated minter.


```solidity
function inactiveOwedMOf(address minter_) external view returns (uint256 inactiveOwedM_);
```

### collateralOf

The collateral of a given minter.


```solidity
function collateralOf(address minter_) public view returns (uint256 collateral_);
```

### collateralUpdateOf

The timestamp of the last collateral update of minter.


```solidity
function collateralUpdateOf(address minter_) external view returns (uint256 lastUpdate_);
```

### collateralUpdateDeadlineOf

The timestamp of the deadline for the next collateral update of minter.


```solidity
function collateralUpdateDeadlineOf(address minter_) public view returns (uint256 updateDeadline_);
```

### lastCollateralUpdateIntervalOf

The length of the last collateral interval for minter in case SPOG changes this parameter.


```solidity
function lastCollateralUpdateIntervalOf(address minter_) external view returns (uint256 lastUpdateInterval_);
```

### penalizedUntilOf

The timestamp until which minter is already penalized for missed collateral updates.


```solidity
function penalizedUntilOf(address minter_) external view returns (uint256 penalizedUntil_);
```

### getPenaltyForMissedCollateralUpdates

The penalty for missed collateral updates. Penalized once per missed interval.


```solidity
function getPenaltyForMissedCollateralUpdates(address minter_) public view returns (uint256 penalty_);
```

### mintProposalOf

The mint proposal of minters, only 1 active proposal per minter


```solidity
function mintProposalOf(address minter_)
    external
    view
    returns (uint256 mintId_, address destination_, uint256 amount_, uint256 createdAt_);
```

### pendingCollateralRetrievalOf

The minter's proposeRetrieval proposal amount


```solidity
function pendingCollateralRetrievalOf(address minter_, uint256 retrievalId_)
    external
    view
    returns (uint256 collateral);
```

### totalPendingCollateralRetrievalsOf

The total amount of active proposeRetrieval requests per minter


```solidity
function totalPendingCollateralRetrievalsOf(address minter_) external view returns (uint256 collateral_);
```

### unfrozenTimeOf

The timestamp when minter becomes unfrozen after being frozen by validator.


```solidity
function unfrozenTimeOf(address minter_) external view returns (uint256 timestamp_);
```

### isActiveMinter

\
|                                       SPOG Registrar Reader Functions                                            |
\*****************************************************************************************************************


```solidity
function isActiveMinter(address minter_) external view returns (bool isActive_);
```

### isMinterApprovedBySPOG

Checks if minter was approved by SPOG


```solidity
function isMinterApprovedBySPOG(address minter_) public view returns (bool isApproved_);
```

### isValidatorApprovedBySPOG

Checks if validator was approved by SPOG


```solidity
function isValidatorApprovedBySPOG(address validator_) public view returns (bool isApproved_);
```

### updateCollateralInterval

The interval that defines the required frequency of collateral updates.


```solidity
function updateCollateralInterval() public view returns (uint256 updateCollateralInterval_);
```

### updateCollateralValidatorThreshold

The number of signatures required for successful collateral update.


```solidity
function updateCollateralValidatorThreshold() public view returns (uint256 threshold_);
```

### mintRatio

The allowed activeOwedM to collateral ratio.


```solidity
function mintRatio() public view returns (uint256 mintRatio_);
```

### mintDelay

The delay between mint proposal creation and its earliest execution.


```solidity
function mintDelay() public view returns (uint256 mintDelay_);
```

### mintTTL

The time while mint request can still be processed before it is considered expired.


```solidity
function mintTTL() public view returns (uint256 mintTTL_);
```

### minterFreezeTime

The freeze time for minter.


```solidity
function minterFreezeTime() public view returns (uint256 minterFreezeTime_);
```

### penaltyRate

The % that defines penalty amount for missed collateral updates or excessive owedM value


```solidity
function penaltyRate() public view returns (uint256 penaltyRate_);
```

### rateModel

The smart contract that defines the minter rate.


```solidity
function rateModel() public view returns (address rateModel_);
```

### _imposePenalty

\
|                                          Internal Interactive Functions                                          |
\*****************************************************************************************************************

Imposes penalty on minter.

*penalty = penalty base * penalty rate*


```solidity
function _imposePenalty(address minter_, uint256 penaltyBase_) internal;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`minter_`|`address`|The address of the minter|
|`penaltyBase_`|`uint256`|The total penalization base|


### _imposePenaltyIfMissedCollateralUpdates

Imposes penalty if minter missed collateral updates.

*penalty = total active owed M * penalty rate * number of missed intervals*


```solidity
function _imposePenaltyIfMissedCollateralUpdates(address minter_) internal;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`minter_`|`address`|The address of the minter|


### _imposePenaltyIfUndercollateralized

Imposes penalty if minter is undercollateralized.

*penalty = excess active owed M * penalty rate*


```solidity
function _imposePenaltyIfUndercollateralized(address minter_) internal;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`minter_`|`address`|The address of the minter|


### _repayForActiveMinter

Repays active (not deactivated, not removed from SPOG) minter's owed M.


```solidity
function _repayForActiveMinter(address minter_, uint256 maxAmount_) internal returns (uint256 amount_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`minter_`|`address`|The address of the minter|
|`maxAmount_`|`uint256`|The maximum amount of active owed M to repay|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`amount_`|`uint256`|The amount of active owed M that was actually repaid|


### _repayForInactiveMinter

Repays inactive (deactivated, removed from SPOG) minter's owed M.


```solidity
function _repayForInactiveMinter(address minter_, uint256 maxAmount_) internal returns (uint256 amount_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`minter_`|`address`|The address of the minter|
|`maxAmount_`|`uint256`|The maximum amount of inactive owed M to repay|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`amount_`|`uint256`|The amount of inactive owed M that was actually repaid|


### _resolvePendingRetrievals

Resolves the collateral retrieval IDs and updates the total pending collateral retrieval amount.


```solidity
function _resolvePendingRetrievals(address minter_, uint256[] calldata retrievalIds_) internal;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`minter_`|`address`|The address of the minter|
|`retrievalIds_`|`uint256[]`|The list of outstanding collateral retrieval IDs to resolve|


### _updateCollateral

Updates the collateral amount and update timestamp for the minter.


```solidity
function _updateCollateral(address minter_, uint256 amount_, uint256 newTimestamp_) internal;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`minter_`|`address`|The address of the minter|
|`amount_`|`uint256`|The amount of collateral|
|`newTimestamp_`|`uint256`|The timestamp of the collateral update, minimum of all given validator timestamps|


### _getPenaltyBaseAndTimeForMissedCollateralUpdates

\
|                                           Internal View/Pure Functions                                           |
\*****************************************************************************************************************

Returns the penalization base and the penalized until timestamp.


```solidity
function _getPenaltyBaseAndTimeForMissedCollateralUpdates(address minter_)
    internal
    view
    returns (uint256 penaltyBase_, uint256 penalizedUntil_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`minter_`|`address`|The address of the minter|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`penaltyBase_`|`uint256`|The base amount of penalty|
|`penalizedUntil_`|`uint256`|The timestamp until which minter is penalized for missed collateral updates|


### _getPresentValue

Returns the present value of M given the principal amount and the current index.

*present = pricipal * index*


```solidity
function _getPresentValue(uint256 principalValue_) internal view returns (uint256 presentValue_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`principalValue_`|`uint256`|The principal value of M|


### _getPrincipalValue

Returns the principal amount of M given the present value and the current index.

*present = principal * index*


```solidity
function _getPrincipalValue(uint256 presentValue_) internal view returns (uint256 principalValue_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`presentValue_`|`uint256`|The present value of M|


### _getUpdateCollateralDigest

Returns the EIP-712 digest for updateCollateral method


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
|`minter_`|`address`|The address of the minter|
|`collateral_`|`uint256`|The amount of collateral|
|`retrievalIds_`|`uint256[]`|The list of outstanding collateral retrieval IDs to resolve|
|`metadataHash_`|`bytes32`|The hash of metadata of the collateral update, reserved for future informational use|
|`timestamp_`|`uint256`|The timestamp of the collateral update|


### _max


```solidity
function _max(uint256 a_, uint256 b_) internal pure returns (uint256 max_);
```

### _min


```solidity
function _min(uint256 a_, uint256 b_) internal pure returns (uint256 min_);
```

### _minIgnoreZero


```solidity
function _minIgnoreZero(uint256 a_, uint256 b_) internal pure returns (uint256 min_);
```

### _rate

Returns the current rate from the rate model contract.


```solidity
function _rate() internal view override returns (uint256 rate_);
```

### _revertIfMinterFrozen

Reverts if minter is frozen by validator.


```solidity
function _revertIfMinterFrozen(address minter_) internal view;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`minter_`|`address`|The address of the minter|


### _revertIfInactiveMinter

Reverts if minter is inactive.


```solidity
function _revertIfInactiveMinter(address minter_) internal view;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`minter_`|`address`|The address of the minter|


### _revertIfNotApprovedValidator

Reverts if validator is not approved.


```solidity
function _revertIfNotApprovedValidator(address validator_) internal view;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`validator_`|`address`|The address of the validator|


### _revertIfUndercollateralized

Reverts if minter position will be undercollateralized after changes.


```solidity
function _revertIfUndercollateralized(address minter_, uint256 additionalOwedM_) internal view;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`minter_`|`address`|The address of the minter|
|`additionalOwedM_`|`uint256`|The amount of additional owed M the action will add to minter's position|


### _verifyValidatorSignatures

Checks that enough valid unique signatures were provided


```solidity
function _verifyValidatorSignatures(
    address minter_,
    uint256 collateral_,
    uint256[] calldata retrievalIds_,
    bytes32 metadataHash_,
    address[] calldata validators_,
    uint256[] calldata timestamps_,
    bytes[] calldata signatures_
) internal view returns (uint256 minTimestamp_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`minter_`|`address`|The address of the minter|
|`collateral_`|`uint256`|The amount of collateral|
|`retrievalIds_`|`uint256[]`|The list of proposed collateral retrieval IDs to resolve|
|`metadataHash_`|`bytes32`|The hash of metadata of the collateral update, reserved for future informational use|
|`validators_`|`address[]`|The list of validators|
|`timestamps_`|`uint256[]`|The list of validator timestamps for the collateral update signatures|
|`signatures_`|`bytes[]`|The list of signatures|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`minTimestamp_`|`uint256`|The minimum timestamp across all valid timestamps with valid signatures|


## Structs
### MintProposal

```solidity
struct MintProposal {
    uint256 id;
    address destination;
    uint256 amount;
    uint256 createdAt;
}
```

