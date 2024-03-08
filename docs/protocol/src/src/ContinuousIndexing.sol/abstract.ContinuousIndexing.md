# ContinuousIndexing
[Git Source](https://github.com/MZero-Labs/protocol/blob/45d6176ce6231b36efc0c52a2961774481e32ec1/src/ContinuousIndexing.sol)

**Inherits:**
[IContinuousIndexing](/src/interfaces/IContinuousIndexing.sol/interface.IContinuousIndexing.md)


## State Variables
### _latestIndex

```solidity
uint256 internal _latestIndex;
```


### _latestRate

```solidity
uint256 internal _latestRate;
```


### _latestUpdateTimestamp

```solidity
uint256 internal _latestUpdateTimestamp;
```


## Functions
### constructor


```solidity
constructor();
```

### updateIndex

\
|                                      External/Public Interactive Functions                                       |
\*****************************************************************************************************************


```solidity
function updateIndex() public virtual returns (uint256 currentIndex_);
```

### currentIndex

\
|                                       External/Public View/Pure Functions                                        |
\*****************************************************************************************************************


```solidity
function currentIndex() public view virtual returns (uint256 currentIndex_);
```

### latestIndex


```solidity
function latestIndex() public view virtual returns (uint256 index_);
```

### latestUpdateTimestamp


```solidity
function latestUpdateTimestamp() public view virtual returns (uint256 latestAccrualTime_);
```

### _getPresentAmountAndUpdateIndex

\
|                                          Internal Interactive Functions                                          |
\*****************************************************************************************************************


```solidity
function _getPresentAmountAndUpdateIndex(uint256 principalAmount_) internal returns (uint256 presentAmount_);
```

### _getPrincipalAmountAndUpdateIndex


```solidity
function _getPrincipalAmountAndUpdateIndex(uint256 presentAmount_) internal returns (uint256 principalAmount_);
```

### _getPresentAmount

\
|                                           Internal View/Pure Functions                                           |
\*****************************************************************************************************************


```solidity
function _getPresentAmount(uint256 principalAmount_, uint256 index_) internal pure returns (uint256 presentAmount_);
```

### _getPrincipalAmount


```solidity
function _getPrincipalAmount(uint256 presentAmount_, uint256 index_) internal pure returns (uint256 principalAmount_);
```

### _rate


```solidity
function _rate() internal view virtual returns (uint256 rate_);
```

