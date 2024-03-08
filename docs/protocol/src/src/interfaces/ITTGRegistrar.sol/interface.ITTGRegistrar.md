# ITTGRegistrar
[Git Source](https://github.com/MZero-Labs/protocol/blob/3382fb7336bbc7276e0c3f51da451c9fa6e0016f/src/interfaces/ITTGRegistrar.sol)

**Author:**
M^0 Labs


## Functions
### get

Key value pair getter.


```solidity
function get(bytes32 key) external view returns (bytes32 value);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`key`|`bytes32`|The key to get the value of.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`value`|`bytes32`|The value of the key.|


### listContains

Checks if the list contains the account.


```solidity
function listContains(bytes32 list, address account) external view returns (bool);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`list`|`bytes32`|The list to check.|
|`account`|`address`|The account to check.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bool`|True if the list contains the account, false otherwise.|


### vault

Returns the vault contract address.


```solidity
function vault() external view returns (address);
```

