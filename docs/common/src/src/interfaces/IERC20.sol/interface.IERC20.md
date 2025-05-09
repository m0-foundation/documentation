# IERC20
[Git Source](https://github.com/MZero-Labs/common/blob/9da96e78d24aadd41ee6f776b7b028203782b632/src/interfaces/IERC20.sol)

**Author:**
M^0 Labs

*The interface as defined by EIP-20: https://eips.ethereum.org/EIPS/eip-20*


## Functions
### approve

Allows a calling account to approve `spender` to spend up to `amount` of its token balance.

*MUST emit an `Approval` event.*


```solidity
function approve(address spender, uint256 amount) external returns (bool);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`spender`|`address`|The address of the account is allowed to spend up to the allowed amount.|
|`amount`|`uint256`| The amount of the allowance being approved.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bool`|Whether or not the approval was successful.|


### transfer

Allows a calling account to transfer `amount` tokens to `recipient`.


```solidity
function transfer(address recipient, uint256 amount) external returns (bool);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`recipient`|`address`|The address of the recipient who's token balance will be incremented.|
|`amount`|`uint256`|   The amount of tokens being transferred.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bool`|Whether or not the transfer was successful.|


### transferFrom

Allows a calling account to transfer `amount` tokens from `sender`, with allowance, to a `recipient`.


```solidity
function transferFrom(address sender, address recipient, uint256 amount) external returns (bool);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`sender`|`address`|   The address of the sender who's token balance will be decremented.|
|`recipient`|`address`|The address of the recipient who's token balance will be incremented.|
|`amount`|`uint256`|   The amount of tokens being transferred.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bool`|Whether or not the transfer was successful.|


### allowance

Returns the allowance `spender` is allowed to spend on behalf of `account`.


```solidity
function allowance(address account, address spender) external view returns (uint256);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account`|`address`|The address of the account who's token balance `spender` is allowed to spend.|
|`spender`|`address`|The address of an account allowed to spend on behalf of `account`.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint256`|The amount `spender` can spend on behalf of `account`.|


### balanceOf

Returns the token balance of `account`.


```solidity
function balanceOf(address account) external view returns (uint256);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account`|`address`|The address of some account.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint256`|The token balance of `account`.|


### decimals

Returns the number of decimals UIs should assume all amounts have.


```solidity
function decimals() external view returns (uint8);
```

### name

Returns the name of the contract/token.


```solidity
function name() external view returns (string memory);
```

### symbol

Returns the symbol of the token.


```solidity
function symbol() external view returns (string memory);
```

### totalSupply

Returns the current total supply of the token.


```solidity
function totalSupply() external view returns (uint256);
```

## Events
### Approval
Emitted when `spender` has been approved for `amount` of the token balance of `account`.


```solidity
event Approval(address indexed account, address indexed spender, uint256 amount);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account`|`address`|The address of the account.|
|`spender`|`address`|The address of the spender being approved for the allowance.|
|`amount`|`uint256`| The amount of the allowance being approved.|

### Transfer
Emitted when `amount` tokens is transferred from `sender` to `recipient`.


```solidity
event Transfer(address indexed sender, address indexed recipient, uint256 amount);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`sender`|`address`|   The address of the sender who's token balance is decremented.|
|`recipient`|`address`|The address of the recipient who's token balance is incremented.|
|`amount`|`uint256`|   The amount of tokens being transferred.|

