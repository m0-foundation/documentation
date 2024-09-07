# SignatureChecker
[Git Source](https://github.com/MZero-Labs/common/blob/9da96e78d24aadd41ee6f776b7b028203782b632/src/libs/SignatureChecker.sol)

**Author:**
M^0 Labs


## Functions
### isValidSignature

*Returns whether a signature is valid (ECDSA/secp256k1 or ERC1271) for a signer and digest.*

*Signatures must not be used as unique identifiers since the `ecrecover` EVM opcode
allows for malleable (non-unique) signatures.
See https://github.com/OpenZeppelin/openzeppelin-contracts/security/advisories/GHSA-4h98-2769-gh6h*


```solidity
function isValidSignature(address signer, bytes32 digest, bytes memory signature) internal view returns (bool);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`signer`|`address`|   The address of the account purported to have signed.|
|`digest`|`bytes32`|   The hash of the data that was signed.|
|`signature`|`bytes`|A byte array signature.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bool`|Whether the signature is valid or not.|


### isValidERC1271Signature

*Returns whether an ERC1271 signature is valid for a signer and digest.*


```solidity
function isValidERC1271Signature(address signer, bytes32 digest, bytes memory signature) internal view returns (bool);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`signer`|`address`|   The address of the account purported to have signed.|
|`digest`|`bytes32`|   The hash of the data that was signed.|
|`signature`|`bytes`|A byte array ERC1271 signature.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bool`|Whether the signature is valid or not.|


### decodeECDSASignature

*Decodes an ECDSA/secp256k1 signature from a byte array to standard v, r, and s parameters.*


```solidity
function decodeECDSASignature(bytes memory signature) internal pure returns (uint8 v, bytes32 r, bytes32 s);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`signature`|`bytes`|A byte array ECDSA/secp256k1 signature.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`v`|`uint8`|        An ECDSA/secp256k1 signature parameter.|
|`r`|`bytes32`|        An ECDSA/secp256k1 signature parameter.|
|`s`|`bytes32`|        An ECDSA/secp256k1 signature parameter.|


### decodeShortECDSASignature

*Decodes an ECDSA/secp256k1 short signature as defined by EIP2098
from a byte array to standard v, r, and s parameters.*


```solidity
function decodeShortECDSASignature(bytes memory signature) internal pure returns (bytes32 r, bytes32 vs);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`signature`|`bytes`|A byte array ECDSA/secp256k1 short signature.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`r`|`bytes32`|        An ECDSA/secp256k1 signature parameter.|
|`vs`|`bytes32`|       An ECDSA/secp256k1 short signature parameter.|


### isValidECDSASignature

*Returns whether an ECDSA/secp256k1 signature is valid for a signer and digest.*


```solidity
function isValidECDSASignature(address signer, bytes32 digest, bytes memory signature) internal pure returns (bool);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`signer`|`address`|   The address of the account purported to have signed.|
|`digest`|`bytes32`|   The hash of the data that was signed.|
|`signature`|`bytes`|A byte array ECDSA/secp256k1 signature (encoded r, s, v).|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bool`|Whether the signature is valid or not.|


### isValidECDSASignature

*Returns whether an ECDSA/secp256k1 short signature is valid for a signer and digest.*


```solidity
function isValidECDSASignature(address signer, bytes32 digest, bytes32 r, bytes32 vs) internal pure returns (bool);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`signer`|`address`| The address of the account purported to have signed.|
|`digest`|`bytes32`| The hash of the data that was signed.|
|`r`|`bytes32`|      An ECDSA/secp256k1 signature parameter.|
|`vs`|`bytes32`|     An ECDSA/secp256k1 short signature parameter.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bool`|Whether the signature is valid or not.|


### recoverECDSASigner

*Returns the signer of an ECDSA/secp256k1 signature for some digest.*


```solidity
function recoverECDSASigner(bytes32 digest, bytes memory signature) internal pure returns (Error, address);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`digest`|`bytes32`|   The hash of the data that was signed.|
|`signature`|`bytes`|A byte array ECDSA/secp256k1 signature.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`Error`|An error, if any, that occurred during the signer recovery.|
|`<none>`|`address`|The address of the account recovered from the signature (0 if error).|


### recoverECDSASigner

*Returns the signer of an ECDSA/secp256k1 short signature for some digest.*

*See https://eips.ethereum.org/EIPS/eip-2098*


```solidity
function recoverECDSASigner(bytes32 digest, bytes32 r, bytes32 vs) internal pure returns (Error, address);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`digest`|`bytes32`|The hash of the data that was signed.|
|`r`|`bytes32`|     An ECDSA/secp256k1 signature parameter.|
|`vs`|`bytes32`|    An ECDSA/secp256k1 short signature parameter.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`Error`|An error, if any, that occurred during the signer recovery.|
|`<none>`|`address`|The address of the account recovered form the signature (0 if error).|


### recoverECDSASigner

*Returns the signer of an ECDSA/secp256k1 signature for some digest.*


```solidity
function recoverECDSASigner(bytes32 digest, uint8 v, bytes32 r, bytes32 s)
    internal
    pure
    returns (Error, address signer);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`digest`|`bytes32`|The hash of the data that was signed.|
|`v`|`uint8`|     An ECDSA/secp256k1 signature parameter.|
|`r`|`bytes32`|     An ECDSA/secp256k1 signature parameter.|
|`s`|`bytes32`|     An ECDSA/secp256k1 signature parameter.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`Error`|An error, if any, that occurred during the signer recovery.|
|`signer`|`address`|The address of the account recovered form the signature (0 if error).|


### validateECDSASignature

*Returns an error, if any, in validating an ECDSA/secp256k1 signature for a signer and digest.*


```solidity
function validateECDSASignature(address signer, bytes32 digest, bytes memory signature) internal pure returns (Error);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`signer`|`address`|   The address of the account purported to have signed.|
|`digest`|`bytes32`|   The hash of the data that was signed.|
|`signature`|`bytes`|A byte array ERC1271 signature.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`Error`|An error, if any, that occurred during the signer recovery.|


### validateECDSASignature

*Returns an error, if any, in validating an ECDSA/secp256k1 short signature for a signer and digest.*


```solidity
function validateECDSASignature(address signer, bytes32 digest, bytes32 r, bytes32 vs) internal pure returns (Error);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`signer`|`address`|The address of the account purported to have signed.|
|`digest`|`bytes32`|The hash of the data that was signed.|
|`r`|`bytes32`|     An ECDSA/secp256k1 signature parameter.|
|`vs`|`bytes32`|    An ECDSA/secp256k1 short signature parameter.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`Error`|An error, if any, that occurred during the signer recovery.|


### validateECDSASignature

*Returns an error, if any, in validating an ECDSA/secp256k1 signature for a signer and digest.*


```solidity
function validateECDSASignature(address signer, bytes32 digest, uint8 v, bytes32 r, bytes32 s)
    internal
    pure
    returns (Error);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`signer`|`address`|The address of the account purported to have signed.|
|`digest`|`bytes32`|The hash of the data that was signed.|
|`v`|`uint8`|     An ECDSA/secp256k1 signature parameter.|
|`r`|`bytes32`|     An ECDSA/secp256k1 signature parameter.|
|`s`|`bytes32`|     An ECDSA/secp256k1 signature parameter.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`Error`|An error, if any, that occurred during the signer recovery.|


### validateRecoveredSigner

*Returns an error if `signer` is not `recoveredSigner`.*


```solidity
function validateRecoveredSigner(address signer, address recoveredSigner) internal pure returns (Error);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`signer`|`address`|         The address of the some signer.|
|`recoveredSigner`|`address`|The address of the some recoveredSigner.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`Error`|An error if `signer` is not `recoveredSigner`.|


## Enums
### Error
An enum representing the possible errors that can be emitted during signature validation.


```solidity
enum Error {
    NoError,
    InvalidSignature,
    InvalidSignatureLength,
    InvalidSignatureS,
    InvalidSignatureV,
    SignerMismatch
}
```

