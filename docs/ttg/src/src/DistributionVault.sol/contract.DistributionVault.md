# DistributionVault
[Git Source](https://github.com/MZero-Labs/ttg/blob/0d2761f8db14b390e923f59bdae9799fbf9adf2c/src/DistributionVault.sol)

**Inherits:**
[IDistributionVault](/src/interfaces/IDistributionVault.sol/interface.IDistributionVault.md), StatefulERC712

**Author:**
M^0 Labs


## State Variables
### _GRANULARITY
*The scale to apply when accumulating an account's claimable token, per epoch, before dividing.
It is arbitrarily set to `1e9`. The smaller it is, the more dust will accumulate in the contract.
Conversely, the larger it is, the more likely it is to overflow when accumulating.
The more epochs that are claimed at once, the less dust will remain.*


```solidity
uint256 internal constant _GRANULARITY = 1e9;
```


### CLAIM_TYPEHASH
Returns the EIP712 typehash used in the encoding of the digest for the claimBySig function.


```solidity
bytes32 public constant CLAIM_TYPEHASH = 0x4b4633c3c305de33d5d9cf70f2712f26961648cd68d020c2556a9e43be58051d;
```


### zeroToken
Returns the address of the Zero Token holders must have in order to be eligible for distributions.


```solidity
address public immutable zeroToken;
```


### _lastTokenBalances
*The last recorded balance per token.*


```solidity
mapping(address token => uint256 balance) internal _lastTokenBalances;
```


### distributionOfAt
Returns the total amount of `token` eligible for distribution to holder at the end of epoch `epoch`.


```solidity
mapping(address token => mapping(uint256 epoch => uint256 amount)) public distributionOfAt;
```


### hasClaimed
Returns whether `account` has already claimed their `token` distribution for `epoch`.


```solidity
mapping(address token => mapping(uint256 epoch => mapping(address account => bool claimed))) public hasClaimed;
```


## Functions
### constructor

Constructs a new DistributionVault contract.


```solidity
constructor(address zeroToken_) StatefulERC712("DistributionVault");
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`zeroToken_`|`address`|The address of the Zero Token contract.|


### claim

Allows a caller to claim `token` distribution between inclusive epochs `startEpoch` and `endEpoch`.


```solidity
function claim(address token_, uint256 startEpoch_, uint256 endEpoch_, address destination_)
    external
    returns (uint256);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`token_`|`address`||
|`startEpoch_`|`uint256`||
|`endEpoch_`|`uint256`||
|`destination_`|`address`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint256`|claimed     The total amount of token claimed by `account`.|


### claimBySig

Allows a signer to claim `token` distribution between inclusive epochs `startEpoch` and `endEpoch`.


```solidity
function claimBySig(
    address account_,
    address token_,
    uint256 startEpoch_,
    uint256 endEpoch_,
    address destination_,
    uint256 deadline_,
    uint8 v_,
    bytes32 r_,
    bytes32 s_
) external returns (uint256);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account_`|`address`||
|`token_`|`address`||
|`startEpoch_`|`uint256`||
|`endEpoch_`|`uint256`||
|`destination_`|`address`||
|`deadline_`|`uint256`||
|`v_`|`uint8`||
|`r_`|`bytes32`||
|`s_`|`bytes32`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint256`|claimed     The total amount of token claimed by `account`.|


### claimBySig

Allows a signer to claim `token` distribution between inclusive epochs `startEpoch` and `endEpoch`.


```solidity
function claimBySig(
    address account_,
    address token_,
    uint256 startEpoch_,
    uint256 endEpoch_,
    address destination_,
    uint256 deadline_,
    bytes memory signature_
) external returns (uint256);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account_`|`address`||
|`token_`|`address`||
|`startEpoch_`|`uint256`||
|`endEpoch_`|`uint256`||
|`destination_`|`address`||
|`deadline_`|`uint256`||
|`signature_`|`bytes`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint256`|claimed     The total amount of token claimed by `account`.|


### distribute

Allows for the `token` distribution of an unaccounted for balance of the token.


```solidity
function distribute(address token_) external returns (uint256 amount_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`token_`|`address`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`amount_`|`uint256`|amount The total amount of additional token accounted in this distribution event.|


### name

Returns the name of the contract.


```solidity
function name() external view returns (string memory);
```

### CLOCK_MODE

Returns a machine-readable string description of the clock the contract is operating on.


```solidity
function CLOCK_MODE() external pure returns (string memory);
```

### getClaimDigest

Returns the digest to be signed, via EIP-712, given an internal digest (i.e. hash struct).


```solidity
function getClaimDigest(
    address account_,
    address token_,
    uint256 startEpoch_,
    uint256 endEpoch_,
    address destination_,
    uint256 nonce_,
    uint256 deadline_
) public view returns (bytes32);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account_`|`address`||
|`token_`|`address`||
|`startEpoch_`|`uint256`||
|`endEpoch_`|`uint256`||
|`destination_`|`address`||
|`nonce_`|`uint256`||
|`deadline_`|`uint256`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bytes32`|The digest to be signed.|


### clock

Returns the current timepoint according to the mode the contract is operating on.


```solidity
function clock() public view returns (uint48);
```

### getClaimable

Returns the amount of `token` `account` can claim between inclusive epochs `startEpoch` and `endEpoch`.


```solidity
function getClaimable(address token_, address account_, uint256 startEpoch_, uint256 endEpoch_)
    public
    view
    returns (uint256 claimable_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`token_`|`address`||
|`account_`|`address`||
|`startEpoch_`|`uint256`||
|`endEpoch_`|`uint256`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`claimable_`|`uint256`|The amount of token that `account` has yet to claim for these epochs, if any.|


### _claim

*Allows a caller to claim `token_` distribution between inclusive epochs `startEpoch` and `endEpoch`.*


```solidity
function _claim(address account_, address token_, uint256 startEpoch_, uint256 endEpoch_, address destination_)
    internal
    returns (uint256 claimed_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account_`|`address`|    The address of the account claiming the token.|
|`token_`|`address`|      The address of the token being claimed.|
|`startEpoch_`|`uint256`| The starting epoch number as a clock value.|
|`endEpoch_`|`uint256`|   The ending epoch number as a clock value.|
|`destination_`|`address`|The address the account where the claimed token will be sent.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`claimed_`|`uint256`|    The total amount of token claimed by `account_`.|


