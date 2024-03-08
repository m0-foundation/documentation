# StableEarnerRateModel
[Git Source](https://github.com/MZero-Labs/protocol/blob/3382fb7336bbc7276e0c3f51da451c9fa6e0016f/src/rateModels/StableEarnerRateModel.sol)

**Inherits:**
[IStableEarnerRateModel](/src/rateModels/interfaces/IStableEarnerRateModel.sol/interface.IStableEarnerRateModel.md)

**Author:**
M^0 Labs


## State Variables
### RATE_CONFIDENCE_INTERVAL
The interval over which there's confidence cash flow to earners will not exceed cash flows from minters.


```solidity
uint32 public constant RATE_CONFIDENCE_INTERVAL = 30 days;
```


### RATE_MULTIPLIER
The percent (in basis points) of the earner rate that will be effectively used.


```solidity
uint32 public constant RATE_MULTIPLIER = 9_000;
```


### ONE
100% in basis points.


```solidity
uint32 public constant ONE = 10_000;
```


### _MAX_EARNER_RATE
The name of parameter in TTG that defines the max earner rate.


```solidity
bytes32 internal constant _MAX_EARNER_RATE = "max_earner_rate";
```


### _EXP_SCALED_ONE
The scaling of rates in for exponent math.


```solidity
uint256 internal constant _EXP_SCALED_ONE = 1e12;
```


### _WAD_TO_EXP_SCALER
The scaling of `_EXP_SCALED_ONE` for wad maths operations.


```solidity
int256 internal constant _WAD_TO_EXP_SCALER = 1e6;
```


### mToken
The M Token contract address.


```solidity
address public immutable mToken;
```


### minterGateway
The Minter Gateway contract address.


```solidity
address public immutable minterGateway;
```


### ttgRegistrar
The TTG Registrar contract address.


```solidity
address public immutable ttgRegistrar;
```


## Functions
### constructor

Constructs the EarnerRateModel contract.


```solidity
constructor(address minterGateway_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`minterGateway_`|`address`|The address of the Minter Gateway contract.|


### rate

Returns the current yearly rate in BPS.
This value does not account for the compounding interest.


```solidity
function rate() external view returns (uint256);
```

### maxRate

The max rate in basis points.


```solidity
function maxRate() public view returns (uint256);
```

### getSafeEarnerRate

Returns the safe earner rate.


```solidity
function getSafeEarnerRate(uint240 totalActiveOwedM_, uint240 totalEarningSupply_, uint32 minterRate_)
    public
    pure
    returns (uint32);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`totalActiveOwedM_`|`uint240`||
|`totalEarningSupply_`|`uint240`||
|`minterRate_`|`uint32`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint32`|The safe earner rate.|


