# Registrar
[Git Source](https://github.com/MZero-Labs/ttg/blob/0d2761f8db14b390e923f59bdae9799fbf9adf2c/src/Registrar.sol)

**Inherits:**
[IRegistrar](/src/interfaces/IRegistrar.sol/interface.IRegistrar.md)

**Author:**
M^0 Labs


## State Variables
### emergencyGovernorDeployer
Returns the address of the Emergency Governor Deployer.


```solidity
address public immutable emergencyGovernorDeployer;
```


### powerTokenDeployer
Returns the address of the Power Token Deployer.


```solidity
address public immutable powerTokenDeployer;
```


### standardGovernorDeployer
Returns the address of the Standard Governor Deployer.


```solidity
address public immutable standardGovernorDeployer;
```


### vault
Returns the address of the Vault.


```solidity
address public immutable vault;
```


### zeroGovernor
Returns the address of the Zero Governor.


```solidity
address public immutable zeroGovernor;
```


### zeroToken
Returns the address of the Zero Token.


```solidity
address public immutable zeroToken;
```


### _valueAt
*A mapping of keys to values.*


```solidity
mapping(bytes32 key => bytes32 value) internal _valueAt;
```


## Functions
### onlyStandardOrEmergencyGovernor

*Revert if the caller is not the Standard Governor nor the Emergency Governor.*


```solidity
modifier onlyStandardOrEmergencyGovernor();
```

### constructor

Constructs a new Registrar contract.


```solidity
constructor(address zeroGovernor_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`zeroGovernor_`|`address`|The address of the ZeroGovernor contract.|


### addToList

Adds `account` to `list`.


```solidity
function addToList(bytes32 list_, address account_) external onlyStandardOrEmergencyGovernor;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`list_`|`bytes32`||
|`account_`|`address`||


### removeFromList

Removes `account` from `list`.


```solidity
function removeFromList(bytes32 list_, address account_) external onlyStandardOrEmergencyGovernor;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`list_`|`bytes32`||
|`account_`|`address`||


### setKey

Sets `key` to `value`.


```solidity
function setKey(bytes32 key_, bytes32 value_) external onlyStandardOrEmergencyGovernor;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`key_`|`bytes32`||
|`value_`|`bytes32`||


### get

Returns the value of `key`.


```solidity
function get(bytes32 key_) external view returns (bytes32);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`key_`|`bytes32`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bytes32`|Some value.|


### get

Returns the value of `key`.


```solidity
function get(bytes32[] calldata keys_) external view returns (bytes32[] memory values_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`keys_`|`bytes32[]`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`values_`|`bytes32[]`|Some value.|


### listContains

Returns whether `list` contains `account`.


```solidity
function listContains(bytes32 list_, address account_) external view returns (bool);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`list_`|`bytes32`||
|`account_`|`address`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bool`|Whether `list` contains `account`.|


### listContains

Returns whether `list` contains `account`.


```solidity
function listContains(bytes32 list_, address[] calldata accounts_) external view returns (bool);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`list_`|`bytes32`||
|`accounts_`|`address[]`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bool`|Whether `list` contains `account`.|


### powerToken

Returns the address of the Power Token.


```solidity
function powerToken() external view returns (address);
```

### emergencyGovernor

Returns the address of the Emergency Governor.


```solidity
function emergencyGovernor() public view returns (address);
```

### standardGovernor

Returns the address of the Standard Governor.


```solidity
function standardGovernor() public view returns (address);
```

### _revertIfNotStandardOrEmergencyGovernor

*Reverts if the caller is not the Standard Governor nor the Emergency Governor.*


```solidity
function _revertIfNotStandardOrEmergencyGovernor() internal view;
```

### _getValueKey

*Returns the key used to store the value of `key_`.*


```solidity
function _getValueKey(bytes32 key_) internal pure returns (bytes32);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`key_`|`bytes32`|The key of the value.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bytes32`|The key used to store the value of `key_`.|


### _getIsInListKey

*Returns the key used to store whether `account_` is in `list_`.*


```solidity
function _getIsInListKey(bytes32 list_, address account_) internal pure returns (bytes32);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`list_`|`bytes32`|   The list of addresses.|
|`account_`|`address`|The address of the account.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bytes32`|The key used to store whether `account_` is in `list_`.|


