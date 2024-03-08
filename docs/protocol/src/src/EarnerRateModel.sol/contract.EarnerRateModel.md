# EarnerRateModel
[Git Source](https://github.com/MZero-Labs/protocol/blob/45d6176ce6231b36efc0c52a2961774481e32ec1/src/EarnerRateModel.sol)

**Inherits:**
[IEarnerRateModel](/src/interfaces/IEarnerRateModel.sol/interface.IEarnerRateModel.md)


## State Variables
### _ONE

```solidity
uint256 internal constant _ONE = 10_000;
```


### mToken

```solidity
address public immutable mToken;
```


### protocol

```solidity
address public immutable protocol;
```


### spogRegistrar

```solidity
address public immutable spogRegistrar;
```


## Functions
### constructor


```solidity
constructor(address protocol_);
```

### rate


```solidity
function rate() external view returns (uint256 rate_);
```

### baseRate


```solidity
function baseRate() public view returns (uint256 baseRate_);
```

### _min


```solidity
function _min(uint256 a_, uint256 b_) internal pure returns (uint256);
```

