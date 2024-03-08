# IZeroToken
[Git Source](https://github.com/MZero-Labs/ttg/blob/0d2761f8db14b390e923f59bdae9799fbf9adf2c/src/interfaces/IZeroToken.sol)

**Inherits:**
[IEpochBasedVoteToken](/src/abstract/interfaces/IEpochBasedVoteToken.sol/interface.IEpochBasedVoteToken.md)

**Author:**
M^0 Labs


## Functions
### mint

Mints `amount` token to `recipient`.


```solidity
function mint(address recipient, uint256 amount) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`recipient`|`address`|The address of the account receiving minted token.|
|`amount`|`uint256`|   The amount of token to mint.|


### pastBalancesOf

Returns an array of token balances of `account`
between `startEpoch` and `endEpoch` past inclusive clocks.


```solidity
function pastBalancesOf(address account, uint256 startEpoch, uint256 endEpoch)
    external
    view
    returns (uint256[] memory);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account`|`address`|   The address of some account.|
|`startEpoch`|`uint256`|The starting epoch number as a clock value.|
|`endEpoch`|`uint256`|  The ending epoch number as a clock value.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint256[]`|An array of token balances, each relating to an epoch in the inclusive range.|


### pastTotalSupplies

Returns an array of total token supplies between `startEpoch` and `endEpoch` clocks inclusively.


```solidity
function pastTotalSupplies(uint256 startEpoch, uint256 endEpoch) external view returns (uint256[] memory);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`startEpoch`|`uint256`|The starting epoch number as a clock value.|
|`endEpoch`|`uint256`|  The ending epoch number as a clock value.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint256[]`|An array of total supplies, each relating to an epoch in the inclusive range.|


### standardGovernor

Returns the address of the Standard Governor.


```solidity
function standardGovernor() external view returns (address);
```

### standardGovernorDeployer

Returns the address of the Standard Governor Deployer.


```solidity
function standardGovernorDeployer() external view returns (address);
```

## Errors
### ArrayLengthMismatch
Revert message when the length of some accounts array does not equal the length of some balances array.


```solidity
error ArrayLengthMismatch(uint256 accountsLength, uint256 balancesLength);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`accountsLength`|`uint256`|The length of the accounts array.|
|`balancesLength`|`uint256`|The length of the balances array.|

### InvalidStandardGovernorDeployerAddress
Revert message when the Standard Governor Deployer specified in the constructor is address(0).


```solidity
error InvalidStandardGovernorDeployerAddress();
```

### NotStandardGovernor
Revert message when the caller is not the Standard Governor.


```solidity
error NotStandardGovernor();
```

### StartEpochAfterEndEpoch
Revert message when the start of an inclusive range query is larger than the end.


```solidity
error StartEpochAfterEndEpoch();
```

