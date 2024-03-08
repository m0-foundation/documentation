# ThresholdGovernor
[Git Source](https://github.com/MZero-Labs/ttg/blob/0d2761f8db14b390e923f59bdae9799fbf9adf2c/src/abstract/ThresholdGovernor.sol)

**Inherits:**
[IThresholdGovernor](/src/abstract/interfaces/IThresholdGovernor.sol/interface.IThresholdGovernor.md), [BatchGovernor](/src/abstract/BatchGovernor.sol/abstract.BatchGovernor.md)

**Author:**
M^0 Labs


## State Variables
### _MIN_THRESHOLD_RATIO
*The minimum allowed threshold ratio.*


```solidity
uint16 internal constant _MIN_THRESHOLD_RATIO = 271;
```


### thresholdRatio
Returns the threshold ratio to be applied to determine the threshold/quorum for a proposal.


```solidity
uint16 public thresholdRatio;
```


## Functions
### constructor

Construct a new ThresholdGovernor contract.


```solidity
constructor(string memory name_, address voteToken_, uint16 thresholdRatio_) BatchGovernor(name_, voteToken_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`name_`|`string`|          The name of the contract. Used to compute EIP712 domain separator.|
|`voteToken_`|`address`|     The address of the token used to vote.|
|`thresholdRatio_`|`uint16`|The ratio of yes votes votes required for a proposal to succeed.|


### execute

Allows the caller to execute a proposal.


```solidity
function execute(address[] memory, uint256[] memory, bytes[] memory callDatas_, bytes32)
    external
    payable
    returns (uint256 proposalId_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`address[]`||
|`<none>`|`uint256[]`||
|`callDatas_`|`bytes[]`||
|`<none>`|`bytes32`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`proposalId_`|`uint256`|proposalId      The unique identifier for the proposal.|


### propose

Allows the caller to create a proposal.


```solidity
function propose(
    address[] memory targets_,
    uint256[] memory values_,
    bytes[] memory callDatas_,
    string memory description_
) external returns (uint256 proposalId_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`targets_`|`address[]`||
|`values_`|`uint256[]`||
|`callDatas_`|`bytes[]`||
|`description_`|`string`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`proposalId_`|`uint256`|proposalId  The unique identifier for the proposal.|


### getProposal

Returns all data of a proposal with identifier `proposalId`.


```solidity
function getProposal(uint256 proposalId_)
    external
    view
    returns (
        uint48 voteStart_,
        uint48 voteEnd_,
        ProposalState state_,
        uint256 noVotes_,
        uint256 yesVotes_,
        address proposer_,
        uint16 thresholdRatio_
    );
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`proposalId_`|`uint256`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`voteStart_`|`uint48`|voteStart      The first clock value when voting on the proposal is allowed.|
|`voteEnd_`|`uint48`|voteEnd        The last clock value when voting on the proposal is allowed.|
|`state_`|`ProposalState`|state          The state of the proposal.|
|`noVotes_`|`uint256`|noVotes        The amount of votes cast against the proposal.|
|`yesVotes_`|`uint256`|yesVotes       The amount of votes cast for the proposal.|
|`proposer_`|`address`|proposer       The address of the account that created the proposal.|
|`thresholdRatio_`|`uint16`|thresholdRatio The threshold ratio to be applied to determine the threshold/quorum for the proposal.|


### quorum

Returns the minimum number of eligible (COUNTING_MODE) votes for a proposal to succeed.


```solidity
function quorum() external view returns (uint256 quorum_);
```

### quorum

Returns the minimum number of eligible (COUNTING_MODE) votes for a proposal to succeed.


```solidity
function quorum(uint256 timepoint_) external view returns (uint256 quorum_);
```

### state

Returns the state of a proposal with identifier `proposalId`.


```solidity
function state(uint256 proposalId_) public view override(BatchGovernor, IGovernor) returns (ProposalState state_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`proposalId_`|`uint256`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`state_`|`ProposalState`|The state of the proposal.|


### _createProposal

*Creates a new proposal with the given parameters.*


```solidity
function _createProposal(uint256 proposalId_, uint16 voteStart_) internal override;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`proposalId_`|`uint256`|The unique identifier of the proposal.|
|`voteStart_`|`uint16`| The epoch at which the proposal will start collecting votes.|


### _setThresholdRatio

*Set the threshold ratio to be applied to determine the threshold/quorum for a proposal.*


```solidity
function _setThresholdRatio(uint16 newThresholdRatio_) internal;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`newThresholdRatio_`|`uint16`|The new threshold ratio.|


### _votingDelay

*Returns the number of clock values that must elapse before voting begins for a newly created proposal.*


```solidity
function _votingDelay() internal pure override returns (uint16);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint16`|The voting delay.|


### _votingPeriod

*Returns the number of clock values between the vote start and vote end.*


```solidity
function _votingPeriod() internal pure override returns (uint16);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint16`|The voting period.|


