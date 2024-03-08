# MinterRateModel
[Git Source](https://github.com/MZero-Labs/protocol/blob/45d6176ce6231b36efc0c52a2961774481e32ec1/src/MinterRateModel.sol)

**Inherits:**
[IMinterRateModel](/src/interfaces/IMinterRateModel.sol/interface.IMinterRateModel.md)


## State Variables
### spogRegistrar

```solidity
address public immutable spogRegistrar;
```


## Functions
### constructor


```solidity
constructor(address spogRegistrar_);
```

### baseRate


```solidity
function baseRate() public view returns (uint256 baseRate_);
```

### rate


```solidity
function rate() external view returns (uint256 rate_);
```

