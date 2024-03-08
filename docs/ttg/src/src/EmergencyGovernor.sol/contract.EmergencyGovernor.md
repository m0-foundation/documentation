# EmergencyGovernor
[Git Source](https://github.com/MZero-Labs/ttg/blob/0d2761f8db14b390e923f59bdae9799fbf9adf2c/src/EmergencyGovernor.sol)

**Inherits:**
[IEmergencyGovernor](/src/interfaces/IEmergencyGovernor.sol/interface.IEmergencyGovernor.md), [ThresholdGovernor](/src/abstract/ThresholdGovernor.sol/abstract.ThresholdGovernor.md)

**Author:**
M^0 Labs


## State Variables
### registrar
Returns the address of the Registrar.


```solidity
address public immutable registrar;
```


### standardGovernor
Returns the address of the Standard Governor.


```solidity
address public immutable standardGovernor;
```


### zeroGovernor
Returns the address of the Zero Governor.


```solidity
address public immutable zeroGovernor;
```


## Functions
### onlyZeroGovernor

*Throws if called by any account other than the Zero Governor.*


```solidity
modifier onlyZeroGovernor();
```

### constructor

Constructs a new Emergency Governor contract.


```solidity
constructor(
    address voteToken_,
    address zeroGovernor_,
    address registrar_,
    address standardGovernor_,
    uint16 thresholdRatio_
) ThresholdGovernor("EmergencyGovernor", voteToken_, thresholdRatio_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`voteToken_`|`address`|       The address of the Vote Token contract.|
|`zeroGovernor_`|`address`|    The address of the Zero Governor contract.|
|`registrar_`|`address`|       The address of the Registrar contract.|
|`standardGovernor_`|`address`|The address of the StandardGovernor contract.|
|`thresholdRatio_`|`uint16`|  The initial threshold ratio.|


### setThresholdRatio

Sets the threshold ratio to use going forward for newly created proposals.


```solidity
function setThresholdRatio(uint16 newThresholdRatio_) external onlyZeroGovernor;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`newThresholdRatio_`|`uint16`||


### addToList

One of the valid proposals. Adds `account` to `list` at the Registrar.


```solidity
function addToList(bytes32 list_, address account_) external onlySelf;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`list_`|`bytes32`||
|`account_`|`address`||


### removeFromList

One of the valid proposals. Removes `account` to `list` at the Registrar.


```solidity
function removeFromList(bytes32 list_, address account_) external onlySelf;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`list_`|`bytes32`||
|`account_`|`address`||


### removeFromAndAddToList

One of the valid proposals. Removes `accountToRemove` and adds `accountToAdd` to `list` at the Registrar.


```solidity
function removeFromAndAddToList(bytes32 list_, address accountToRemove_, address accountToAdd_) external onlySelf;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`list_`|`bytes32`||
|`accountToRemove_`|`address`||
|`accountToAdd_`|`address`||


### setKey

One of the valid proposals. Sets `key` to `value` at the Registrar.


```solidity
function setKey(bytes32 key_, bytes32 value_) external onlySelf;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`key_`|`bytes32`||
|`value_`|`bytes32`||


### setStandardProposalFee

One of the valid proposals. Sets the proposal fee of the Standard Governor.


```solidity
function setStandardProposalFee(uint256 newProposalFee_) external onlySelf;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`newProposalFee_`|`uint256`||


### _addToList

*Adds `account_` to `list_` at the Registrar.*


```solidity
function _addToList(bytes32 list_, address account_) internal;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`list_`|`bytes32`|   The key for some list.|
|`account_`|`address`|The address of some account to be added.|


### _removeFromList

*Removes `account_` from `list_` at the Registrar.*


```solidity
function _removeFromList(bytes32 list_, address account_) internal;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`list_`|`bytes32`|   The key for some list.|
|`account_`|`address`|The address of some account to be removed.|


### _revertIfInvalidCalldata

*All proposals target this contract itself, and must call one of the listed functions to be valid.*


```solidity
function _revertIfInvalidCalldata(bytes memory callData_) internal pure override;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`callData_`|`bytes`|The call data to check.|


