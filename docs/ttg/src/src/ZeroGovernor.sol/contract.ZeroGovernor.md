# ZeroGovernor
[Git Source](https://github.com/MZero-Labs/ttg/blob/0d2761f8db14b390e923f59bdae9799fbf9adf2c/src/ZeroGovernor.sol)

**Inherits:**
[IZeroGovernor](/src/interfaces/IZeroGovernor.sol/interface.IZeroGovernor.md), [ThresholdGovernor](/src/abstract/ThresholdGovernor.sol/abstract.ThresholdGovernor.md)

**Author:**
M^0 Labs


## State Variables
### _MAX_TOTAL_ZERO_REWARD_PER_ACTIVE_EPOCH
*The maximum number of Zero tokens that can be rewarded per active epoch.*


```solidity
uint256 internal constant _MAX_TOTAL_ZERO_REWARD_PER_ACTIVE_EPOCH = 5_000_000e6;
```


### emergencyGovernorDeployer
Returns the address of the Emergency Governor Deployer.


```solidity
address public immutable emergencyGovernorDeployer;
```


### powerTokenDeployer
Returns the address of the Power Token Deployer.


```solidity
address public immutable powerTokenDeployer;
```


### standardGovernorDeployer
Returns the address of the Standard Governor Deployer.


```solidity
address public immutable standardGovernorDeployer;
```


### _allowedCashTokens
*The set of allowed cash tokens.*


```solidity
mapping(address token => bool allowed) internal _allowedCashTokens;
```


## Functions
### constructor

Construct a new ZeroGovernor contract.


```solidity
constructor(
    address voteToken_,
    address emergencyGovernorDeployer_,
    address powerTokenDeployer_,
    address standardGovernorDeployer_,
    address bootstrapToken_,
    uint256 standardProposalFee_,
    uint16 emergencyProposalThresholdRatio_,
    uint16 zeroProposalThresholdRatio_,
    address[] memory allowedCashTokens_
) ThresholdGovernor("ZeroGovernor", voteToken_, zeroProposalThresholdRatio_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`voteToken_`|`address`|                      The address of the token used to vote.|
|`emergencyGovernorDeployer_`|`address`|      The address of the Emergency Governor Deployer contract.|
|`powerTokenDeployer_`|`address`|             The address of the Power Token Deployer contract.|
|`standardGovernorDeployer_`|`address`|       The address of the Standard Governor Deployer contract.|
|`bootstrapToken_`|`address`|                 The address of the token that bootstraps the reset.|
|`standardProposalFee_`|`uint256`|            The proposal fee for the Standard Governor.|
|`emergencyProposalThresholdRatio_`|`uint16`|The threshold ratio for the Emergency Governor.|
|`zeroProposalThresholdRatio_`|`uint16`|     The threshold ratio for the Zero Governor.|
|`allowedCashTokens_`|`address[]`|              The set of allowed cash tokens.|


### resetToPowerHolders

One of the valid proposals. Reset the Standard Governor, Emergency Governor, and Power Token to the
Power Token holders. This would be used by Zero Token holders in the event that inflation is soon to
result in Power Token overflowing, and/or there is a loss of faith in the state of either the Standard
Governor or Emergency Governor.


```solidity
function resetToPowerHolders() external onlySelf;
```

### resetToZeroHolders

One of the valid proposals. Reset the Standard Governor, Emergency Governor, and Power Token to the
ZeroToken holders. This would be used by Zero Token holders if they no longer have faith in the current
set of PowerToken holders and/or the state of either the Standard Governor or Emergency Governor.


```solidity
function resetToZeroHolders() external onlySelf;
```

### setCashToken

One of the valid proposals. Sets the Cash Token of the system.


```solidity
function setCashToken(address newCashToken_, uint256 newProposalFee_) external onlySelf;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`newCashToken_`|`address`||
|`newProposalFee_`|`uint256`||


### setEmergencyProposalThresholdRatio

One of the valid proposals. Sets the threshold ratio for Emergency Governor proposals.


```solidity
function setEmergencyProposalThresholdRatio(uint16 newThresholdRatio_) external onlySelf;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`newThresholdRatio_`|`uint16`||


### setZeroProposalThresholdRatio

One of the valid proposals. Sets the threshold ratio for this governor's proposals.


```solidity
function setZeroProposalThresholdRatio(uint16 newThresholdRatio_) external onlySelf;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`newThresholdRatio_`|`uint16`||


### isAllowedCashToken

Returns whether `token` is an allowed Cash Token of the system, as a parameter in setCashToken proposal.


```solidity
function isAllowedCashToken(address token_) external view returns (bool);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`token_`|`address`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bool`|Whether `token` is an allowed Cash Token.|


### emergencyGovernor

Returns the address of the Emergency Governor.


```solidity
function emergencyGovernor() public view returns (address);
```

### standardGovernor

Returns the address of the Standard Governor.


```solidity
function standardGovernor() public view returns (address);
```

### _deployEphemeralContracts

*Deploys the ephemeral `standardGovernor`, `emergencyGovernor`, and `powerToken` contracts.*


```solidity
function _deployEphemeralContracts(
    address emergencyGovernorDeployer_,
    address powerTokenDeployer_,
    address standardGovernorDeployer_,
    address bootstrapToken_,
    address cashToken_,
    uint16 emergencyProposalThresholdRatio_,
    uint256 proposalFee_
) internal returns (address standardGovernor_, address emergencyGovernor_, address powerToken_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`emergencyGovernorDeployer_`|`address`|      The address of the Emergency Governor Deployer contract.|
|`powerTokenDeployer_`|`address`|             The address of the Power Token Deployer contract.|
|`standardGovernorDeployer_`|`address`|       The address of the Standard Governor Deployer contract.|
|`bootstrapToken_`|`address`|                 The address of a token to bootstrap the new Power Token.|
|`cashToken_`|`address`|                      The address of the Cash Token contract.|
|`emergencyProposalThresholdRatio_`|`uint16`|The threshold ratio for the Emergency Governor.|
|`proposalFee_`|`uint256`|                    The proposal fee for the Standard Governor.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`standardGovernor_`|`address`|               The address of the deployed Standard Governor contract.|
|`emergencyGovernor_`|`address`|              The address of the deployed Emergency Governor contract.|
|`powerToken_`|`address`|                     The address of the deployed Power Token contract.|


### _resetContracts

*Redeploy the ephemeral `standardGovernor`, `emergencyGovernor`, and `powerToken` contracts, where:
- the cash token is the same cash token in the existing `standardGovernor`
- the `emergencyGovernor` threshold ratio is the same threshold ratio in the existing `emergencyGovernor`
- the `standardGovernor` proposal fee is the same proposal fee in the existing `standardGovernor`*


```solidity
function _resetContracts(address bootstrapToken_) internal;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`bootstrapToken_`|`address`|The token to bootstrap the `powerToken` balances and voting powers.|


### _revertIfInvalidCalldata

*All proposals target this contract itself, and must call one of the listed functions to be valid.*


```solidity
function _revertIfInvalidCalldata(bytes memory callData_) internal pure override;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`callData_`|`bytes`|The call data to check.|


