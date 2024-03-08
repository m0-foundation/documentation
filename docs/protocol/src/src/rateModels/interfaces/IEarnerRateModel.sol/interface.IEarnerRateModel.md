# IEarnerRateModel
[Git Source](https://github.com/MZero-Labs/protocol/blob/3382fb7336bbc7276e0c3f51da451c9fa6e0016f/src/rateModels/interfaces/IEarnerRateModel.sol)

**Inherits:**
[IRateModel](/src/interfaces/IRateModel.sol/interface.IRateModel.md)

**Author:**
M^0 Labs


## Functions
### mToken

The M Token contract address.


```solidity
function mToken() external view returns (address);
```

### minterGateway

The Minter Gateway contract address.


```solidity
function minterGateway() external view returns (address);
```

### ttgRegistrar

The TTG Registrar contract address.


```solidity
function ttgRegistrar() external view returns (address);
```

### maxRate

The max rate in basis points.


```solidity
function maxRate() external view returns (uint256);
```

## Errors
### ZeroMToken
Emitted when M Token contract address is zero.


```solidity
error ZeroMToken();
```

### ZeroMinterGateway
Emitted when Minter Gateway contract address is zero.


```solidity
error ZeroMinterGateway();
```

### ZeroTTGRegistrar
Emitted when TTG Registrar contract address is zero.


```solidity
error ZeroTTGRegistrar();
```

