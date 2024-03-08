# UIntMath
[Git Source](https://github.com/MZero-Labs/common/blob/9da96e78d24aadd41ee6f776b7b028203782b632/src/libs/UIntMath.sol)

**Author:**
M^0 Labs


## Functions
### safe16

Casts a given uint256 value to a uint16,
ensuring that it is less than or equal to the maximum uint16 value.


```solidity
function safe16(uint256 n) internal pure returns (uint16);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`n`|`uint256`|The value to check.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint16`|The value casted to uint16.|


### safe40

Casts a given uint256 value to a uint40,
ensuring that it is less than or equal to the maximum uint40 value.


```solidity
function safe40(uint256 n) internal pure returns (uint40);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`n`|`uint256`|The value to check.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint40`|The value casted to uint40.|


### safe48

Casts a given uint256 value to a uint48,
ensuring that it is less than or equal to the maximum uint48 value.


```solidity
function safe48(uint256 n) internal pure returns (uint48);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`n`|`uint256`|The value to check.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint48`|The value casted to uint48.|


### safe112

Casts a given uint256 value to a uint112,
ensuring that it is less than or equal to the maximum uint112 value.


```solidity
function safe112(uint256 n) internal pure returns (uint112);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`n`|`uint256`|The value to check.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint112`|The value casted to uint112.|


### safe128

Casts a given uint256 value to a uint128,
ensuring that it is less than or equal to the maximum uint128 value.


```solidity
function safe128(uint256 n) internal pure returns (uint128);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`n`|`uint256`|The value to check.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint128`|The value casted to uint128.|


### safe240

Casts a given uint256 value to a uint240,
ensuring that it is less than or equal to the maximum uint240 value.


```solidity
function safe240(uint256 n) internal pure returns (uint240);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`n`|`uint256`|The value to check.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint240`|The value casted to uint240.|


### bound32

Limits a given uint256 value to the maximum uint32 value.


```solidity
function bound32(uint256 n) internal pure returns (uint32);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`n`|`uint256`|The value to check.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint32`|The value limited to within uint32 bounds.|


### bound112

Limits a given uint256 value to the maximum uint112 value.


```solidity
function bound112(uint256 n) internal pure returns (uint112);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`n`|`uint256`|The value to check.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint112`|The value limited to within uint112 bounds.|


### bound128

Limits a given uint256 value to the maximum uint128 value.


```solidity
function bound128(uint256 n) internal pure returns (uint128);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`n`|`uint256`|The value to check.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint128`|The value limited to within uint128 bounds.|


### bound240

Limits a given uint256 value to the maximum uint240 value.


```solidity
function bound240(uint256 n) internal pure returns (uint240);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`n`|`uint256`|The value to check.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint240`|The value limited to within uint240 bounds.|


### max40

Compares two uint40 values and returns the larger one.


```solidity
function max40(uint40 a_, uint40 b_) internal pure returns (uint40);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`a_`|`uint40`| Value to check.|
|`b_`|`uint40`| Value to check.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint40`|The larger value.|


### min32

Compares two uint32 values and returns the lesser one.


```solidity
function min32(uint32 a_, uint32 b_) internal pure returns (uint32);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`a_`|`uint32`| Value to check.|
|`b_`|`uint32`| Value to check.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint32`|The lesser value.|


### min40

Compares two uint40 values and returns the lesser one.


```solidity
function min40(uint40 a_, uint40 b_) internal pure returns (uint40);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`a_`|`uint40`| Value to check.|
|`b_`|`uint40`| Value to check.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint40`|The lesser value.|


### min240

Compares two uint240 values and returns the lesser one.


```solidity
function min240(uint240 a_, uint240 b_) internal pure returns (uint240);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`a_`|`uint240`| Value to check.|
|`b_`|`uint240`| Value to check.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint240`|The lesser value.|


### min112

Compares two uint112 values and returns the lesser one.


```solidity
function min112(uint112 a_, uint112 b_) internal pure returns (uint112);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`a_`|`uint112`| Value to check.|
|`b_`|`uint112`| Value to check.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint112`|The lesser value.|


### min256

Compares two uint256 values and returns the lesser one.


```solidity
function min256(uint256 a_, uint256 b_) internal pure returns (uint256);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`a_`|`uint256`| Value to check.|
|`b_`|`uint256`| Value to check.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint256`|The lesser value.|


## Errors
### InvalidUInt16
Emitted when a passed value is greater than the maximum value of uint16.


```solidity
error InvalidUInt16();
```

### InvalidUInt40
Emitted when a passed value is greater than the maximum value of uint40.


```solidity
error InvalidUInt40();
```

### InvalidUInt48
Emitted when a passed value is greater than the maximum value of uint48.


```solidity
error InvalidUInt48();
```

### InvalidUInt112
Emitted when a passed value is greater than the maximum value of uint112.


```solidity
error InvalidUInt112();
```

### InvalidUInt128
Emitted when a passed value is greater than the maximum value of uint128.


```solidity
error InvalidUInt128();
```

### InvalidUInt240
Emitted when a passed value is greater than the maximum value of uint240.


```solidity
error InvalidUInt240();
```

