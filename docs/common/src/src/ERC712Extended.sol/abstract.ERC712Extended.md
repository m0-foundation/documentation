# ERC712Extended
[Git Source](https://github.com/MZero-Labs/common/blob/9da96e78d24aadd41ee6f776b7b028203782b632/src/ERC712Extended.sol)

**Inherits:**
[IERC712Extended](/src/interfaces/IERC712Extended.sol/interface.IERC712Extended.md)

**Author:**
M^0 Labs

*An abstract implementation to satisfy EIP-712: https://eips.ethereum.org/EIPS/eip-712*


## State Variables
### _EIP712_DOMAIN_HASH
*keccak256("EIP712Domain(string name,string version,uint256 chainId,address verifyingContract)")*


```solidity
bytes32 internal constant _EIP712_DOMAIN_HASH = 0x8b73c3c69bb8fe3d512ecc4cf759cc79239f7b179b0ffacaa9a75d522b39400f;
```


### _EIP712_VERSION_HASH
*keccak256("1")*


```solidity
bytes32 internal constant _EIP712_VERSION_HASH = 0xc89efdaa54c0f20c7adf612882df0950f5a951637e0307cdcb4c672f298b8bc6;
```


### _INITIAL_CHAIN_ID
*Initial Chain ID set at deployment.*


```solidity
uint256 internal immutable _INITIAL_CHAIN_ID;
```


### _INITIAL_DOMAIN_SEPARATOR
*Initial EIP-712 domain separator set at deployment.*


```solidity
bytes32 internal immutable _INITIAL_DOMAIN_SEPARATOR;
```


### _name
*The name of the contract.*


```solidity
string internal _name;
```


## Functions
### constructor

Constructs the EIP-712 domain separator.


```solidity
constructor(string memory name_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`name_`|`string`|The name of the contract.|


### eip712Domain

Returns the fields and values that describe the domain separator used by this contract for EIP-712.


```solidity
function eip712Domain()
    external
    view
    virtual
    returns (
        bytes1 fields_,
        string memory name_,
        string memory version_,
        uint256 chainId_,
        address verifyingContract_,
        bytes32 salt_,
        uint256[] memory extensions_
    );
```

### DOMAIN_SEPARATOR

Returns the EIP712 domain separator used in the encoding of a signed digest.


```solidity
function DOMAIN_SEPARATOR() public view virtual returns (bytes32);
```

### _getDomainSeparator

*Computes the EIP-712 domain separator.*


```solidity
function _getDomainSeparator() internal view returns (bytes32);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bytes32`|The EIP-712 domain separator.|


### _getDigest

*Returns the digest to be signed, via EIP-712, given an internal digest (i.e. hash struct).*


```solidity
function _getDigest(bytes32 internalDigest_) internal view returns (bytes32);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`internalDigest_`|`bytes32`|The internal digest.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bytes32`|The digest to be signed.|


### _revertIfExpired

*Revert if the signature is expired.*


```solidity
function _revertIfExpired(uint256 expiry_) internal view;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`expiry_`|`uint256`|Timestamp at which the signature expires or max uint256 for no expiry.|


### _revertIfInvalidSignature

*Revert if the signature is invalid.*

*We first validate if the signature is a valid ECDSA signature and return early if it is the case.
Then, we validate if it is a valid ERC-1271 signature, and return early if it is the case.
If not, we revert with the error from the ECDSA signature validation.*


```solidity
function _revertIfInvalidSignature(address signer_, bytes32 digest_, bytes memory signature_) internal view;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`signer_`|`address`|   The signer of the signature.|
|`digest_`|`bytes32`|   The digest that was signed.|
|`signature_`|`bytes`|The signature.|


### _getSignerAndRevertIfInvalidSignature

*Returns the signer of a signed digest, via EIP-712, and reverts if the signature is invalid.*


```solidity
function _getSignerAndRevertIfInvalidSignature(bytes32 digest_, uint8 v_, bytes32 r_, bytes32 s_)
    internal
    pure
    returns (address signer_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`digest_`|`bytes32`|The digest that was signed.|
|`v_`|`uint8`|     v of the signature.|
|`r_`|`bytes32`|     r of the signature.|
|`s_`|`bytes32`|     s of the signature.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`signer_`|`address`|The signer of the digest.|


### _revertIfInvalidSignature

*Revert if the signature is invalid.*


```solidity
function _revertIfInvalidSignature(address signer_, bytes32 digest_, bytes32 r_, bytes32 vs_) internal pure;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`signer_`|`address`|The signer of the signature.|
|`digest_`|`bytes32`|The digest that was signed.|
|`r_`|`bytes32`|     An ECDSA/secp256k1 signature parameter.|
|`vs_`|`bytes32`|    An ECDSA/secp256k1 short signature parameter.|


### _revertIfInvalidSignature

*Revert if the signature is invalid.*


```solidity
function _revertIfInvalidSignature(address signer_, bytes32 digest_, uint8 v_, bytes32 r_, bytes32 s_) internal pure;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`signer_`|`address`|The signer of the signature.|
|`digest_`|`bytes32`|The digest that was signed.|
|`v_`|`uint8`|     v of the signature.|
|`r_`|`bytes32`|     r of the signature.|
|`s_`|`bytes32`|     s of the signature.|


### _revertIfError

*Revert if error.*


```solidity
function _revertIfError(SignatureChecker.Error error_) private pure;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`error_`|`SignatureChecker.Error`|The SignatureChecker Error enum.|


