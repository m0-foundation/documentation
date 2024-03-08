# IMinterRateModel
[Git Source](https://github.com/MZero-Labs/protocol/blob/3382fb7336bbc7276e0c3f51da451c9fa6e0016f/src/rateModels/interfaces/IMinterRateModel.sol)

**Inherits:**
[IRateModel](/src/interfaces/IRateModel.sol/interface.IRateModel.md)

**Author:**
M^0 Labs


## Functions
### ttgRegistrar

The TTG Registrar contract address.


```solidity
function ttgRegistrar() external view returns (address);
```

## Errors
### ZeroTTGRegistrar
Emitted when TTG Registrar contract address is zero.


```solidity
error ZeroTTGRegistrar();
```

