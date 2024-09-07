# IDistributionVault
[Git Source](https://github.com/MZero-Labs/ttg/blob/0d2761f8db14b390e923f59bdae9799fbf9adf2c/src/interfaces/IDistributionVault.sol)

**Inherits:**
[IERC6372](/src/abstract/interfaces/IERC6372.sol/interface.IERC6372.md), IStatefulERC712

**Author:**
M^0 Labs


## Functions
### claim

Allows a caller to claim `token` distribution between inclusive epochs `startEpoch` and `endEpoch`.


```solidity
function claim(address token, uint256 startEpoch, uint256 endEpoch, address destination)
    external
    returns (uint256 claimed);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`token`|`address`|      The address of the token being claimed.|
|`startEpoch`|`uint256`| The starting epoch number as a clock value.|
|`endEpoch`|`uint256`|   The ending epoch number as a clock value.|
|`destination`|`address`|The address of the account where the claimed token will be sent.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`claimed`|`uint256`|    The total amount of token claimed by `account`.|


### claimBySig

Allows a signer to claim `token` distribution between inclusive epochs `startEpoch` and `endEpoch`.


```solidity
function claimBySig(
    address account,
    address token,
    uint256 startEpoch,
    uint256 endEpoch,
    address destination,
    uint256 deadline,
    uint8 v,
    bytes32 r,
    bytes32 s
) external returns (uint256 claimed);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account`|`address`|    The purported address of the signing account.|
|`token`|`address`|      The address of the token being claimed.|
|`startEpoch`|`uint256`| The starting epoch number as a clock value.|
|`endEpoch`|`uint256`|   The ending epoch number as a clock value.|
|`destination`|`address`|The address of the account where the claimed token will be sent.|
|`deadline`|`uint256`|   The last timestamp at which the signature is still valid.|
|`v`|`uint8`|          v of the signature.|
|`r`|`bytes32`|          r of the signature.|
|`s`|`bytes32`|          s of the signature.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`claimed`|`uint256`|    The total amount of token claimed by `account`.|


### claimBySig

Allows a signer to claim `token` distribution between inclusive epochs `startEpoch` and `endEpoch`.


```solidity
function claimBySig(
    address account,
    address token,
    uint256 startEpoch,
    uint256 endEpoch,
    address destination,
    uint256 deadline,
    bytes memory signature
) external returns (uint256 claimed);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account`|`address`|    The purported address of the signing account.|
|`token`|`address`|      The address of the token being claimed.|
|`startEpoch`|`uint256`| The starting epoch number as a clock value.|
|`endEpoch`|`uint256`|   The ending epoch number as a clock value.|
|`destination`|`address`|The address of the account where the claimed token will be sent.|
|`deadline`|`uint256`|   The last timestamp at which the signature is still valid.|
|`signature`|`bytes`|  A byte array signature.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`claimed`|`uint256`|    The total amount of token claimed by `account`.|


### distribute

Allows for the `token` distribution of an unaccounted for balance of the token.


```solidity
function distribute(address token) external returns (uint256 amount);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`token`|`address`| The address of the token being distributed.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`amount`|`uint256`|The total amount of additional token accounted in this distribution event.|


### CLAIM_TYPEHASH

Returns the EIP712 typehash used in the encoding of the digest for the claimBySig function.


```solidity
function CLAIM_TYPEHASH() external view returns (bytes32);
```

### distributionOfAt

Returns the total amount of `token` eligible for distribution to holder at the end of epoch `epoch`.


```solidity
function distributionOfAt(address token, uint256 epoch) external view returns (uint256);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`token`|`address`|The address of some token.|
|`epoch`|`uint256`|The epoch number as a clock value.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint256`|The total amount of token eligible for distribution to holder at the end of the epoch.|


### getClaimable

Returns the amount of `token` `account` can claim between inclusive epochs `startEpoch` and `endEpoch`.


```solidity
function getClaimable(address token, address account, uint256 startEpoch, uint256 endEpoch)
    external
    view
    returns (uint256);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`token`|`address`|     The address of some token.|
|`account`|`address`|   The address of some account.|
|`startEpoch`|`uint256`|The starting epoch number as a clock value.|
|`endEpoch`|`uint256`|  The ending epoch number as a clock value.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint256`|The amount of token that `account` has yet to claim for these epochs, if any.|


### getClaimDigest

Returns the digest to be signed, via EIP-712, given an internal digest (i.e. hash struct).


```solidity
function getClaimDigest(
    address account,
    address token,
    uint256 startEpoch,
    uint256 endEpoch,
    address destination,
    uint256 nonce,
    uint256 deadline
) external view returns (bytes32);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account`|`address`|    The purported address of the signing account.|
|`token`|`address`|      The address of the token being claimed.|
|`startEpoch`|`uint256`| The starting epoch number as a clock value.|
|`endEpoch`|`uint256`|   The ending epoch number as a clock value.|
|`destination`|`address`|The address the account where the claimed token will be sent.|
|`nonce`|`uint256`|      The nonce of the account claiming the token.|
|`deadline`|`uint256`|   The last timestamp at which the signature is still valid.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bytes32`|The digest to be signed.|


### hasClaimed

Returns whether `account` has already claimed their `token` distribution for `epoch`.


```solidity
function hasClaimed(address token, uint256 epoch, address account) external view returns (bool);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`token`|`address`|  The address of some token.|
|`epoch`|`uint256`|  The epoch number as a clock value.|
|`account`|`address`|The address of some account.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bool`|Whether `account` has already claimed `token` rewards for `epoch`.|


### name

Returns the name of the contract.


```solidity
function name() external view returns (string memory);
```

### zeroToken

Returns the address of the Zero Token holders must have in order to be eligible for distributions.


```solidity
function zeroToken() external view returns (address);
```

## Events
### Claim
Emitted when `account` claims `token` distribution between inclusive epochs `startEpoch` and `endEpoch`.


```solidity
event Claim(address indexed token, address indexed account, uint256 startEpoch, uint256 endEpoch, uint256 amount);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`token`|`address`|     The address of the token being claimed.|
|`account`|`address`|   The address of the account claiming the distribution.|
|`startEpoch`|`uint256`|The starting epoch number as a clock value.|
|`endEpoch`|`uint256`|  The ending epoch number as a clock value.|
|`amount`|`uint256`|    The total amount of token claimed by `account`.|

### Distribution
Emitted when `token` is distributed pro rata to all holders at epoch `epoch`.


```solidity
event Distribution(address indexed token, uint256 indexed epoch, uint256 amount);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`token`|`address`| The address of the token being distributed.|
|`epoch`|`uint256`| The epoch number as a clock value.|
|`amount`|`uint256`|The total amount of token being distributed.|

## Errors
### InvalidDestinationAddress
Revert message when the destination address is address(0).


```solidity
error InvalidDestinationAddress();
```

### InvalidZeroTokenAddress
Revert message when the Zero Token address set at deployment is address(0).


```solidity
error InvalidZeroTokenAddress();
```

### NotPastTimepoint
Revert message when a query for past values is for a timepoint greater or equal to the current clock.


```solidity
error NotPastTimepoint(uint256 timepoint, uint256 clock);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`timepoint`|`uint256`|The timepoint being queried.|
|`clock`|`uint256`|    The current timepoint.|

### StartEpochAfterEndEpoch
Revert message when the start epoch is greater than the end epoch.


```solidity
error StartEpochAfterEndEpoch(uint256 startEpoch, uint256 endEpoch);
```

### TransferFailed
Revert message when a token transfer, from this contract, fails.


```solidity
error TransferFailed();
```

