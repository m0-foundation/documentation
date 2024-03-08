# MinterRateModel
[Git Source](https://github.com/MZero-Labs/protocol/blob/3382fb7336bbc7276e0c3f51da451c9fa6e0016f/src/rateModels/MinterRateModel.sol)

**Inherits:**
[IMinterRateModel](/src/rateModels/interfaces/IMinterRateModel.sol/interface.IMinterRateModel.md)

**Author:**
M^0 Labs


## State Variables
### _BASE_MINTER_RATE
The name of parameter in TTG that defines the base minter rate.


```solidity
bytes32 internal constant _BASE_MINTER_RATE = "base_minter_rate";
```


### ttgRegistrar
The TTG Registrar contract address.


```solidity
address public immutable ttgRegistrar;
```


## Functions
### constructor

Constructs the MinterRateModel contract.


```solidity
constructor(address ttgRegistrar_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`ttgRegistrar_`|`address`|The address of the TTG Registrar contract.|


### rate

Returns the current yearly rate in BPS.
This value does not account for the compounding interest.


```solidity
function rate() external view returns (uint256 rate_);
```

