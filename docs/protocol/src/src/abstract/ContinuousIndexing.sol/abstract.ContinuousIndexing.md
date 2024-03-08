# ContinuousIndexing
[Git Source](https://github.com/MZero-Labs/protocol/blob/3382fb7336bbc7276e0c3f51da451c9fa6e0016f/src/abstract/ContinuousIndexing.sol)

**Inherits:**
[IContinuousIndexing](/src/interfaces/IContinuousIndexing.sol/interface.IContinuousIndexing.md)

**Author:**
M^0 Labs


## State Variables
### latestIndex
The latest updated index.


```solidity
uint128 public latestIndex;
```


### _latestRate
*The latest updated rate.*


```solidity
uint32 internal _latestRate;
```


### latestUpdateTimestamp
The latest timestamp when the index was updated.


```solidity
uint40 public latestUpdateTimestamp;
```


## Functions
### constructor

Constructs the ContinuousIndexing contract.


```solidity
constructor();
```

### updateIndex

Updates the latest index and latest accrual time in storage.


```solidity
function updateIndex() public virtual returns (uint128 currentIndex_);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`currentIndex_`|`uint128`|index The new stored index for computing present amounts from principal amounts.|


### currentIndex

The current index that would be written to storage if `updateIndex` is called.


```solidity
function currentIndex() public view virtual returns (uint128);
```

### _getPrincipalAmountRoundedDown

*Returns the principal amount (rounded down) given the present amount, using the current index.*


```solidity
function _getPrincipalAmountRoundedDown(uint240 presentAmount_) internal view returns (uint112);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`presentAmount_`|`uint240`|The present amount.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint112`|The principal amount rounded down.|


### _getPrincipalAmountRoundedUp

*Returns the principal amount (rounded up) given the present amount and an index.*


```solidity
function _getPrincipalAmountRoundedUp(uint240 presentAmount_) internal view returns (uint112);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`presentAmount_`|`uint240`|The present amount.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint112`|The principal amount rounded up.|


### _getPresentAmountRoundedDown

*Returns the present amount (rounded down) given the principal amount and an index.*


```solidity
function _getPresentAmountRoundedDown(uint112 principalAmount_, uint128 index_) internal pure returns (uint240);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`principalAmount_`|`uint112`|The principal amount.|
|`index_`|`uint128`|          An index.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint240`|The present amount rounded down.|


### _getPresentAmountRoundedUp

*Returns the present amount (rounded up) given the principal amount and an index.*


```solidity
function _getPresentAmountRoundedUp(uint112 principalAmount_, uint128 index_) internal pure returns (uint240);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`principalAmount_`|`uint112`|The principal amount.|
|`index_`|`uint128`|          An index.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint240`|The present amount rounded up.|


### _getPrincipalAmountRoundedDown

*Returns the principal amount given the present amount, using the current index.*


```solidity
function _getPrincipalAmountRoundedDown(uint240 presentAmount_, uint128 index_) internal pure returns (uint112);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`presentAmount_`|`uint240`|The present amount.|
|`index_`|`uint128`|        An index.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint112`|The principal amount rounded down.|


### _getPrincipalAmountRoundedUp

*Returns the principal amount given the present amount, using the current index.*


```solidity
function _getPrincipalAmountRoundedUp(uint240 presentAmount_, uint128 index_) internal pure returns (uint112);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`presentAmount_`|`uint240`|The present amount.|
|`index_`|`uint128`|        An index.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint112`|The principal amount rounded up.|


### _rate

*To be overridden by the inheriting contract to return the current rate.*


```solidity
function _rate() internal view virtual returns (uint32);
```

