# ContinuousIndexingMath
[Git Source](https://github.com/MZero-Labs/protocol/blob/3382fb7336bbc7276e0c3f51da451c9fa6e0016f/src/libs/ContinuousIndexingMath.sol)

**Author:**
M^0 Labs


## State Variables
### SECONDS_PER_YEAR
The number of seconds in a year.


```solidity
uint32 internal constant SECONDS_PER_YEAR = 31_536_000;
```


### BPS_SCALED_ONE
100% in basis points.


```solidity
uint16 internal constant BPS_SCALED_ONE = 1e4;
```


### EXP_SCALED_ONE
The scaling of rates in for exponent math.


```solidity
uint56 internal constant EXP_SCALED_ONE = 1e12;
```


## Functions
### divideDown

Helper function to calculate `(x * EXP_SCALED_ONE) / index`, rounded down.

*Inspired by USM (https://github.com/usmfum/USM/blob/master/contracts/WadMath.sol)*


```solidity
function divideDown(uint240 x, uint128 index) internal pure returns (uint112 z);
```

### divideUp

Helper function to calculate `(x * EXP_SCALED_ONE) / index`, rounded up.

*Inspired by USM (https://github.com/usmfum/USM/blob/master/contracts/WadMath.sol)*


```solidity
function divideUp(uint240 x, uint128 index) internal pure returns (uint112 z);
```

### multiplyDown

Helper function to calculate `(x * index) / EXP_SCALED_ONE`, rounded down.

*Inspired by USM (https://github.com/usmfum/USM/blob/master/contracts/WadMath.sol)*


```solidity
function multiplyDown(uint112 x, uint128 index) internal pure returns (uint240 z);
```

### multiplyUp

Helper function to calculate `(x * index) / EXP_SCALED_ONE`, rounded up.

*Inspired by USM (https://github.com/usmfum/USM/blob/master/contracts/WadMath.sol)*


```solidity
function multiplyUp(uint112 x, uint128 index) internal pure returns (uint240 z);
```

### multiplyIndicesDown

Helper function to calculate `(index * deltaIndex) / EXP_SCALED_ONE`, rounded down.

*Inspired by USM (https://github.com/usmfum/USM/blob/master/contracts/WadMath.sol)*


```solidity
function multiplyIndicesDown(uint128 index, uint48 deltaIndex) internal pure returns (uint144 z);
```

### multiplyIndicesUp

Helper function to calculate `(index * deltaIndex) / EXP_SCALED_ONE`, rounded up.

*Inspired by USM (https://github.com/usmfum/USM/blob/master/contracts/WadMath.sol)*


```solidity
function multiplyIndicesUp(uint128 index, uint48 deltaIndex) internal pure returns (uint144 z);
```

### getContinuousIndex

Helper function to calculate e^rt (continuous compounding formula).

*`uint64 yearlyRate` can accommodate 1000% interest per year.*

*`uint32 time` can accommodate 100 years.*

*`type(uint64).max * type(uint32).max / SECONDS_PER_YEAR` fits in a `uint72`.*


```solidity
function getContinuousIndex(uint64 yearlyRate, uint32 time) internal pure returns (uint48 index);
```

### exponent

Helper function to calculate y = e^x using R(4,4) Padé approximation:
e(x) = (1 + x/2 + 3(x^2)/28 + x^3/84 + x^4/1680) / (1 - x/2 + 3(x^2)/28 - x^3/84 + x^4/1680)
See: https://en.wikipedia.org/wiki/Pad%C3%A9_table
See: https://www.wolframalpha.com/input?i=PadeApproximant%5Bexp%5Bx%5D%2C%7Bx%2C0%2C%7B4%2C+4%7D%7D%5D
Despite itself being a whole number, `x` represents a real number scaled by `EXP_SCALED_ONE`, thus
allowing for y = e^x where x is a real number.

*Output `y` for a `uint72` input `x` will fit in `uint48`*


```solidity
function exponent(uint72 x) internal pure returns (uint48 y);
```

### convertToBasisPoints

Helper function to convert 12-decimal representation to basis points.


```solidity
function convertToBasisPoints(uint64 input) internal pure returns (uint40);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`input`|`uint64`|The input in 12-decimal representation.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint40`|The output in basis points.|


### convertFromBasisPoints

Helper function to convert basis points to 12-decimal representation.


```solidity
function convertFromBasisPoints(uint32 input) internal pure returns (uint64);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`input`|`uint32`|The input in basis points.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint64`|The output in 12-decimal representation.|


## Errors
### DivisionByZero
Emitted when a division by zero occurs.


```solidity
error DivisionByZero();
```

