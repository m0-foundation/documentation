# PowerBootstrapToken
[Git Source](https://github.com/MZero-Labs/ttg/blob/0d2761f8db14b390e923f59bdae9799fbf9adf2c/src/PowerBootstrapToken.sol)

**Inherits:**
[IPowerBootstrapToken](/src/interfaces/IPowerBootstrapToken.sol/interface.IPowerBootstrapToken.md)

**Author:**
M^0 Labs

*The timepoints queried is ignored as this token is not time-dependent.*


## State Variables
### _totalSupply
*The total supply of token.*


```solidity
uint256 internal immutable _totalSupply;
```


### _balances
*Mapping to keep track of token balances per account.*


```solidity
mapping(address account => uint256 balance) internal _balances;
```


## Functions
### constructor

Constructs a new PowerBootstrapToken contract.


```solidity
constructor(address[] memory initialAccounts_, uint256[] memory initialBalances_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`initialAccounts_`|`address[]`|The initial accounts to mint tokens to.|
|`initialBalances_`|`uint256[]`|The initial token balances to mint to each accounts.|


### pastBalanceOf

Returns the token balance of `account` at a past clock value `epoch`.


```solidity
function pastBalanceOf(address account_, uint256) external view returns (uint256);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account_`|`address`||
|`<none>`|`uint256`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint256`|The token balance `account` at `epoch`.|


### pastTotalSupply

Returns the total token supply at a past clock value `epoch`.


```solidity
function pastTotalSupply(uint256) external view returns (uint256);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint256`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint256`|The total token supply at `epoch`.|


