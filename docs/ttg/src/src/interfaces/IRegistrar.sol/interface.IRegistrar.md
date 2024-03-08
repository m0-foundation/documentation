# IRegistrar
[Git Source](https://github.com/MZero-Labs/ttg/blob/0d2761f8db14b390e923f59bdae9799fbf9adf2c/src/interfaces/IRegistrar.sol)

**Author:**
M^0 Labs


## Functions
### addToList

Adds `account` to `list`.


```solidity
function addToList(bytes32 list, address account) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`list`|`bytes32`|   The key for some list.|
|`account`|`address`|The address of some account to be added.|


### removeFromList

Removes `account` from `list`.


```solidity
function removeFromList(bytes32 list, address account) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`list`|`bytes32`|   The key for some list.|
|`account`|`address`|The address of some account to be removed.|


### setKey

Sets `key` to `value`.


```solidity
function setKey(bytes32 key, bytes32 value) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`key`|`bytes32`|  Some key.|
|`value`|`bytes32`|Some value.|


### get

Returns the value of `key`.


```solidity
function get(bytes32 key) external view returns (bytes32);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`key`|`bytes32`|Some key.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bytes32`|Some value.|


### get

Returns the values of `keys` respectively.


```solidity
function get(bytes32[] calldata keys) external view returns (bytes32[] memory);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`keys`|`bytes32[]`|Some keys.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bytes32[]`|Some values.|


### listContains

Returns whether `list` contains `account`.


```solidity
function listContains(bytes32 list, address account) external view returns (bool);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`list`|`bytes32`|   The key for some list.|
|`account`|`address`|The address of some account.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bool`|Whether `list` contains `account`.|


### listContains

Returns whether `list` contains all specified accounts.


```solidity
function listContains(bytes32 list, address[] calldata accounts) external view returns (bool);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`list`|`bytes32`|    The key for some list.|
|`accounts`|`address[]`|An array of addressed of some accounts.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bool`|Whether `list` contains all specified accounts.|


### emergencyGovernor

Returns the address of the Emergency Governor.


```solidity
function emergencyGovernor() external view returns (address);
```

### emergencyGovernorDeployer

Returns the address of the Emergency Governor Deployer.


```solidity
function emergencyGovernorDeployer() external view returns (address);
```

### powerToken

Returns the address of the Power Token.


```solidity
function powerToken() external view returns (address);
```

### powerTokenDeployer

Returns the address of the Power Token Deployer.


```solidity
function powerTokenDeployer() external view returns (address);
```

### standardGovernor

Returns the address of the Standard Governor.


```solidity
function standardGovernor() external view returns (address);
```

### standardGovernorDeployer

Returns the address of the Standard Governor Deployer.


```solidity
function standardGovernorDeployer() external view returns (address);
```

### vault

Returns the address of the Vault.


```solidity
function vault() external view returns (address);
```

### zeroGovernor

Returns the address of the Zero Governor.


```solidity
function zeroGovernor() external view returns (address);
```

### zeroToken

Returns the address of the Zero Token.


```solidity
function zeroToken() external view returns (address);
```

## Events
### AddressAddedToList
Emitted when `account` is added to `list`.


```solidity
event AddressAddedToList(bytes32 indexed list, address indexed account);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`list`|`bytes32`|   The key for the list.|
|`account`|`address`|The address of the added account.|

### AddressRemovedFromList
Emitted when `account` is removed from `list`.


```solidity
event AddressRemovedFromList(bytes32 indexed list, address indexed account);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`list`|`bytes32`|   The key for the list.|
|`account`|`address`|The address of the removed account.|

### KeySet
Emitted when `key` is set to `value`.


```solidity
event KeySet(bytes32 indexed key, bytes32 indexed value);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`key`|`bytes32`|  The key.|
|`value`|`bytes32`|The value.|

## Errors
### InvalidEmergencyGovernorDeployerAddress
Revert message when the Emergency Governor Deployer retrieved in the constructor is address(0).


```solidity
error InvalidEmergencyGovernorDeployerAddress();
```

### InvalidPowerTokenDeployerAddress
Revert message when the Power Token Deployer retrieved in the constructor is address(0).


```solidity
error InvalidPowerTokenDeployerAddress();
```

### InvalidStandardGovernorDeployerAddress
Revert message when the Standard Governor Deployer retrieved in the constructor is address(0).


```solidity
error InvalidStandardGovernorDeployerAddress();
```

### InvalidVaultAddress
Revert message when the Vault retrieved in the constructor is address(0).


```solidity
error InvalidVaultAddress();
```

### InvalidVoteTokenAddress
Revert message when the Vote Token retrieved in the constructor is address(0).


```solidity
error InvalidVoteTokenAddress();
```

### InvalidZeroGovernorAddress
Revert message when the Zero Governor specified in the constructor is address(0).


```solidity
error InvalidZeroGovernorAddress();
```

### NotStandardOrEmergencyGovernor
Revert message when the caller is not the Standard Governor nor the Emergency Governor.


```solidity
error NotStandardOrEmergencyGovernor();
```

