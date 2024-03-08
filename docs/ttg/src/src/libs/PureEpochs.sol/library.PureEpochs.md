# PureEpochs
[Git Source](https://github.com/MZero-Labs/ttg/blob/0d2761f8db14b390e923f59bdae9799fbf9adf2c/src/libs/PureEpochs.sol)

**Author:**
M^0 Labs

Defines epochs as 15 days away from 'The Merge' timestamp.

*Allows for a `uint16` epoch up to timestamp 86,595,288,162 (i.e. Thu, Feb 05, Year 4714, 06:42:42 GMT).*


## State Variables
### _MERGE_TIMESTAMP
The timestamp of The Merge block.


```solidity
uint40 internal constant _MERGE_TIMESTAMP = 1_663_224_162;
```


### _EPOCH_PERIOD
The approximate target of seconds an epoch should endure.


```solidity
uint40 internal constant _EPOCH_PERIOD = 15 days;
```


## Functions
### currentEpoch

*Returns the current epoch number.*


```solidity
function currentEpoch() internal view returns (uint16);
```

### timeRemainingInCurrentEpoch

*Returns the remaining time in the current epoch.*


```solidity
function timeRemainingInCurrentEpoch() internal view returns (uint40);
```

