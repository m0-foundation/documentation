# IRateModel
[Git Source](https://github.com/MZero-Labs/protocol/blob/3382fb7336bbc7276e0c3f51da451c9fa6e0016f/src/interfaces/IRateModel.sol)

**Author:**
M^0 Labs


## Functions
### rate

Returns the current yearly rate in BPS.
This value does not account for the compounding interest.


```solidity
function rate() external view returns (uint256);
```

