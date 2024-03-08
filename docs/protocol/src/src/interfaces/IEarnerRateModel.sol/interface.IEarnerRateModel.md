# IEarnerRateModel
[Git Source](https://github.com/MZero-Labs/protocol/blob/45d6176ce6231b36efc0c52a2961774481e32ec1/src/interfaces/IEarnerRateModel.sol)

**Inherits:**
[IRateModel](/src/interfaces/IRateModel.sol/interface.IRateModel.md)


## Functions
### mToken


```solidity
function mToken() external view returns (address mToken);
```

### protocol


```solidity
function protocol() external view returns (address protocol);
```

### spogRegistrar


```solidity
function spogRegistrar() external view returns (address spogRegistrar);
```

### baseRate


```solidity
function baseRate() external view returns (uint256 baseRate_);
```

## Errors
### ZeroMToken

```solidity
error ZeroMToken();
```

### ZeroProtocol

```solidity
error ZeroProtocol();
```

### ZeroSpogRegistrar

```solidity
error ZeroSpogRegistrar();
```

