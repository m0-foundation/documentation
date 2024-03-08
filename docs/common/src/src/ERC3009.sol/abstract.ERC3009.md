# ERC3009
[Git Source](https://github.com/MZero-Labs/common/blob/9da96e78d24aadd41ee6f776b7b028203782b632/src/ERC3009.sol)

**Inherits:**
[IERC3009](/src/interfaces/IERC3009.sol/interface.IERC3009.md), [StatefulERC712](/src/StatefulERC712.sol/abstract.StatefulERC712.md)

**Author:**
M^0 Labs

*Inherits from ERC712 and StatefulERC712.*


## State Variables
### TRANSFER_WITH_AUTHORIZATION_TYPEHASH
Returns `transferWithAuthorization` typehash.

*keccak256("TransferWithAuthorization(address from,address to,uint256 value,uint256 validAfter,uint256 validBefore,bytes32 nonce)")*


```solidity
bytes32 public constant TRANSFER_WITH_AUTHORIZATION_TYPEHASH =
    0x7c7c6cdb67a18743f49ec6fa9b35f50d52ed05cbed4cc592e13b44501c1a2267;
```


### RECEIVE_WITH_AUTHORIZATION_TYPEHASH
Returns `receiveWithAuthorization` typehash.

*keccak256("ReceiveWithAuthorization(address from,address to,uint256 value,uint256 validAfter,uint256 validBefore,bytes32 nonce)")*


```solidity
bytes32 public constant RECEIVE_WITH_AUTHORIZATION_TYPEHASH =
    0xd099cc98ef71107a616c4f0f941f04c322d8e254fe26b3c6668db87aae413de8;
```


### CANCEL_AUTHORIZATION_TYPEHASH
Returns `cancelAuthorization` typehash.

*keccak256("CancelAuthorization(address authorizer,bytes32 nonce)")*


```solidity
bytes32 public constant CANCEL_AUTHORIZATION_TYPEHASH =
    0x158b0a9edf7a828aad02f63cd515c68ef2f50ba807396f6d12842833a1597429;
```


### authorizationState
Returns the state of an authorization.

*Nonces are randomly generated 32-byte data unique to the authorizer's address*


```solidity
mapping(address authorizer => mapping(bytes32 nonce => bool isNonceUsed)) public authorizationState;
```


## Functions
### constructor

Construct the ERC3009 contract.


```solidity
constructor(string memory name_) StatefulERC712(name_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`name_`|`string`|The name of the contract.|


### transferWithAuthorization

Execute a transfer with a signed authorization.


```solidity
function transferWithAuthorization(
    address from_,
    address to_,
    uint256 value_,
    uint256 validAfter_,
    uint256 validBefore_,
    bytes32 nonce_,
    bytes memory signature_
) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`from_`|`address`||
|`to_`|`address`||
|`value_`|`uint256`||
|`validAfter_`|`uint256`||
|`validBefore_`|`uint256`||
|`nonce_`|`bytes32`||
|`signature_`|`bytes`||


### transferWithAuthorization

Execute a transfer with a signed authorization.


```solidity
function transferWithAuthorization(
    address from_,
    address to_,
    uint256 value_,
    uint256 validAfter_,
    uint256 validBefore_,
    bytes32 nonce_,
    bytes32 r_,
    bytes32 vs_
) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`from_`|`address`||
|`to_`|`address`||
|`value_`|`uint256`||
|`validAfter_`|`uint256`||
|`validBefore_`|`uint256`||
|`nonce_`|`bytes32`||
|`r_`|`bytes32`||
|`vs_`|`bytes32`||


### transferWithAuthorization

Execute a transfer with a signed authorization.


```solidity
function transferWithAuthorization(
    address from_,
    address to_,
    uint256 value_,
    uint256 validAfter_,
    uint256 validBefore_,
    bytes32 nonce_,
    uint8 v_,
    bytes32 r_,
    bytes32 s_
) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`from_`|`address`||
|`to_`|`address`||
|`value_`|`uint256`||
|`validAfter_`|`uint256`||
|`validBefore_`|`uint256`||
|`nonce_`|`bytes32`||
|`v_`|`uint8`||
|`r_`|`bytes32`||
|`s_`|`bytes32`||


### receiveWithAuthorization

Receive a transfer with a signed authorization from the payer.

*This has an additional check to ensure that the payee's address matches
the caller of this function to prevent front-running attacks.
(See security considerations)*


```solidity
function receiveWithAuthorization(
    address from_,
    address to_,
    uint256 value_,
    uint256 validAfter_,
    uint256 validBefore_,
    bytes32 nonce_,
    bytes memory signature_
) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`from_`|`address`||
|`to_`|`address`||
|`value_`|`uint256`||
|`validAfter_`|`uint256`||
|`validBefore_`|`uint256`||
|`nonce_`|`bytes32`||
|`signature_`|`bytes`||


### receiveWithAuthorization

Receive a transfer with a signed authorization from the payer.

*This has an additional check to ensure that the payee's address matches
the caller of this function to prevent front-running attacks.
(See security considerations)*


```solidity
function receiveWithAuthorization(
    address from_,
    address to_,
    uint256 value_,
    uint256 validAfter_,
    uint256 validBefore_,
    bytes32 nonce_,
    bytes32 r_,
    bytes32 vs_
) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`from_`|`address`||
|`to_`|`address`||
|`value_`|`uint256`||
|`validAfter_`|`uint256`||
|`validBefore_`|`uint256`||
|`nonce_`|`bytes32`||
|`r_`|`bytes32`||
|`vs_`|`bytes32`||


### receiveWithAuthorization

Receive a transfer with a signed authorization from the payer.

*This has an additional check to ensure that the payee's address matches
the caller of this function to prevent front-running attacks.
(See security considerations)*


```solidity
function receiveWithAuthorization(
    address from_,
    address to_,
    uint256 value_,
    uint256 validAfter_,
    uint256 validBefore_,
    bytes32 nonce_,
    uint8 v_,
    bytes32 r_,
    bytes32 s_
) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`from_`|`address`||
|`to_`|`address`||
|`value_`|`uint256`||
|`validAfter_`|`uint256`||
|`validBefore_`|`uint256`||
|`nonce_`|`bytes32`||
|`v_`|`uint8`||
|`r_`|`bytes32`||
|`s_`|`bytes32`||


### cancelAuthorization

Attempt to cancel an authorization.


```solidity
function cancelAuthorization(address authorizer_, bytes32 nonce_, bytes memory signature_) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`authorizer_`|`address`||
|`nonce_`|`bytes32`||
|`signature_`|`bytes`||


### cancelAuthorization

Attempt to cancel an authorization.


```solidity
function cancelAuthorization(address authorizer_, bytes32 nonce_, bytes32 r_, bytes32 vs_) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`authorizer_`|`address`||
|`nonce_`|`bytes32`||
|`r_`|`bytes32`||
|`vs_`|`bytes32`||


### cancelAuthorization

Attempt to cancel an authorization.


```solidity
function cancelAuthorization(address authorizer_, bytes32 nonce_, uint8 v_, bytes32 r_, bytes32 s_) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`authorizer_`|`address`||
|`nonce_`|`bytes32`||
|`v_`|`uint8`||
|`r_`|`bytes32`||
|`s_`|`bytes32`||


### _transferWithAuthorization

*Common transfer function used by `transferWithAuthorization` and `_receiveWithAuthorization`.*


```solidity
function _transferWithAuthorization(
    address from_,
    address to_,
    uint256 value_,
    uint256 validAfter_,
    uint256 validBefore_,
    bytes32 nonce_
) internal;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`from_`|`address`|       Payer's address (Authorizer).|
|`to_`|`address`|         Payee's address.|
|`value_`|`uint256`|      Amount to be transferred.|
|`validAfter_`|`uint256`| The time after which this is valid (unix time).|
|`validBefore_`|`uint256`|The time before which this is valid (unix time).|
|`nonce_`|`bytes32`|      Unique nonce.|


### _receiveWithAuthorization

*Common receive function used by `receiveWithAuthorization`.*


```solidity
function _receiveWithAuthorization(
    address from_,
    address to_,
    uint256 value_,
    uint256 validAfter_,
    uint256 validBefore_,
    bytes32 nonce_
) internal;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`from_`|`address`|       Payer's address (Authorizer).|
|`to_`|`address`|         Payee's address.|
|`value_`|`uint256`|      Amount to be transferred.|
|`validAfter_`|`uint256`| The time after which this is valid (unix time).|
|`validBefore_`|`uint256`|The time before which this is valid (unix time).|
|`nonce_`|`bytes32`|      Unique nonce.|


### _cancelAuthorization

*Common cancel function used by `cancelAuthorization`.*


```solidity
function _cancelAuthorization(address authorizer_, bytes32 nonce_) internal;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`authorizer_`|`address`|Authorizer's address.|
|`nonce_`|`bytes32`|     Nonce of the authorization.|


### _transfer

*Internal ERC20 transfer function that needs to be implemented by the inheriting contract.*


```solidity
function _transfer(address sender_, address recipient_, uint256 amount_) internal virtual;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`sender_`|`address`|   The sender's address.|
|`recipient_`|`address`|The recipient's address.|
|`amount_`|`uint256`|   The amount to be transferred.|


### _getTransferWithAuthorizationDigest

*Returns the internal EIP-712 digest of a transferWithAuthorization call.*


```solidity
function _getTransferWithAuthorizationDigest(
    address from_,
    address to_,
    uint256 value_,
    uint256 validAfter_,
    uint256 validBefore_,
    bytes32 nonce_
) internal view returns (bytes32);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`from_`|`address`|       Payer's address (Authorizer).|
|`to_`|`address`|         Payee's address.|
|`value_`|`uint256`|      Amount to be transferred.|
|`validAfter_`|`uint256`| The time after which this is valid (unix time).|
|`validBefore_`|`uint256`|The time before which this is valid (unix time).|
|`nonce_`|`bytes32`|      Unique nonce.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bytes32`|The internal EIP-712 digest.|


### _getReceiveWithAuthorizationDigest

*Returns the internal EIP-712 digest of a receiveWithAuthorization call.*


```solidity
function _getReceiveWithAuthorizationDigest(
    address from_,
    address to_,
    uint256 value_,
    uint256 validAfter_,
    uint256 validBefore_,
    bytes32 nonce_
) internal view returns (bytes32);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`from_`|`address`|       Payer's address (Authorizer).|
|`to_`|`address`|         Payee's address.|
|`value_`|`uint256`|      Amount to be transferred.|
|`validAfter_`|`uint256`| The time after which this is valid (unix time).|
|`validBefore_`|`uint256`|The time before which this is valid (unix time).|
|`nonce_`|`bytes32`|      Unique nonce.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bytes32`|The internal EIP-712 digest.|


### _getCancelAuthorizationDigest

*Returns the internal EIP-712 digest of a cancelAuthorization call.*


```solidity
function _getCancelAuthorizationDigest(address authorizer_, bytes32 nonce_) internal view returns (bytes32);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`authorizer_`|`address`|Authorizer's address.|
|`nonce_`|`bytes32`|     Nonce of the authorization.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bytes32`|The internal EIP-712 digest.|


### _revertIfAuthorizationAlreadyUsed

*Reverts if the authorization is already used.*


```solidity
function _revertIfAuthorizationAlreadyUsed(address authorizer_, bytes32 nonce_) internal view;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`authorizer_`|`address`|The authorizer's address.|
|`nonce_`|`bytes32`|     The nonce of the authorization.|


