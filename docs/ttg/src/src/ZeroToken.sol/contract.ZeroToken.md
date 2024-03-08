# ZeroToken
[Git Source](https://github.com/MZero-Labs/ttg/blob/0d2761f8db14b390e923f59bdae9799fbf9adf2c/src/ZeroToken.sol)

**Inherits:**
[IZeroToken](/src/interfaces/IZeroToken.sol/interface.IZeroToken.md), [EpochBasedVoteToken](/src/abstract/EpochBasedVoteToken.sol/abstract.EpochBasedVoteToken.md)

**Author:**
M^0 Labs


## State Variables
### standardGovernorDeployer
Returns the address of the Standard Governor Deployer.


```solidity
address public immutable standardGovernorDeployer;
```


## Functions
### onlyStandardGovernor

*Revert if the caller is not the Standard Governor.*


```solidity
modifier onlyStandardGovernor();
```

### constructor

Constructs a new ZeroToken contract.


```solidity
constructor(address standardGovernorDeployer_, address[] memory initialAccounts_, uint256[] memory initialBalances_)
    EpochBasedVoteToken("Zero Token", "ZERO", 6);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`standardGovernorDeployer_`|`address`|The address of the StandardGovernorDeployer contract.|
|`initialAccounts_`|`address[]`|         The addresses of the accounts to mint tokens to.|
|`initialBalances_`|`uint256[]`|         The amounts of tokens to mint to the accounts.|


### mint

Mints `amount` token to `recipient`.


```solidity
function mint(address recipient_, uint256 amount_) external onlyStandardGovernor;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`recipient_`|`address`||
|`amount_`|`uint256`||


### pastBalancesOf

Returns an array of token balances of `account`
between `startEpoch` and `endEpoch` past inclusive clocks.


```solidity
function pastBalancesOf(address account_, uint256 startEpoch_, uint256 endEpoch_)
    external
    view
    returns (uint256[] memory);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account_`|`address`||
|`startEpoch_`|`uint256`||
|`endEpoch_`|`uint256`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint256[]`|An array of token balances, each relating to an epoch in the inclusive range.|


### pastTotalSupplies

Returns an array of total token supplies between `startEpoch` and `endEpoch` clocks inclusively.


```solidity
function pastTotalSupplies(uint256 startEpoch_, uint256 endEpoch_) external view returns (uint256[] memory);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`startEpoch_`|`uint256`||
|`endEpoch_`|`uint256`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint256[]`|An array of total supplies, each relating to an epoch in the inclusive range.|


### standardGovernor

Returns the address of the Standard Governor.


```solidity
function standardGovernor() public view returns (address);
```

### _getValuesBetween

*Returns the values of `amountSnaps_` between `startEpoch_` and `endEpoch_`.*


```solidity
function _getValuesBetween(AmountSnap[] storage amountSnaps_, uint16 startEpoch_, uint16 endEpoch_)
    internal
    view
    returns (uint256[] memory values_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`amountSnaps_`|`AmountSnap[]`|The array of AmountSnaps to query.|
|`startEpoch_`|`uint16`| The epoch from which to start querying.|
|`endEpoch_`|`uint16`|   The epoch at which to stop querying.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`values_`|`uint256[]`|     The values of `amountSnaps_` between `startEpoch_` and `endEpoch_`.|


