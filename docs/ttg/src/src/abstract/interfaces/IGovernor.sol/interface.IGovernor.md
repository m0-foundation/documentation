# IGovernor
[Git Source](https://github.com/MZero-Labs/ttg/blob/0d2761f8db14b390e923f59bdae9799fbf9adf2c/src/abstract/interfaces/IGovernor.sol)

**Inherits:**
[IERC6372](/src/abstract/interfaces/IERC6372.sol/interface.IERC6372.md), IERC712

**Author:**
M^0 Labs


## Functions
### castVote

Allows the caller to cast a vote on a proposal with id `proposalId`.


```solidity
function castVote(uint256 proposalId, uint8 support) external returns (uint256 weight);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`proposalId`|`uint256`|The unique identifier for the proposal.|
|`support`|`uint8`|   The type of support to cast for the proposal.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`weight`|`uint256`|    The number of votes cast.|


### castVoteBySig

Allows a signer to cast a vote on a proposal with id `proposalId` via an ECDSA secp256k1 signature.


```solidity
function castVoteBySig(uint256 proposalId, uint8 support, uint8 v, bytes32 r, bytes32 s)
    external
    returns (uint256 weight);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`proposalId`|`uint256`|The unique identifier for the proposal.|
|`support`|`uint8`|   The type of support to cast for the proposal.|
|`v`|`uint8`|         An ECDSA secp256k1 signature parameter.|
|`r`|`bytes32`|         An ECDSA secp256k1 signature parameter.|
|`s`|`bytes32`|         An ECDSA secp256k1 signature parameter.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`weight`|`uint256`|    The number of votes cast.|


### castVoteBySig

Allows `voter` to cast a vote on a proposal with id `proposalId` via an arbitrary signature.


```solidity
function castVoteBySig(address voter, uint256 proposalId, uint8 support, bytes memory signature)
    external
    returns (uint256 weight);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`voter`|`address`|     The address of the account that casting their vote, and purported the have signed.|
|`proposalId`|`uint256`|The unique identifier for the proposal.|
|`support`|`uint8`|   The type of support to cast for the proposal.|
|`signature`|`bytes`| An arbitrary signature.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`weight`|`uint256`|    The number of votes cast.|


### castVoteWithReason

Allows the caller to cast a vote with reason on a proposal with id `proposalId`.


```solidity
function castVoteWithReason(uint256 proposalId, uint8 support, string calldata reason)
    external
    returns (uint256 weight);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`proposalId`|`uint256`|The unique identifier for the proposal.|
|`support`|`uint8`|   The type of support to cast for the proposal.|
|`reason`|`string`|    The reason for which the caller casts their vote, if any.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`weight`|`uint256`|    The number of votes cast.|


### castVoteWithReasonBySig

Allows a signer to cast a vote with reason on a proposal with id `proposalId`
via an ECDSA secp256k1 signature.


```solidity
function castVoteWithReasonBySig(
    uint256 proposalId,
    uint8 support,
    string calldata reason,
    uint8 v,
    bytes32 r,
    bytes32 s
) external returns (uint256 weight);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`proposalId`|`uint256`|The unique identifier for the proposal.|
|`support`|`uint8`|   The type of support to cast for the proposal.|
|`reason`|`string`|    The reason for which the caller casts their vote, if any.|
|`v`|`uint8`|         An ECDSA secp256k1 signature parameter.|
|`r`|`bytes32`|         An ECDSA secp256k1 signature parameter.|
|`s`|`bytes32`|         An ECDSA secp256k1 signature parameter.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`weight`|`uint256`|    The number of votes cast.|


### castVoteWithReasonBySig

Allows `voter` to cast a vote with reason on a proposal with id `proposalId` via an arbitrary signature.


```solidity
function castVoteWithReasonBySig(
    address voter,
    uint256 proposalId,
    uint8 support,
    string calldata reason,
    bytes memory signature
) external returns (uint256 weight);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`voter`|`address`|     The address of the account that casting their vote, and purported the have signed.|
|`proposalId`|`uint256`|The unique identifier for the proposal.|
|`support`|`uint8`|   The type of support to cast for the proposal.|
|`reason`|`string`|    The reason for which the caller casts their vote, if any.|
|`signature`|`bytes`| An arbitrary signature.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`weight`|`uint256`|    The number of votes cast.|


### execute

Allows the caller to execute a proposal.


```solidity
function execute(address[] memory targets, uint256[] memory values, bytes[] memory callDatas, bytes32 descriptionHash)
    external
    payable
    returns (uint256 proposalId);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`targets`|`address[]`|        An array of addresses that will be called upon the execution.|
|`values`|`uint256[]`|         An array of ETH amounts that will be sent to each respective target upon execution.|
|`callDatas`|`bytes[]`|      An array of call data used to call each respective target upon execution.|
|`descriptionHash`|`bytes32`|The hash of the string of the description of the proposal.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`proposalId`|`uint256`|     The unique identifier for the proposal.|


### propose

Allows the caller to create a proposal.


```solidity
function propose(address[] memory targets, uint256[] memory values, bytes[] memory callDatas, string memory description)
    external
    returns (uint256 proposalId);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`targets`|`address[]`|    An array of addresses that will be called upon the execution.|
|`values`|`uint256[]`|     An array of ETH amounts that will be sent to each respective target upon execution.|
|`callDatas`|`bytes[]`|  An array of call data used to call each respective target upon execution.|
|`description`|`string`|The string of the description of the proposal.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`proposalId`|`uint256`| The unique identifier for the proposal.|


### COUNTING_MODE

module:voting

*A description of the possible "support" values for castVote and the way these votes are counted, meant to
be consumed by UIs to show correct vote options and interpret the results. The string is a URL-encoded
sequence of key-value pairs that each describe one aspect, for example `support=for,against&quorum=for`.
The string can be decoded by the standard URLSearchParams JavaScript class.*


```solidity
function COUNTING_MODE() external view returns (string memory);
```

### getVotes

Returns the voting power of `account` at clock value `timepoint`.


```solidity
function getVotes(address account, uint256 timepoint) external view returns (uint256);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account`|`address`|  The address of the account with voting power.|
|`timepoint`|`uint256`|The point in time, according to the clock mode the contract is operating on.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint256`|The voting power of `account` at `timepoint`.|


### hashProposal

Returns the unique identifier for the proposal if it were created at this exact moment.


```solidity
function hashProposal(
    address[] memory targets,
    uint256[] memory values,
    bytes[] memory callDatas,
    bytes32 descriptionHash
) external view returns (uint256);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`targets`|`address[]`|        An array of addresses that will be called upon the execution.|
|`values`|`uint256[]`|         An array of ETH amounts that will be sent to each respective target upon execution.|
|`callDatas`|`bytes[]`|      An array of call data used to call each respective target upon execution.|
|`descriptionHash`|`bytes32`|The hash of the string of the description of the proposal.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint256`|The unique identifier for the proposal.|


### hasVoted

Returns whether `account` has voted on the proposal with identifier `proposalId`.


```solidity
function hasVoted(uint256 proposalId, address account) external view returns (bool);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`proposalId`|`uint256`|The unique identifier for the proposal.|
|`account`|`address`|   The address of some account.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bool`|Whether `account` has already voted on the proposal.|


### name

Returns the name of the contract.


```solidity
function name() external view returns (string memory);
```

### proposalDeadline

Returns the last clock value when voting on the proposal with identifier `proposalId` is allowed.


```solidity
function proposalDeadline(uint256 proposalId) external view returns (uint256);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`proposalId`|`uint256`|The unique identifier for the proposal.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint256`|The last clock value when voting on the proposal is allowed.|


### proposalProposer

Returns the account that created the proposal with identifier `proposalId`.


```solidity
function proposalProposer(uint256 proposalId) external view returns (address);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`proposalId`|`uint256`|The unique identifier for the proposal.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`address`|The address of the account that created the proposal.|


### proposalSnapshot

Returns the clock value used to retrieve voting power to vote on proposal with identifier `proposalId`.


```solidity
function proposalSnapshot(uint256 proposalId) external view returns (uint256);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`proposalId`|`uint256`|The unique identifier for the proposal.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint256`|The clock value used to retrieve voting power.|


### proposalThreshold

Returns the required voting power an account needs to create a proposal.


```solidity
function proposalThreshold() external view returns (uint256);
```

### quorum

Returns the minimum number of eligible (COUNTING_MODE) votes for a proposal to succeed.


```solidity
function quorum() external view returns (uint256);
```

### quorum

Returns the minimum number of eligible (COUNTING_MODE) votes for a proposal to succeed at `timepoint`.


```solidity
function quorum(uint256 timepoint) external view returns (uint256);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`timepoint`|`uint256`|The point in time, according to the clock mode the contract is operating on.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint256`|The quorum value at `timepoint`.|


### state

Returns the state of a proposal with identifier `proposalId`.


```solidity
function state(uint256 proposalId) external view returns (ProposalState);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`proposalId`|`uint256`|The unique identifier for the proposal.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`ProposalState`|The state of the proposal.|


### votingDelay

Returns the number of clock values that must elapse before voting begins for a newly created proposal.


```solidity
function votingDelay() external view returns (uint256);
```

### votingPeriod

Returns the number of clock values between the vote start and vote end.


```solidity
function votingPeriod() external view returns (uint256);
```

### BALLOT_TYPEHASH

Returns the EIP712 typehash used in the encoding of the digest for `castVoteBySig` function.


```solidity
function BALLOT_TYPEHASH() external pure returns (bytes32);
```

### BALLOT_WITH_REASON_TYPEHASH

Returns the EIP712 typehash used in the encoding of the digest for `castVoteWithReasonBySig` function.


```solidity
function BALLOT_WITH_REASON_TYPEHASH() external pure returns (bytes32);
```

## Events
### ProposalCreated
Emitted when a proposal has been created.


```solidity
event ProposalCreated(
    uint256 proposalId,
    address proposer,
    address[] targets,
    uint256[] values,
    string[] signatures,
    bytes[] callDatas,
    uint256 voteStart,
    uint256 voteEnd,
    string description
);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`proposalId`|`uint256`| The unique identifier for the proposal.|
|`proposer`|`address`|   The address of the account that created the proposal.|
|`targets`|`address[]`|    An array of addresses that will be called upon the execution.|
|`values`|`uint256[]`|     An array of ETH amounts that will be sent to each respective target upon execution.|
|`signatures`|`string[]`| Empty string array required to be compatible with OZ governor contract.|
|`callDatas`|`bytes[]`|  An array of call data used to call each respective target upon execution.|
|`voteStart`|`uint256`|  The first clock value when voting on the proposal is allowed.|
|`voteEnd`|`uint256`|    The last clock value when voting on the proposal is allowed.|
|`description`|`string`|The string of the description of the proposal.|

### ProposalExecuted
Emitted when a proposal has been executed.


```solidity
event ProposalExecuted(uint256 proposalId);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`proposalId`|`uint256`|The unique identifier for the proposal.|

### VoteCast
Emitted when a vote for a proposal with id `proposalId` has been cast by `voter`.


```solidity
event VoteCast(address indexed voter, uint256 proposalId, uint8 support, uint256 weight, string reason);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`voter`|`address`|     The address of the account that has casted their vote.|
|`proposalId`|`uint256`|The unique identifier for the proposal.|
|`support`|`uint8`|   The type of support that has been cast for the proposal.|
|`weight`|`uint256`|    The number of votes cast.|
|`reason`|`string`|    The string of the reason `voter` has cast their vote, if any.|

## Enums
### ProposalState
Proposal state.


```solidity
enum ProposalState {
    Pending,
    Active,
    Canceled,
    Defeated,
    Succeeded,
    Queued,
    Expired,
    Executed
}
```

