# EmergencyGovernorDeployer
[Git Source](https://github.com/MZero-Labs/ttg/blob/0d2761f8db14b390e923f59bdae9799fbf9adf2c/src/EmergencyGovernorDeployer.sol)

**Inherits:**
[IEmergencyGovernorDeployer](/src/interfaces/IEmergencyGovernorDeployer.sol/interface.IEmergencyGovernorDeployer.md)

**Author:**
M^0 Labs


## State Variables
### registrar
Returns the address of the Registrar.


```solidity
address public immutable registrar;
```


### zeroGovernor
Returns the address of the Zero Governor.


```solidity
address public immutable zeroGovernor;
```


### lastDeploy
Returns the address of the last contract deployed by this contract.


```solidity
address public lastDeploy;
```


### nonce
Returns the nonce used to pre deterministically compute the address of the next deployed contract.


```solidity
uint256 public nonce;
```


## Functions
### onlyZeroGovernor

*Throws if called by any contract other than the Zero Governor.*


```solidity
modifier onlyZeroGovernor();
```

### constructor

Constructs a new EmergencyGovernorDeployer contract.


```solidity
constructor(address zeroGovernor_, address registrar_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`zeroGovernor_`|`address`|The address of the ZeroGovernor contract.|
|`registrar_`|`address`|   The address of the Registrar contract.|


### deploy

Deploys a new instance of an Emergency Governor.


```solidity
function deploy(address powerToken_, address standardGovernor_, uint16 thresholdRatio_)
    external
    onlyZeroGovernor
    returns (address);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`powerToken_`|`address`||
|`standardGovernor_`|`address`||
|`thresholdRatio_`|`uint16`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`address`|The address of the deployed Emergency Governor.|


### nextDeploy

Returns the address of the next contract this contract will deploy.


```solidity
function nextDeploy() external view returns (address);
```

