# IPowerBootstrapToken
[Git Source](https://github.com/MZero-Labs/ttg/blob/0d2761f8db14b390e923f59bdae9799fbf9adf2c/src/interfaces/IPowerBootstrapToken.sol)

**Author:**
M^0 Labs


## Functions
### pastBalanceOf

Returns the token balance of `account` at a past clock value `epoch`.


```solidity
function pastBalanceOf(address account, uint256 epoch) external view returns (uint256);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account`|`address`|The address of some account.|
|`epoch`|`uint256`|  The epoch number as a clock value.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint256`|The token balance `account` at `epoch`.|


### pastTotalSupply

Returns the total token supply at a past clock value `epoch`.


```solidity
function pastTotalSupply(uint256 epoch) external view returns (uint256);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`epoch`|`uint256`|The epoch number as a clock value.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint256`|The total token supply at `epoch`.|


## Errors
### ArrayLengthMismatch
Revert message when the length of some accounts array does not equal the length of some balances array.


```solidity
error ArrayLengthMismatch(uint256 accountsLength, uint256 balancesLength);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`accountsLength`|`uint256`|The length of the accounts array.|
|`balancesLength`|`uint256`|The length of the balances array.|

### TotalSupplyTooLarge
Revert message when the total supply is larger than `type(uint240).max`, rendering the contract
incompatible as a bootstrap token for the PowerToken.


```solidity
error TotalSupplyTooLarge();
```

