# IThresholdGovernor
[Git Source](https://github.com/MZero-Labs/ttg/blob/0d2761f8db14b390e923f59bdae9799fbf9adf2c/src/abstract/interfaces/IThresholdGovernor.sol)

**Inherits:**
[IBatchGovernor](/src/abstract/interfaces/IBatchGovernor.sol/interface.IBatchGovernor.md)

**Author:**
M^0 Labs


## Functions
### getProposal

Returns all data of a proposal with identifier `proposalId`.


```solidity
function getProposal(uint256 proposalId)
    external
    view
    returns (
        uint48 voteStart,
        uint48 voteEnd,
        ProposalState state,
        uint256 noVotes,
        uint256 yesVotes,
        address proposer,
        uint16 thresholdRatio
    );
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`proposalId`|`uint256`|    The unique identifier for the proposal.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`voteStart`|`uint48`|     The first clock value when voting on the proposal is allowed.|
|`voteEnd`|`uint48`|       The last clock value when voting on the proposal is allowed.|
|`state`|`ProposalState`|         The state of the proposal.|
|`noVotes`|`uint256`|       The amount of votes cast against the proposal.|
|`yesVotes`|`uint256`|      The amount of votes cast for the proposal.|
|`proposer`|`address`|      The address of the account that created the proposal.|
|`thresholdRatio`|`uint16`|The threshold ratio to be applied to determine the threshold/quorum for the proposal.|


### thresholdRatio

Returns the threshold ratio to be applied to determine the threshold/quorum for a proposal.


```solidity
function thresholdRatio() external view returns (uint16);
```

## Events
### ThresholdRatioSet
Emitted when the threshold ratio is set.


```solidity
event ThresholdRatioSet(uint16 thresholdRatio);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`thresholdRatio`|`uint16`|The new threshold ratio.|

## Errors
### InvalidThresholdRatio
Revert message when trying to set the threshold ratio above 100% or below 2.71%.


```solidity
error InvalidThresholdRatio(uint256 thresholdRatio, uint256 minThresholdRatio, uint256 maxThresholdRatio);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`thresholdRatio`|`uint256`|   The threshold ratio being set.|
|`minThresholdRatio`|`uint256`|The minimum allowed threshold ratio.|
|`maxThresholdRatio`|`uint256`|The maximum allowed threshold ratio.|

