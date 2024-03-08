# IERC1271
[Git Source](https://github.com/MZero-Labs/common/blob/9da96e78d24aadd41ee6f776b7b028203782b632/src/interfaces/IERC1271.sol)

**Author:**
M^0 Labs

*The interface as defined by EIP-1271: https://eips.ethereum.org/EIPS/eip-1271*


## Functions
### isValidSignature

*Returns a specific magic value if the provided signature is valid for the provided digest.*


```solidity
function isValidSignature(bytes32 digest, bytes memory signature) external view returns (bytes4 magicValue);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`digest`|`bytes32`|    Hash of the data purported to have been signed.|
|`signature`|`bytes`| Signature byte array associated with the digest.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`magicValue`|`bytes4`|Magic value 0x1626ba7e if the signature is valid.|


