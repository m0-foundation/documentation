# IZeroGovernor
[Git Source](https://github.com/MZero-Labs/ttg/blob/0d2761f8db14b390e923f59bdae9799fbf9adf2c/src/interfaces/IZeroGovernor.sol)

**Inherits:**
[IThresholdGovernor](/src/abstract/interfaces/IThresholdGovernor.sol/interface.IThresholdGovernor.md)

**Author:**
M^0 Labs


## Functions
### resetToPowerHolders

One of the valid proposals. Reset the Standard Governor, Emergency Governor, and Power Token to the
Power Token holders. This would be used by Zero Token holders in the event that inflation is soon to
result in Power Token overflowing, and/or there is a loss of faith in the state of either the Standard
Governor or Emergency Governor.


```solidity
function resetToPowerHolders() external;
```

### resetToZeroHolders

One of the valid proposals. Reset the Standard Governor, Emergency Governor, and Power Token to the
ZeroToken holders. This would be used by Zero Token holders if they no longer have faith in the current
set of PowerToken holders and/or the state of either the Standard Governor or Emergency Governor.


```solidity
function resetToZeroHolders() external;
```

### setCashToken

One of the valid proposals. Sets the Cash Token of the system.


```solidity
function setCashToken(address newCashToken, uint256 newProposalFee) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`newCashToken`|`address`|  The address of the new cash token.|
|`newProposalFee`|`uint256`|The amount of cash token required onwards to create Standard Governor proposals.|


### setEmergencyProposalThresholdRatio

One of the valid proposals. Sets the threshold ratio for Emergency Governor proposals.


```solidity
function setEmergencyProposalThresholdRatio(uint16 newThresholdRatio) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`newThresholdRatio`|`uint16`|The new threshold ratio.|


### setZeroProposalThresholdRatio

One of the valid proposals. Sets the threshold ratio for this governor's proposals.


```solidity
function setZeroProposalThresholdRatio(uint16 newThresholdRatio) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`newThresholdRatio`|`uint16`|The new threshold ratio.|


### isAllowedCashToken

Returns whether `token` is an allowed Cash Token of the system, as a parameter in setCashToken proposal.


```solidity
function isAllowedCashToken(address token) external view returns (bool);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`token`|`address`|The address of some token.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bool`|Whether `token` is an allowed Cash Token.|


### emergencyGovernor

Returns the address of the Emergency Governor.


```solidity
function emergencyGovernor() external view returns (address);
```

### emergencyGovernorDeployer

Returns the address of the Emergency Governor Deployer.


```solidity
function emergencyGovernorDeployer() external view returns (address);
```

### powerTokenDeployer

Returns the address of the Power Token Deployer.


```solidity
function powerTokenDeployer() external view returns (address);
```

### standardGovernor

Returns the address of the Standard Governor.


```solidity
function standardGovernor() external view returns (address);
```

### standardGovernorDeployer

Returns the address of the Standard Governor Deployer.


```solidity
function standardGovernorDeployer() external view returns (address);
```

## Events
### AllowedCashTokensSet
Emitted upon contract deployment, once the set of allowed cash tokens is finalized.


```solidity
event AllowedCashTokensSet(address[] allowedCashTokens);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`allowedCashTokens`|`address[]`|An array of addresses that are allowed as cash tokens.|

### ResetExecuted
Emitted upon a Reset, resulting in a new Standard Governor, Emergency Governor, and Power Token.


```solidity
event ResetExecuted(
    address indexed bootstrapToken, address standardGovernor, address emergencyGovernor, address powerToken
);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`bootstrapToken`|`address`|   The address of token (Zero Token or old Power Token), that bootstraps the reset.|
|`standardGovernor`|`address`| The address of the new Standard Governor.|
|`emergencyGovernor`|`address`|The address of the new Emergency Governor.|
|`powerToken`|`address`|       The address of the new Power Token.|

## Errors
### InvalidCashToken
Revert message when the Cash Token specified is not in the allowed set.


```solidity
error InvalidCashToken();
```

### InvalidCashTokenAddress
Revert message when the Cash Token specified in the constructor is address(0).


```solidity
error InvalidCashTokenAddress();
```

### InvalidEmergencyGovernorDeployerAddress
Revert message when the Emergency Governor Deployer specified in the constructor is address(0).


```solidity
error InvalidEmergencyGovernorDeployerAddress();
```

### InvalidPowerTokenDeployerAddress
Revert message when the Power Token Deployer specified in the constructor is address(0).


```solidity
error InvalidPowerTokenDeployerAddress();
```

### InvalidStandardGovernorDeployerAddress
Revert message when the Standard Governor Deployer specified in the constructor is address(0).


```solidity
error InvalidStandardGovernorDeployerAddress();
```

### NoAllowedCashTokens
Revert message when the set of allowed cash tokens specified in the constructor is empty.


```solidity
error NoAllowedCashTokens();
```

### UnexpectedPowerTokenDeployed
Revert message when the address of the deployed Poker Token differs fro what was expected.


```solidity
error UnexpectedPowerTokenDeployed(address expected, address deployed);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`expected`|`address`|The expected address of the deployed Poker Token.|
|`deployed`|`address`|The actual address of the deployed Poker Token.|

### UnexpectedStandardGovernorDeployed
Revert message when the address of the deployed Standard Governor differs fro what was expected.


```solidity
error UnexpectedStandardGovernorDeployed(address expected, address deployed);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`expected`|`address`|The expected address of the deployed Standard Governor.|
|`deployed`|`address`|The actual address of the deployed Standard Governor.|

