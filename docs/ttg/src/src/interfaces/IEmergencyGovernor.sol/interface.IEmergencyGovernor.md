# IEmergencyGovernor
[Git Source](https://github.com/MZero-Labs/ttg/blob/0d2761f8db14b390e923f59bdae9799fbf9adf2c/src/interfaces/IEmergencyGovernor.sol)

**Inherits:**
[IThresholdGovernor](/src/abstract/interfaces/IThresholdGovernor.sol/interface.IThresholdGovernor.md)

**Author:**
M^0 Labs


## Functions
### setThresholdRatio

Sets the threshold ratio to use going forward for newly created proposals.


```solidity
function setThresholdRatio(uint16 newThresholdRatio) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`newThresholdRatio`|`uint16`|The new threshold ratio.|


### addToList

One of the valid proposals. Adds `account` to `list` at the Registrar.


```solidity
function addToList(bytes32 list, address account) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`list`|`bytes32`|   The key for some list.|
|`account`|`address`|The address of some account to be added.|


### removeFromList

One of the valid proposals. Removes `account` to `list` at the Registrar.


```solidity
function removeFromList(bytes32 list, address account) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`list`|`bytes32`|   The key for some list.|
|`account`|`address`|The address of some account to be removed.|


### removeFromAndAddToList

One of the valid proposals. Removes `accountToRemove` and adds `accountToAdd` to `list` at the Registrar.


```solidity
function removeFromAndAddToList(bytes32 list, address accountToRemove, address accountToAdd) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`list`|`bytes32`|           The key for some list.|
|`accountToRemove`|`address`|The address of some account to be removed.|
|`accountToAdd`|`address`|   The address of some account to be added.|


### setKey

One of the valid proposals. Sets `key` to `value` at the Registrar.


```solidity
function setKey(bytes32 key, bytes32 value) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`key`|`bytes32`|  Some key.|
|`value`|`bytes32`|Some value.|


### setStandardProposalFee

One of the valid proposals. Sets the proposal fee of the Standard Governor.


```solidity
function setStandardProposalFee(uint256 newProposalFee) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`newProposalFee`|`uint256`|The new proposal fee.|


### registrar

Returns the address of the Registrar.


```solidity
function registrar() external view returns (address);
```

### standardGovernor

Returns the address of the Standard Governor.


```solidity
function standardGovernor() external view returns (address);
```

### zeroGovernor

Returns the address of the Zero Governor.


```solidity
function zeroGovernor() external view returns (address);
```

## Errors
### InvalidRegistrarAddress
Revert message when the Registrar specified in the constructor is address(0).


```solidity
error InvalidRegistrarAddress();
```

### InvalidStandardGovernorAddress
Revert message when the Standard Governor specified in the constructor is address(0).


```solidity
error InvalidStandardGovernorAddress();
```

### InvalidZeroGovernorAddress
Revert message when the Zero Governor specified in the constructor is address(0).


```solidity
error InvalidZeroGovernorAddress();
```

### NotZeroGovernor
Revert message when the caller is not the Zero Governor.


```solidity
error NotZeroGovernor();
```

