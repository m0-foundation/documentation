# IStandardGovernor
[Git Source](https://github.com/MZero-Labs/ttg/blob/0d2761f8db14b390e923f59bdae9799fbf9adf2c/src/interfaces/IStandardGovernor.sol)

**Inherits:**
[IBatchGovernor](/src/abstract/interfaces/IBatchGovernor.sol/interface.IBatchGovernor.md)

**Author:**
M^0 Labs


## Functions
### sendProposalFeeToVault

Sends the proposal fee for proposal `proposalId` to the vault, if it is Defeated or Expired.


```solidity
function sendProposalFeeToVault(uint256 proposalId) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`proposalId`|`uint256`|The unique identifier of the proposal.|


### setCashToken

Set the cash token and proposal fee to be used to create proposals going forward.


```solidity
function setCashToken(address newCashToken, uint256 newProposalFee) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`newCashToken`|`address`|  The address of the new cash token.|
|`newProposalFee`|`uint256`|The amount of cash token required onwards to create proposals.|


### addToList

One of the valid proposals. Adds `account` to `list` at the Registrar.


```solidity
function addToList(bytes32 list, address account) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`list`|`bytes32`|   The key for some list.|
|`account`|`address`|The address of some account to be added.|


### removeFromList

One of the valid proposals. Removes `account` to `list` at the Registrar.


```solidity
function removeFromList(bytes32 list, address account) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`list`|`bytes32`|   The key for some list.|
|`account`|`address`|The address of some account to be removed.|


### removeFromAndAddToList

One of the valid proposals. Removes `accountToRemove` and adds `accountToAdd` to `list` at the Registrar.


```solidity
function removeFromAndAddToList(bytes32 list, address accountToRemove, address accountToAdd) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`list`|`bytes32`|           The key for some list.|
|`accountToRemove`|`address`|The address of some account to be removed.|
|`accountToAdd`|`address`|   The address of some account to be added.|


### setKey

One of the valid proposals. Sets `key` to `value` at the Registrar.


```solidity
function setKey(bytes32 key, bytes32 value) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`key`|`bytes32`|  Some key.|
|`value`|`bytes32`|Some value.|


### setProposalFee

One of the valid proposals. Sets the proposal fee of the Standard Governor.


```solidity
function setProposalFee(uint256 newProposalFee) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`newProposalFee`|`uint256`|The new proposal fee.|


### proposalFee

Returns the required amount of cashToken it costs an account to create a proposal.


```solidity
function proposalFee() external view returns (uint256);
```

### getProposal

Returns all the proposal details for a proposal with identifier `proposalId`.


```solidity
function getProposal(uint256 proposalId)
    external
    view
    returns (uint48 voteStart, uint48 voteEnd, ProposalState state, uint256 noVotes, uint256 yesVotes, address proposer);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`proposalId`|`uint256`|The unique identifier of the proposal.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`voteStart`|`uint48`| The first clock value when voting on the proposal is allowed.|
|`voteEnd`|`uint48`|   The last clock value when voting on the proposal is allowed.|
|`state`|`ProposalState`|     The state of the proposal.|
|`noVotes`|`uint256`|   The amount of votes cast against the proposal.|
|`yesVotes`|`uint256`|  The amount of votes cast for the proposal.|
|`proposer`|`address`|  The address of the account that created the proposal.|


### getProposalFee

Returns the proposal fee information.


```solidity
function getProposalFee(uint256 proposalId) external view returns (address cashToken, uint256 amount);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`proposalId`|`uint256`|The unique identifier of the proposal.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`cashToken`|`address`| The address of the cash token for this particular proposal fee.|
|`amount`|`uint256`|    The amount of cash token of the proposal fee.|


### maxTotalZeroRewardPerActiveEpoch

Returns the maximum amount of Zero Token that can be rewarded to all vote casters per active epoch.


```solidity
function maxTotalZeroRewardPerActiveEpoch() external view returns (uint256);
```

### numberOfProposalsAt

Returns the number of proposals at epoch `epoch`.


```solidity
function numberOfProposalsAt(uint256 epoch) external view returns (uint256);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`epoch`|`uint256`|The epoch as a clock value.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint256`|The number of proposals at epoch `epoch`.|


### numberOfProposalsVotedOnAt

Returns the number of proposals that were voted on at `epoch`.


```solidity
function numberOfProposalsVotedOnAt(address voter, uint256 epoch) external view returns (uint256);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`voter`|`address`|The address of some account.|
|`epoch`|`uint256`|The epoch as a clock value.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint256`|The number of proposals at `epoch`.|


### hasVotedOnAllProposals

Returns whether `voter` has voted on all proposals in `epoch`.


```solidity
function hasVotedOnAllProposals(address voter, uint256 epoch) external view returns (bool);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`voter`|`address`|The address of some account.|
|`epoch`|`uint256`|The epoch as a clock value.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bool`|Whether `voter` has voted on all proposals in `epoch`.|


### cashToken

Returns the address of the Cash Token.


```solidity
function cashToken() external view returns (address);
```

### emergencyGovernor

Returns the address of the Emergency Governor.


```solidity
function emergencyGovernor() external view returns (address);
```

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

## Events
### CashTokenSet
Emitted when the cash token is set to `cashToken`.


```solidity
event CashTokenSet(address indexed cashToken);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`cashToken`|`address`|The address of the cash token taking effect.|

### HasVotedOnAllProposals
Emitted when `voter` has voted on all the proposals in the current epoch `currentEpoch`.


```solidity
event HasVotedOnAllProposals(address indexed voter, uint256 indexed currentEpoch);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`voter`|`address`|       The address of the account voting.|
|`currentEpoch`|`uint256`|The current epoch number as a clock value.|

### ProposalFeeSentToVault
Emitted when the proposal fee for the proposal, with identifier `proposalFee`, is sent to the vault.


```solidity
event ProposalFeeSentToVault(uint256 indexed proposalId, address indexed cashToken, uint256 amount);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`proposalId`|`uint256`|The unique identifier of the proposal.|
|`cashToken`|`address`| The address of the cash token for this particular proposal fee.|
|`amount`|`uint256`|    The amount of cash token of the proposal fee.|

### ProposalFeeSet
Emitted when the proposal fee is set to `proposalFee`.


```solidity
event ProposalFeeSet(uint256 proposalFee);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`proposalFee`|`uint256`|The amount of cash token required onwards to create proposals.|

## Errors
### FeeNotDestinedForVault
Revert message when the proposal fee for a yet defeated or yet expired proposal is trying to be moved.


```solidity
error FeeNotDestinedForVault(ProposalState state);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`state`|`ProposalState`|The current state of the proposal.|

### InvalidCashTokenAddress
Revert message when the Cash Token specified in the constructor is address(0).


```solidity
error InvalidCashTokenAddress();
```

### InvalidEmergencyGovernorAddress
Revert message when the Emergency Governor specified in the constructor is address(0).


```solidity
error InvalidEmergencyGovernorAddress();
```

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

### NoFeeToSend
Revert message when proposal fee trying to be moved to the vault is 0.


```solidity
error NoFeeToSend();
```

### NotSelfOrEmergencyGovernor
Revert message when the caller is not this contract itself nor the Emergency Governor.


```solidity
error NotSelfOrEmergencyGovernor();
```

### NotZeroGovernor
Revert message when the caller is not the Zero Governor.


```solidity
error NotZeroGovernor();
```

### TransferFailed
Revert message when a token transfer, from this contract, fails.


```solidity
error TransferFailed();
```

### TransferFromFailed
Revert message when a token transferFrom fails.


```solidity
error TransferFromFailed();
```

