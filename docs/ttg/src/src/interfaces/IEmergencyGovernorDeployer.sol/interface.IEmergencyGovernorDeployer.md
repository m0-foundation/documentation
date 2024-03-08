# IEmergencyGovernorDeployer
[Git Source](https://github.com/MZero-Labs/ttg/blob/0d2761f8db14b390e923f59bdae9799fbf9adf2c/src/interfaces/IEmergencyGovernorDeployer.sol)

**Inherits:**
[IDeployer](/src/interfaces/IDeployer.sol/interface.IDeployer.md)

**Author:**
M^0 Labs


## Functions
### deploy

Deploys a new instance of an Emergency Governor.


```solidity
function deploy(address powerToken, address standardGovernor, uint16 thresholdRatio) external returns (address);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`powerToken`|`address`|      The address of some Power Token that will be used by voters.|
|`standardGovernor`|`address`|The address of some Standard Governor.|
|`thresholdRatio`|`uint16`|  The threshold ratio to use for proposals.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`address`|The address of the deployed Emergency Governor.|


### registrar

Returns the address of the Registrar.


```solidity
function registrar() external view returns (address);
```

### zeroGovernor

Returns the address of the Zero Governor.


```solidity
function zeroGovernor() external view returns (address);
```

## Errors
### InvalidRegistrarAddress
Revert message when the Registrar specified in the constructor is address(0).


```solidity
error InvalidRegistrarAddress();
```

### InvalidZeroGovernorAddress
Revert message when the Zero Governor specified in the constructor is address(0).


```solidity
error InvalidZeroGovernorAddress();
```

### NotZeroGovernor
Revert message when the caller is not the Zero Governor.


```solidity
error NotZeroGovernor();
```

