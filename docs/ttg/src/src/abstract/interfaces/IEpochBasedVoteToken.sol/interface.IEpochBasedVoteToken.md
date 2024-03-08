# IEpochBasedVoteToken
[Git Source](https://github.com/MZero-Labs/ttg/blob/0d2761f8db14b390e923f59bdae9799fbf9adf2c/src/abstract/interfaces/IEpochBasedVoteToken.sol)

**Inherits:**
[IERC5805](/src/abstract/interfaces/IERC5805.sol/interface.IERC5805.md), IERC20Extended

**Author:**
M^0 Labs


## Functions
### delegateBySig

Changes the voting power delegation for `account` to `delegatee`.


```solidity
function delegateBySig(address account, address delegatee, uint256 nonce, uint256 expiry, bytes memory signature)
    external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account`|`address`|  The purported address of the signing account.|
|`delegatee`|`address`|The address the voting power of `account` will be delegated to.|
|`nonce`|`uint256`|    The nonce used for the signature.|
|`expiry`|`uint256`|   The last block number where the signature is still valid.|
|`signature`|`bytes`|A byte array signature.|


### getDelegationDigest

Returns the digest to be signed, via EIP-712, given an internal digest (i.e. hash struct).


```solidity
function getDelegationDigest(address delegatee, uint256 nonce, uint256 expiry) external view returns (bytes32);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`delegatee`|`address`|The address of the delegatee to delegate to.|
|`nonce`|`uint256`|    The nonce of the account delegating.|
|`expiry`|`uint256`|   The last timestamp at which the signature is still valid.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bytes32`|The digest to be signed.|


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


### pastDelegates

Returns the delegatee of `account` at a past clock value `epoch`.


```solidity
function pastDelegates(address account, uint256 epoch) external view returns (address);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account`|`address`|The address of some account.|
|`epoch`|`uint256`|  The epoch number as a clock value.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`address`|The delegatee of the voting power of `account` at `epoch`.|


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
### EpochZero
Revert message when the provided epoch is zero.


```solidity
error EpochZero();
```

