# IERC712
[Git Source](https://github.com/MZero-Labs/common/blob/9da96e78d24aadd41ee6f776b7b028203782b632/src/interfaces/IERC712.sol)

**Author:**
M^0 Labs

*The interface as defined by EIP-712: https://eips.ethereum.org/EIPS/eip-712*


## Functions
### DOMAIN_SEPARATOR

Returns the EIP712 domain separator used in the encoding of a signed digest.


```solidity
function DOMAIN_SEPARATOR() external view returns (bytes32);
```

## Errors
### InvalidSignature
Revert the message when an invalid signature is detected.


```solidity
error InvalidSignature();
```

### InvalidSignatureLength
Revert the message when a signature with an invalid length is detected.


```solidity
error InvalidSignatureLength();
```

### InvalidSignatureS
Revert the message when the S portion of a signature is invalid.


```solidity
error InvalidSignatureS();
```

### InvalidSignatureV
Revert the message when the V portion of a signature is invalid.


```solidity
error InvalidSignatureV();
```

### SignatureExpired
Revert the message when a signature is being used beyond its deadline (i.e. expiry).


```solidity
error SignatureExpired(uint256 deadline, uint256 timestamp);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`deadline`|`uint256`| The deadline of the signature.|
|`timestamp`|`uint256`|The current timestamp.|

### SignerMismatch
Revert message when a recovered signer does not match the account being purported to have signed.


```solidity
error SignerMismatch();
```

