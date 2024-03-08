# IERC20Extended
[Git Source](https://github.com/MZero-Labs/common/blob/9da96e78d24aadd41ee6f776b7b028203782b632/src/interfaces/IERC20Extended.sol)

**Inherits:**
[IERC20](/src/interfaces/IERC20.sol/interface.IERC20.md), [IERC3009](/src/interfaces/IERC3009.sol/interface.IERC3009.md)

**Author:**
M^0 Labs

*The additional interface as defined by EIP-2612: https://eips.ethereum.org/EIPS/eip-2612*


## Functions
### permit

Approves `spender` to spend up to `amount` of the token balance of `owner`, via a signature.


```solidity
function permit(address owner, address spender, uint256 value, uint256 deadline, uint8 v, bytes32 r, bytes32 s)
    external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`owner`|`address`|   The address of the account who's token balance is being approved to be spent by `spender`.|
|`spender`|`address`| The address of an account allowed to spend on behalf of `owner`.|
|`value`|`uint256`|   The amount of the allowance being approved.|
|`deadline`|`uint256`|The last block number where the signature is still valid.|
|`v`|`uint8`|       An ECDSA secp256k1 signature parameter (EIP-2612 via EIP-712).|
|`r`|`bytes32`|       An ECDSA secp256k1 signature parameter (EIP-2612 via EIP-712).|
|`s`|`bytes32`|       An ECDSA secp256k1 signature parameter (EIP-2612 via EIP-712).|


### permit

Approves `spender` to spend up to `amount` of the token balance of `owner`, via a signature.


```solidity
function permit(address owner, address spender, uint256 value, uint256 deadline, bytes memory signature) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`owner`|`address`|    The address of the account who's token balance is being approved to be spent by `spender`.|
|`spender`|`address`|  The address of an account allowed to spend on behalf of `owner`.|
|`value`|`uint256`|    The amount of the allowance being approved.|
|`deadline`|`uint256`| The last block number where the signature is still valid.|
|`signature`|`bytes`|An arbitrary signature (EIP-712).|


### PERMIT_TYPEHASH

Returns the EIP712 typehash used in the encoding of the digest for the permit function.


```solidity
function PERMIT_TYPEHASH() external view returns (bytes32);
```

## Errors
### InsufficientAllowance
Revert message when spender's allowance is not sufficient.


```solidity
error InsufficientAllowance(address spender, uint256 allowance, uint256 needed);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`spender`|`address`|   Address that may be allowed to operate on tokens without being their owner.|
|`allowance`|`uint256`| Amount of tokens a `spender` is allowed to operate with.|
|`needed`|`uint256`|    Minimum amount required to perform a transfer.|

### InsufficientAmount
Revert message emitted when the transferred amount is insufficient.


```solidity
error InsufficientAmount(uint256 amount);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`amount`|`uint256`|Amount transferred.|

### InvalidRecipient
Revert message emitted when the recipient of a token is invalid.


```solidity
error InvalidRecipient(address recipient);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`recipient`|`address`|Address of the invalid recipient.|

