# IERC3009
[Git Source](https://github.com/MZero-Labs/common/blob/9da96e78d24aadd41ee6f776b7b028203782b632/src/interfaces/IERC3009.sol)

**Inherits:**
[IStatefulERC712](/src/interfaces/IStatefulERC712.sol/interface.IStatefulERC712.md)

**Author:**
M^0 Labs

*The interface as defined by EIP-3009: https://eips.ethereum.org/EIPS/eip-3009*


## Functions
### transferWithAuthorization

Execute a transfer with a signed authorization.


```solidity
function transferWithAuthorization(
    address from,
    address to,
    uint256 value,
    uint256 validAfter,
    uint256 validBefore,
    bytes32 nonce,
    bytes memory signature
) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`from`|`address`|       Payer's address (Authorizer).|
|`to`|`address`|         Payee's address.|
|`value`|`uint256`|      Amount to be transferred.|
|`validAfter`|`uint256`| The time after which this is valid (unix time).|
|`validBefore`|`uint256`|The time before which this is valid (unix time).|
|`nonce`|`bytes32`|      Unique nonce.|
|`signature`|`bytes`|  A byte array ECDSA/secp256k1 signature (encoded r, s, v).|


### transferWithAuthorization

Execute a transfer with a signed authorization.


```solidity
function transferWithAuthorization(
    address from,
    address to,
    uint256 value,
    uint256 validAfter,
    uint256 validBefore,
    bytes32 nonce,
    bytes32 r,
    bytes32 vs
) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`from`|`address`|       Payer's address (Authorizer).|
|`to`|`address`|         Payee's address.|
|`value`|`uint256`|      Amount to be transferred.|
|`validAfter`|`uint256`| The time after which this is valid (unix time).|
|`validBefore`|`uint256`|The time before which this is valid (unix time).|
|`nonce`|`bytes32`|      Unique nonce.|
|`r`|`bytes32`|          An ECDSA/secp256k1 signature parameter.|
|`vs`|`bytes32`|         An ECDSA/secp256k1 short signature parameter.|


### transferWithAuthorization

Execute a transfer with a signed authorization.


```solidity
function transferWithAuthorization(
    address from,
    address to,
    uint256 value,
    uint256 validAfter,
    uint256 validBefore,
    bytes32 nonce,
    uint8 v,
    bytes32 r,
    bytes32 s
) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`from`|`address`|       Payer's address (Authorizer).|
|`to`|`address`|         Payee's address.|
|`value`|`uint256`|      Amount to be transferred.|
|`validAfter`|`uint256`| The time after which this is valid (unix time).|
|`validBefore`|`uint256`|The time before which this is valid (unix time).|
|`nonce`|`bytes32`|      Unique nonce.|
|`v`|`uint8`|          v of the signature.|
|`r`|`bytes32`|          r of the signature.|
|`s`|`bytes32`|          s of the signature.|


### receiveWithAuthorization

Receive a transfer with a signed authorization from the payer.

*This has an additional check to ensure that the payee's address matches
the caller of this function to prevent front-running attacks.
(See security considerations)*


```solidity
function receiveWithAuthorization(
    address from,
    address to,
    uint256 value,
    uint256 validAfter,
    uint256 validBefore,
    bytes32 nonce,
    bytes memory signature
) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`from`|`address`|       Payer's address (Authorizer).|
|`to`|`address`|         Payee's address.|
|`value`|`uint256`|      Amount to be transferred.|
|`validAfter`|`uint256`| The time after which this is valid (unix time).|
|`validBefore`|`uint256`|The time before which this is valid (unix time).|
|`nonce`|`bytes32`|      Unique nonce.|
|`signature`|`bytes`|  A byte array ECDSA/secp256k1 signature (encoded r, s, v).|


### receiveWithAuthorization

Receive a transfer with a signed authorization from the payer.

*This has an additional check to ensure that the payee's address matches
the caller of this function to prevent front-running attacks.
(See security considerations)*


```solidity
function receiveWithAuthorization(
    address from,
    address to,
    uint256 value,
    uint256 validAfter,
    uint256 validBefore,
    bytes32 nonce,
    bytes32 r,
    bytes32 vs
) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`from`|`address`|       Payer's address (Authorizer).|
|`to`|`address`|         Payee's address.|
|`value`|`uint256`|      Amount to be transferred.|
|`validAfter`|`uint256`| The time after which this is valid (unix time).|
|`validBefore`|`uint256`|The time before which this is valid (unix time).|
|`nonce`|`bytes32`|      Unique nonce.|
|`r`|`bytes32`|          An ECDSA/secp256k1 signature parameter.|
|`vs`|`bytes32`|         An ECDSA/secp256k1 short signature parameter.|


### receiveWithAuthorization

Receive a transfer with a signed authorization from the payer.

*This has an additional check to ensure that the payee's address matches
the caller of this function to prevent front-running attacks.
(See security considerations)*


```solidity
function receiveWithAuthorization(
    address from,
    address to,
    uint256 value,
    uint256 validAfter,
    uint256 validBefore,
    bytes32 nonce,
    uint8 v,
    bytes32 r,
    bytes32 s
) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`from`|`address`|       Payer's address (Authorizer).|
|`to`|`address`|         Payee's address.|
|`value`|`uint256`|      Amount to be transferred.|
|`validAfter`|`uint256`| The time after which this is valid (unix time).|
|`validBefore`|`uint256`|The time before which this is valid (unix time).|
|`nonce`|`bytes32`|      Unique nonce.|
|`v`|`uint8`|          v of the signature.|
|`r`|`bytes32`|          r of the signature.|
|`s`|`bytes32`|          s of the signature.|


### cancelAuthorization

Attempt to cancel an authorization.


```solidity
function cancelAuthorization(address authorizer, bytes32 nonce, bytes memory signature) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`authorizer`|`address`|Authorizer's address.|
|`nonce`|`bytes32`|     Nonce of the authorization.|
|`signature`|`bytes`| A byte array ECDSA/secp256k1 signature (encoded r, s, v).|


### cancelAuthorization

Attempt to cancel an authorization.


```solidity
function cancelAuthorization(address authorizer, bytes32 nonce, bytes32 r, bytes32 vs) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`authorizer`|`address`|Authorizer's address.|
|`nonce`|`bytes32`|     Nonce of the authorization.|
|`r`|`bytes32`|         An ECDSA/secp256k1 signature parameter.|
|`vs`|`bytes32`|        An ECDSA/secp256k1 short signature parameter.|


### cancelAuthorization

Attempt to cancel an authorization.


```solidity
function cancelAuthorization(address authorizer, bytes32 nonce, uint8 v, bytes32 r, bytes32 s) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`authorizer`|`address`|Authorizer's address.|
|`nonce`|`bytes32`|     Nonce of the authorization.|
|`v`|`uint8`|         v of the signature.|
|`r`|`bytes32`|         r of the signature.|
|`s`|`bytes32`|         s of the signature.|


### authorizationState

Returns the state of an authorization.

*Nonces are randomly generated 32-byte data unique to the authorizer's address*


```solidity
function authorizationState(address authorizer, bytes32 nonce) external view returns (bool);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`authorizer`|`address`|Authorizer's address.|
|`nonce`|`bytes32`|     Nonce of the authorization.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bool`|True if the nonce is used.|


### TRANSFER_WITH_AUTHORIZATION_TYPEHASH

Returns `transferWithAuthorization` typehash.


```solidity
function TRANSFER_WITH_AUTHORIZATION_TYPEHASH() external view returns (bytes32);
```

### RECEIVE_WITH_AUTHORIZATION_TYPEHASH

Returns `receiveWithAuthorization` typehash.


```solidity
function RECEIVE_WITH_AUTHORIZATION_TYPEHASH() external view returns (bytes32);
```

### CANCEL_AUTHORIZATION_TYPEHASH

Returns `cancelAuthorization` typehash.


```solidity
function CANCEL_AUTHORIZATION_TYPEHASH() external view returns (bytes32);
```

## Events
### AuthorizationCanceled
Emitted when an authorization has been canceled.


```solidity
event AuthorizationCanceled(address indexed authorizer, bytes32 indexed nonce);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`authorizer`|`address`|Authorizer's address.|
|`nonce`|`bytes32`|     Nonce of the canceled authorization.|

### AuthorizationUsed
Emitted when an authorization has been used.


```solidity
event AuthorizationUsed(address indexed authorizer, bytes32 indexed nonce);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`authorizer`|`address`|Authorizer's address.|
|`nonce`|`bytes32`|     Nonce of the used authorization.|

## Errors
### AuthorizationAlreadyUsed
Emitted when an authorization has already been used.


```solidity
error AuthorizationAlreadyUsed(address authorizer, bytes32 nonce);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`authorizer`|`address`|Authorizer's address.|
|`nonce`|`bytes32`|     Nonce of the used authorization.|

### AuthorizationExpired
Emitted when an authorization is expired.


```solidity
error AuthorizationExpired(uint256 timestamp, uint256 validBefore);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`timestamp`|`uint256`|  Timestamp at which the transaction was submitted.|
|`validBefore`|`uint256`|Timestamp before which the authorization would have been valid.|

### AuthorizationNotYetValid
Emitted when an authorization is not yet valid.


```solidity
error AuthorizationNotYetValid(uint256 timestamp, uint256 validAfter);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`timestamp`|`uint256`| Timestamp at which the transaction was submitted.|
|`validAfter`|`uint256`|Timestamp after which the authorization will be valid.|

### CallerMustBePayee
Emitted when the caller of `receiveWithAuthorization` is not the payee.


```solidity
error CallerMustBePayee(address caller, address payee);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`caller`|`address`|Caller's address.|
|`payee`|`address`| Payee's address.|

