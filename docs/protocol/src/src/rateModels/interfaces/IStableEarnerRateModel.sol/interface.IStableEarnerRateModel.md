# IStableEarnerRateModel
[Git Source](https://github.com/MZero-Labs/protocol/blob/3382fb7336bbc7276e0c3f51da451c9fa6e0016f/src/rateModels/interfaces/IStableEarnerRateModel.sol)

**Inherits:**
[IEarnerRateModel](/src/rateModels/interfaces/IEarnerRateModel.sol/interface.IEarnerRateModel.md)

**Author:**
M^0 Labs


## Functions
### RATE_CONFIDENCE_INTERVAL

The interval over which there's confidence cash flow to earners will not exceed cash flows from minters.


```solidity
function RATE_CONFIDENCE_INTERVAL() external view returns (uint32);
```

### RATE_MULTIPLIER

The percent (in basis points) of the earner rate that will be effectively used.


```solidity
function RATE_MULTIPLIER() external view returns (uint32);
```

### ONE

100% in basis points.


```solidity
function ONE() external view returns (uint32);
```

### getSafeEarnerRate

Returns the safe earner rate.


```solidity
function getSafeEarnerRate(uint240 totalActiveOwedM, uint240 totalEarningSupply, uint32 minterRate)
    external
    pure
    returns (uint32);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`totalActiveOwedM`|`uint240`|  The total active owed M.|
|`totalEarningSupply`|`uint240`|The total earning supply of M Token.|
|`minterRate`|`uint32`|        The minter rate.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint32`|The safe earner rate.|


