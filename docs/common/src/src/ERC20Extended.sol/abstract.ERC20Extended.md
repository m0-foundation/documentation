# ERC20Extended
[Git Source](https://github.com/MZero-Labs/common/blob/9da96e78d24aadd41ee6f776b7b028203782b632/src/ERC20Extended.sol)

**Inherits:**
[IERC20Extended](/src/interfaces/IERC20Extended.sol/interface.IERC20Extended.md), [ERC3009](/src/ERC3009.sol/abstract.ERC3009.md)

**Author:**
M^0 Labs


## State Variables
### PERMIT_TYPEHASH
Returns the EIP712 typehash used in the encoding of the digest for the permit function.

*Keeping this constant, despite `permit` parameter name differences, to ensure max EIP-2612 compatibility.
keccak256("Permit(address owner,address spender,uint256 value,uint256 nonce,uint256 deadline)")*


```solidity
bytes32 public constant PERMIT_TYPEHASH = 0x6e71edae12b1b97f4d1f60370fef10105fa2faae0126114a169c64845d6126c9;
```


### decimals
Returns the number of decimals UIs should assume all amounts have.


```solidity
uint8 public immutable decimals;
```


### symbol
Returns the symbol of the token.


```solidity
string public symbol;
```


### allowance
Returns the allowance `spender` is allowed to spend on behalf of `account`.


```solidity
mapping(address account => mapping(address spender => uint256 allowance)) public allowance;
```


## Functions
### constructor

Constructs the ERC20Extended contract.


```solidity
constructor(string memory name_, string memory symbol_, uint8 decimals_) ERC3009(name_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`name_`|`string`|    The name of the token.|
|`symbol_`|`string`|  The symbol of the token.|
|`decimals_`|`uint8`|The number of decimals the token uses.|


### approve

Allows a calling account to approve `spender` to spend up to `amount` of its token balance.

*MUST emit an `Approval` event.*


```solidity
function approve(address spender_, uint256 amount_) external returns (bool success_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`spender_`|`address`||
|`amount_`|`uint256`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`success_`|`bool`|Whether or not the approval was successful.|


### permit

Approves `spender` to spend up to `amount` of the token balance of `owner`, via a signature.


```solidity
function permit(address owner_, address spender_, uint256 value_, uint256 deadline_, uint8 v_, bytes32 r_, bytes32 s_)
    external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`owner_`|`address`||
|`spender_`|`address`||
|`value_`|`uint256`||
|`deadline_`|`uint256`||
|`v_`|`uint8`||
|`r_`|`bytes32`||
|`s_`|`bytes32`||


### permit

Approves `spender` to spend up to `amount` of the token balance of `owner`, via a signature.


```solidity
function permit(address owner_, address spender_, uint256 value_, uint256 deadline_, bytes memory signature_)
    external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`owner_`|`address`||
|`spender_`|`address`||
|`value_`|`uint256`||
|`deadline_`|`uint256`||
|`signature_`|`bytes`||


### transfer

Allows a calling account to transfer `amount` tokens to `recipient`.


```solidity
function transfer(address recipient_, uint256 amount_) external returns (bool success_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`recipient_`|`address`||
|`amount_`|`uint256`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`success_`|`bool`|Whether or not the transfer was successful.|


### transferFrom

Allows a calling account to transfer `amount` tokens from `sender`, with allowance, to a `recipient`.


```solidity
function transferFrom(address sender_, address recipient_, uint256 amount_) external returns (bool success_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`sender_`|`address`||
|`recipient_`|`address`||
|`amount_`|`uint256`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`success_`|`bool`|Whether or not the transfer was successful.|


### name

Returns the name of the contract/token.


```solidity
function name() external view returns (string memory name_);
```

### _approve

*Approve `spender_` to spend `amount_` of tokens from `account_`.*


```solidity
function _approve(address account_, address spender_, uint256 amount_) internal virtual;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account_`|`address`|The address approving the allowance.|
|`spender_`|`address`|The address approved to spend the tokens.|
|`amount_`|`uint256`| The amount of tokens being approved for spending.|


### _setAllowance

*Set the `amount_` of tokens `spender_` is allowed to spend from `account_`.*


```solidity
function _setAllowance(address account_, address spender_, uint256 amount_) internal virtual;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account_`|`address`|The address for which the allowance is set.|
|`spender_`|`address`|The address allowed to spend the tokens.|
|`amount_`|`uint256`| The amount of tokens being allowed for spending.|


### _permitAndGetDigest

*Performs the approval based on the permit info, validates the deadline, and returns the digest.*


```solidity
function _permitAndGetDigest(address owner_, address spender_, uint256 amount_, uint256 deadline_)
    internal
    virtual
    returns (bytes32 digest_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`owner_`|`address`|   The address of the account approving the allowance.|
|`spender_`|`address`| The address of the account being allowed to spend the tokens.|
|`amount_`|`uint256`|  The amount of tokens being approved for spending.|
|`deadline_`|`uint256`|The deadline by which the signature must be used.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`digest_`|`bytes32`|  The EIP-712 digest of the permit.|


