# IStatefulERC712
[Git Source](https://github.com/MZero-Labs/common/blob/9da96e78d24aadd41ee6f776b7b028203782b632/src/interfaces/IStatefulERC712.sol)

**Inherits:**
[IERC712Extended](/src/interfaces/IERC712Extended.sol/interface.IERC712Extended.md)

**Author:**
M^0 Labs


## Functions
### nonces

Returns the next nonce to be used in a signature by `account`.


```solidity
function nonces(address account) external view returns (uint256 nonce);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account`|`address`|The address of some account.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`nonce`|`uint256`|  The next nonce to be used in a signature by `account`.|


## Errors
### InvalidAccountNonce
Revert message when a signing account's nonce is not the expected current nonce.


```solidity
error InvalidAccountNonce(uint256 nonce, uint256 expectedNonce);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`nonce`|`uint256`|        The nonce used in the signature.|
|`expectedNonce`|`uint256`|The expected nonce to be used in a signature by the signing account.|

