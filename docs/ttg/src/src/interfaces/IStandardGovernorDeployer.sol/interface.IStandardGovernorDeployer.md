# IStandardGovernorDeployer
[Git Source](https://github.com/MZero-Labs/ttg/blob/0d2761f8db14b390e923f59bdae9799fbf9adf2c/src/interfaces/IStandardGovernorDeployer.sol)

**Inherits:**
[IDeployer](/src/interfaces/IDeployer.sol/interface.IDeployer.md)

**Author:**
M^0 Labs


## Functions
### deploy

Deploys a new instance of a Standard Governor.


```solidity
function deploy(
    address powerToken,
    address emergencyGovernor,
    address cashToken,
    uint256 proposalFee,
    uint256 maxTotalZeroRewardPerActiveEpoch
) external returns (address);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`powerToken`|`address`|                      The address of some Power Token that will be used by voters.|
|`emergencyGovernor`|`address`|               The address of some Emergency Governor.|
|`cashToken`|`address`|                       The address of some Cash Token.|
|`proposalFee`|`uint256`|                     The proposal fee required to create proposals.|
|`maxTotalZeroRewardPerActiveEpoch`|`uint256`|The maximum amount of Zero Token rewarded per active epoch.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`address`|The address of the deployed Standard Governor.|


### registrar

Returns the address of the Registrar.


```solidity
function registrar() external view returns (address);
```

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

### zeroToken

Returns the address of the Zero Token.


```solidity
function zeroToken() external view returns (address);
```

## Errors
### InvalidRegistrarAddress
Revert message when the Registrar specified in the constructor is address(0).


```solidity
error InvalidRegistrarAddress();
```

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

### InvalidZeroTokenAddress
Revert message when the Zero Token specified in the constructor is address(0).


```solidity
error InvalidZeroTokenAddress();
```

### NotZeroGovernor
Revert message when the caller is not the Zero Governor.


```solidity
error NotZeroGovernor();
```

