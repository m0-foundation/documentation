# IContinuousIndexing
[Git Source](https://github.com/MZero-Labs/protocol/blob/3382fb7336bbc7276e0c3f51da451c9fa6e0016f/src/interfaces/IContinuousIndexing.sol)

**Author:**
M^0 Labs


## Functions
### updateIndex

Updates the latest index and latest accrual time in storage.


```solidity
function updateIndex() external returns (uint128);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint128`|index The new stored index for computing present amounts from principal amounts.|


### currentIndex

The current index that would be written to storage if `updateIndex` is called.


```solidity
function currentIndex() external view returns (uint128);
```

### latestIndex

The latest updated index.


```solidity
function latestIndex() external view returns (uint128);
```

### latestUpdateTimestamp

The latest timestamp when the index was updated.


```solidity
function latestUpdateTimestamp() external view returns (uint40);
```

## Events
### IndexUpdated
Emitted when the index is updated.


```solidity
event IndexUpdated(uint128 indexed index, uint32 indexed rate);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`index`|`uint128`|The new index.|
|`rate`|`uint32`| The current rate.|

