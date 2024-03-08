# IPowerTokenDeployer
[Git Source](https://github.com/MZero-Labs/ttg/blob/0d2761f8db14b390e923f59bdae9799fbf9adf2c/src/interfaces/IPowerTokenDeployer.sol)

**Inherits:**
[IDeployer](/src/interfaces/IDeployer.sol/interface.IDeployer.md)

**Author:**
M^0 Labs


## Functions
### deploy

Deploys a new instance of a Power Token.

*Callable only by the Zero Governor.*


```solidity
function deploy(address bootstrapToken, address standardGovernor, address cashToken) external returns (address);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`bootstrapToken`|`address`|  The address of some token to bootstrap from.|
|`standardGovernor`|`address`|The address of some Standard Governor.|
|`cashToken`|`address`|       The address of some Cash Token.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`address`|The address of the deployed Emergency Governor.|


### vault

Returns the address of the Vault.


```solidity
function vault() external view returns (address);
```

### zeroGovernor

Returns the address of the Zero Governor.


```solidity
function zeroGovernor() external view returns (address);
```

## Errors
### InvalidVaultAddress
Revert message when the Vault specified in the constructor is address(0).


```solidity
error InvalidVaultAddress();
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

