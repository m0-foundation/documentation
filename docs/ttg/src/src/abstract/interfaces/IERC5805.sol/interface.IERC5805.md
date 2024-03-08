# IERC5805
[Git Source](https://github.com/MZero-Labs/ttg/blob/0d2761f8db14b390e923f59bdae9799fbf9adf2c/src/abstract/interfaces/IERC5805.sol)

**Inherits:**
IStatefulERC712, [IERC6372](/src/abstract/interfaces/IERC6372.sol/interface.IERC6372.md)

**Author:**
M^0 Labs

*The interface as defined by EIP-5805: https://eips.ethereum.org/EIPS/eip-5805*


## Functions
### delegate

Allows a calling account to change its voting power delegation to `delegatee`.


```solidity
function delegate(address delegatee) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`delegatee`|`address`|The address of the account the caller's voting power will be delegated to.|


### delegateBySig

Changes the signing account's voting power delegation to `delegatee`.


```solidity
function delegateBySig(address delegatee, uint256 nonce, uint256 expiry, uint8 v, bytes32 r, bytes32 s) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`delegatee`|`address`|The address of the account the signing account's voting power will be delegated to.|
|`nonce`|`uint256`|    The nonce of the account delegating.|
|`expiry`|`uint256`|   The last block number where the signature is still valid.|
|`v`|`uint8`|        A signature parameter.|
|`r`|`bytes32`|        A signature parameter.|
|`s`|`bytes32`|        A signature parameter.|


### DELEGATION_TYPEHASH

Returns the EIP712 typehash used in the encoding of the digest for the delegateBySig function.


```solidity
function DELEGATION_TYPEHASH() external view returns (bytes32);
```

### delegates

Returns the delegatee the voting power of `account` is delegated to.


```solidity
function delegates(address account) external view returns (address);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account`|`address`|The address of the account that can delegate its voting power.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`address`|The address of the account the voting power of `account` will be delegated to.|


### getPastVotes

Returns the total voting power of `account` at a past clock value `timepoint`.


```solidity
function getPastVotes(address account, uint256 timepoint) external view returns (uint256);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account`|`address`|  The address of some account.|
|`timepoint`|`uint256`|The point in time, according to the clock mode the contract is operating on.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint256`|The total voting power of `account` at clock value `timepoint`.|


### getVotes

Returns the total voting power of `account`.


```solidity
function getVotes(address account) external view returns (uint256);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account`|`address`|The address of some account.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint256`|The total voting power of `account`.|


## Events
### DelegateChanged
Emitted when `delegator` changes its voting power delegation from `fromDelegatee` to `toDelegatee`.


```solidity
event DelegateChanged(address indexed delegator, address indexed fromDelegatee, address indexed toDelegatee);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`delegator`|`address`|    The address of the account changing its voting power delegation.|
|`fromDelegatee`|`address`|The previous account the voting power of `delegator` was delegated to.|
|`toDelegatee`|`address`|  The new account the voting power of `delegator` is delegated to.|

### DelegateVotesChanged
Emitted when the available voting power of `delegatee` changes from `previousBalance` to `newBalance`.


```solidity
event DelegateVotesChanged(address indexed delegatee, uint256 previousBalance, uint256 newBalance);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`delegatee`|`address`|      The address of the account whose voting power is changed.|
|`previousBalance`|`uint256`|The previous voting power of `delegatee`.|
|`newBalance`|`uint256`|     The new voting power of `delegatee`.|

## Errors
### NotPastTimepoint
Revert message when a query for past values is for a timepoint greater or equal to the current clock.


```solidity
error NotPastTimepoint(uint48 timepoint, uint48 clock);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`timepoint`|`uint48`|The timepoint being queried.|
|`clock`|`uint48`|    The current timepoint.|

