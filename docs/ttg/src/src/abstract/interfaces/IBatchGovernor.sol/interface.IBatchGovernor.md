# IBatchGovernor
[Git Source](https://github.com/MZero-Labs/ttg/blob/0d2761f8db14b390e923f59bdae9799fbf9adf2c/src/abstract/interfaces/IBatchGovernor.sol)

**Inherits:**
[IGovernor](/src/abstract/interfaces/IGovernor.sol/interface.IGovernor.md)

**Author:**
M^0 Labs


## Functions
### castVotes

Allows the caller to cast votes on multiple proposals.


```solidity
function castVotes(uint256[] calldata proposalIds, uint8[] calldata supportList) external returns (uint256 weight);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`proposalIds`|`uint256[]`|The list of unique proposal IDs being voted on.|
|`supportList`|`uint8[]`|The list of support type per proposal IDs to cast.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`weight`|`uint256`|     The number of votes cast for each proposal (the same for all of them).|


### castVotesBySig

Allows a signer to cast votes on multiple proposals via an ECDSA secp256k1 signature.


```solidity
function castVotesBySig(uint256[] calldata proposalIds, uint8[] calldata supportList, uint8 v, bytes32 r, bytes32 s)
    external
    returns (uint256 weight);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`proposalIds`|`uint256[]`|The list of unique proposal IDs being voted on.|
|`supportList`|`uint8[]`|The list of support type per proposal IDs to cast.|
|`v`|`uint8`|          An ECDSA secp256k1 signature parameter.|
|`r`|`bytes32`|          An ECDSA secp256k1 signature parameter.|
|`s`|`bytes32`|          An ECDSA secp256k1 signature parameter.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`weight`|`uint256`|     The number of votes cast for each proposal (the same for all of them).|


### castVotesBySig

Allows a signer to cast votes on multiple proposals via an arbitrary signature.


```solidity
function castVotesBySig(
    address voter,
    uint256[] calldata proposalIds,
    uint8[] calldata supportList,
    bytes memory signature
) external returns (uint256 weight);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`voter`|`address`|       The address of the account casting the votes.|
|`proposalIds`|`uint256[]`|The list of unique proposal IDs being voted on.|
|`supportList`|`uint8[]`|The list of support type per proposal IDs to cast.|
|`signature`|`bytes`|  An arbitrary signature|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`weight`|`uint256`|     The number of votes cast for each proposal (the same for all of them).|


### castVotesWithReason

Allows the caller to cast votes with reason on multiple proposals.


```solidity
function castVotesWithReason(uint256[] calldata proposalIds, uint8[] calldata supportList, string[] calldata reasonList)
    external
    returns (uint256 weight);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`proposalIds`|`uint256[]`|The list of unique proposal IDs being voted on.|
|`supportList`|`uint8[]`|The list of support type per proposal IDs to cast.|
|`reasonList`|`string[]`| The list of reason per proposal IDs to cast.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`weight`|`uint256`|     The number of votes cast for each proposal (the same for all of them).|


### castVotesWithReasonBySig

Allows a signer to cast votes with reason on multiple proposals via an ECDSA secp256k1 signature.


```solidity
function castVotesWithReasonBySig(
    uint256[] calldata proposalIds,
    uint8[] calldata supportList,
    string[] calldata reasonList,
    uint8 v,
    bytes32 r,
    bytes32 s
) external returns (uint256 weight);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`proposalIds`|`uint256[]`|The list of unique proposal IDs being voted on.|
|`supportList`|`uint8[]`|The list of support type per proposal IDs to cast.|
|`reasonList`|`string[]`| The list of reason per proposal IDs to cast.|
|`v`|`uint8`|          An ECDSA secp256k1 signature parameter.|
|`r`|`bytes32`|          An ECDSA secp256k1 signature parameter.|
|`s`|`bytes32`|          An ECDSA secp256k1 signature parameter.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`weight`|`uint256`|     The number of votes cast for each proposal (the same for all of them).|


### castVotesWithReasonBySig

Allows a signer to cast votes with reason on multiple proposals via an arbitrary signature.


```solidity
function castVotesWithReasonBySig(
    address voter,
    uint256[] calldata proposalIds,
    uint8[] calldata supportList,
    string[] calldata reasonList,
    bytes memory signature
) external returns (uint256 weight);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`voter`|`address`|      The address of the account casting the votes.|
|`proposalIds`|`uint256[]`|The list of unique proposal IDs being voted on.|
|`supportList`|`uint8[]`|The list of support type per proposal IDs to cast.|
|`reasonList`|`string[]`| The list of reason per proposal IDs to cast.|
|`signature`|`bytes`|  An arbitrary signature|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`weight`|`uint256`|     The number of votes cast for each proposal (the same for all of them).|


### getBallotDigest

Returns the ballot digest to be signed, via EIP-712, given an internal digest (i.e. hash struct).


```solidity
function getBallotDigest(uint256 proposalId, uint8 support) external view returns (bytes32);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`proposalId`|`uint256`|The unique proposal ID being voted on.|
|`support`|`uint8`|   The type of support to cast for the proposal.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bytes32`|The digest to be signed.|


### getBallotsDigest

Returns the ballots digest to be signed, via EIP-712, given an internal digest (i.e. hash struct).


```solidity
function getBallotsDigest(uint256[] calldata proposalIds, uint8[] calldata supportList)
    external
    view
    returns (bytes32);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`proposalIds`|`uint256[]`|The list of unique proposal IDs being voted on.|
|`supportList`|`uint8[]`|The list of support type per proposal IDs to cast.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bytes32`|The digest to be signed.|


### getBallotWithReasonDigest

Returns the ballot with reason digest to be signed, via EIP-712,
given an internal digest (i.e. hash struct).


```solidity
function getBallotWithReasonDigest(uint256 proposalId, uint8 support, string calldata reason)
    external
    view
    returns (bytes32);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`proposalId`|`uint256`|The unique proposal ID being voted on.|
|`support`|`uint8`|   The type of support to cast for the proposal.|
|`reason`|`string`|    The reason for which the caller casts their vote, if any.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bytes32`|The digest to be signed.|


### getBallotsWithReasonDigest

Returns the ballots with reason digest to be signed, via EIP-712,
given an internal digest (i.e. hash struct).


```solidity
function getBallotsWithReasonDigest(
    uint256[] calldata proposalIds,
    uint8[] calldata supportList,
    string[] calldata reasonList
) external view returns (bytes32);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`proposalIds`|`uint256[]`|The list of unique proposal IDs being voted on.|
|`supportList`|`uint8[]`|The list of support type per proposal IDs to cast.|
|`reasonList`|`string[]`| The list of reason per proposal IDs to cast.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bytes32`|The digest to be signed.|


### hashProposal

Returns the unique identifier for the proposal if it were created at this exact moment.


```solidity
function hashProposal(bytes memory callData) external view returns (uint256);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`callData`|`bytes`|The single call data used to call this governor upon execution of a proposal.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint256`|The unique identifier for the proposal.|


### voteToken

Returns the EIP-5805 token contact used for determine voting power and total supplies.


```solidity
function voteToken() external view returns (address);
```

### BALLOTS_TYPEHASH

Returns the EIP712 typehash used in the encoding of the digest for `castVotesBySig` function.


```solidity
function BALLOTS_TYPEHASH() external pure returns (bytes32);
```

### BALLOTS_WITH_REASON_TYPEHASH

Returns the EIP712 typehash used in the encoding of the digest for `castVotesWithReasonBySig` function.


```solidity
function BALLOTS_WITH_REASON_TYPEHASH() external pure returns (bytes32);
```

### ONE

Returns the value used as 100%, to be used to correctly ascertain the threshold ratio.


```solidity
function ONE() external pure returns (uint256);
```

## Errors
### AlreadyVoted
Revert message when a voter is trying to vote on a proposal they already voted on.


```solidity
error AlreadyVoted();
```

### ArrayLengthMismatch
Revert message when input arrays do not match in length.


```solidity
error ArrayLengthMismatch(uint256 length1, uint256 length2);
```

### EmptyProposalIdsArray
Revert message when the proposal IDs array is empty.


```solidity
error EmptyProposalIdsArray();
```

### ExecutionFailed
Revert message when execution of a proposal fails.


```solidity
error ExecutionFailed(bytes data);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`data`|`bytes`|The revert data returned due to the failed execution.|

### InvalidCallData
Revert message when a proposal's call data is not specifically supported.


```solidity
error InvalidCallData();
```

### InvalidCallDatasLength
Revert message when a proposal's call data array is not of length 1.


```solidity
error InvalidCallDatasLength();
```

### InvalidTarget
Revert message when a proposal target is not this governor itself.


```solidity
error InvalidTarget();
```

### InvalidTargetsLength
Revert message when a proposal's targets array is not of length 1.


```solidity
error InvalidTargetsLength();
```

### InvalidValue
Revert message when a proposal value is not 0 ETH.


```solidity
error InvalidValue();
```

### InvalidValuesLength
Revert message when a proposal's values array is not of length 1.


```solidity
error InvalidValuesLength();
```

### InvalidVoteStart
Revert message when a an invalid vote start is detected.


```solidity
error InvalidVoteStart();
```

### InvalidVoteTokenAddress
Revert message when the vote token specified in the constructor is address(0).


```solidity
error InvalidVoteTokenAddress();
```

### NotSelf
Revert message when the caller of a governance-controlled function is not this governor itself.


```solidity
error NotSelf();
```

### ProposalCannotBeExecuted
Revert message when the proposal information provided cannot be executed.


```solidity
error ProposalCannotBeExecuted();
```

### ProposalDoesNotExist
Revert message when the proposal does not exist.


```solidity
error ProposalDoesNotExist();
```

### ProposalExists
Revert message when the proposal already exists.


```solidity
error ProposalExists();
```

### ProposalInactive
Revert message when voting on a proposal that is not in an active state (i.e. not collecting votes).


```solidity
error ProposalInactive(ProposalState state);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`state`|`ProposalState`|The current state of the proposal.|

## Enums
### VoteType
The type of support to cast for a proposal.


```solidity
enum VoteType {
    No,
    Yes
}
```

