# ERC5805
[Git Source](https://github.com/MZero-Labs/ttg/blob/0d2761f8db14b390e923f59bdae9799fbf9adf2c/src/abstract/ERC5805.sol)

**Inherits:**
[IERC5805](/src/abstract/interfaces/IERC5805.sol/interface.IERC5805.md), StatefulERC712

**Author:**
M^0 Labs


## State Variables
### DELEGATION_TYPEHASH
Returns the EIP712 typehash used in the encoding of the digest for the delegateBySig function.

*Keeping this constant, despite `delegateBySig` param name differences, to ensure max EIP-5805 compatibility.
keccak256("Delegation(address delegatee,uint256 nonce,uint256 expiry)")*


```solidity
bytes32 public constant DELEGATION_TYPEHASH = 0xe48329057bfd03d55e49b547132e39cffd9c1820ad7b9d4c5307691425d15adf;
```


## Functions
### delegate

Allows a calling account to change its voting power delegation to `delegatee`.


```solidity
function delegate(address delegatee_) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`delegatee_`|`address`||


### delegateBySig

Changes the signing account's voting power delegation to `delegatee`.


```solidity
function delegateBySig(address delegatee_, uint256 nonce_, uint256 expiry_, uint8 v_, bytes32 r_, bytes32 s_)
    external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`delegatee_`|`address`||
|`nonce_`|`uint256`||
|`expiry_`|`uint256`||
|`v_`|`uint8`||
|`r_`|`bytes32`||
|`s_`|`bytes32`||


### _checkAndIncrementNonce

*Reverts if a given `nonce_` is reused for `account_`, then increments the nonce in storage.*


```solidity
function _checkAndIncrementNonce(address account_, uint256 nonce_) internal;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account_`|`address`|The address of the account the nonce is being verified for.|
|`nonce_`|`uint256`|  The nonce being used by the account.|


### _delegate

*Delegate voting power from `delegator_` to `newDelegatee_`.*


```solidity
function _delegate(address delegator_, address newDelegatee_) internal virtual;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`delegator_`|`address`|   The address of the account delegating voting power.|
|`newDelegatee_`|`address`|The address of the account receiving voting power.|


### _getDelegationDigest

*Returns the digest to be signed, via EIP-712, given an internal digest (i.e. hash struct).*


```solidity
function _getDelegationDigest(address delegatee_, uint256 nonce_, uint256 expiry_) internal view returns (bytes32);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`delegatee_`|`address`|The address of the delegatee to delegate to.|
|`nonce_`|`uint256`|    The nonce of the account delegating.|
|`expiry_`|`uint256`|   The last timestamp at which the signature is still valid.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bytes32`|The digest to be signed.|


