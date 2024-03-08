# BatchGovernor
[Git Source](https://github.com/MZero-Labs/ttg/blob/0d2761f8db14b390e923f59bdae9799fbf9adf2c/src/abstract/BatchGovernor.sol)

**Inherits:**
[IBatchGovernor](/src/abstract/interfaces/IBatchGovernor.sol/interface.IBatchGovernor.md), ERC712Extended

**Author:**
M^0 Labs


## State Variables
### _SELECTOR_PLUS_0_ARGS
*Length constant for calldata with no argument.*


```solidity
uint256 internal constant _SELECTOR_PLUS_0_ARGS = 4;
```


### _SELECTOR_PLUS_1_ARGS
*Length constant for calldata with one argument.*


```solidity
uint256 internal constant _SELECTOR_PLUS_1_ARGS = 36;
```


### _SELECTOR_PLUS_2_ARGS
*Length constant for calldata with two arguments.*


```solidity
uint256 internal constant _SELECTOR_PLUS_2_ARGS = 68;
```


### _SELECTOR_PLUS_3_ARGS
*Length constant for calldata with three arguments.*


```solidity
uint256 internal constant _SELECTOR_PLUS_3_ARGS = 100;
```


### ONE
Returns the value used as 100%, to be used to correctly ascertain the threshold ratio.


```solidity
uint256 public constant ONE = 10_000;
```


### BALLOT_TYPEHASH
Returns the EIP712 typehash used in the encoding of the digest for `castVoteBySig` function.


```solidity
bytes32 public constant BALLOT_TYPEHASH = 0x150214d74d59b7d1e90c73fc22ef3d991dd0a76b046543d4d80ab92d2a50328f;
```


### BALLOT_WITH_REASON_TYPEHASH
Returns the EIP712 typehash used in the encoding of the digest for `castVoteWithReasonBySig` function.


```solidity
bytes32 public constant BALLOT_WITH_REASON_TYPEHASH = 0x7949bd92105c02f48ca245aa185f4a7a4d7185641d59b186ac64abeb44964f0c;
```


### BALLOTS_TYPEHASH
Returns the EIP712 typehash used in the encoding of the digest for `castVotesBySig` function.


```solidity
bytes32 public constant BALLOTS_TYPEHASH = 0x9a121fc10d6025acfc09275f9709796b68831733b5bbac0d510d13f85b1b730f;
```


### BALLOTS_WITH_REASON_TYPEHASH
Returns the EIP712 typehash used in the encoding of the digest for `castVotesWithReasonBySig` function.


```solidity
bytes32 public constant BALLOTS_WITH_REASON_TYPEHASH =
    0xa891f76027ef63a24501b9dd3b0c779b49ad26d2328e9d423640209d1ad4fcc4;
```


### voteToken
Returns the EIP-5805 token contact used for determine voting power and total supplies.


```solidity
address public immutable voteToken;
```


### _proposals
*The list of proposals per proposal ID.*


```solidity
mapping(uint256 proposalId => Proposal proposal) internal _proposals;
```


### hasVoted
Returns whether `account` has voted on the proposal with identifier `proposalId`.


```solidity
mapping(uint256 proposalId => mapping(address voter => bool hasVoted)) public hasVoted;
```


## Functions
### onlySelf

*Reverts if the caller is not the contract itself.*


```solidity
modifier onlySelf();
```

### constructor

Construct a new BatchGovernor contract.


```solidity
constructor(string memory name_, address voteToken_) ERC712Extended(name_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`name_`|`string`|     The name of the contract. Used to compute EIP712 domain separator.|
|`voteToken_`|`address`|The address of the token used to vote.|


### castVote

Allows the caller to cast a vote on a proposal with id `proposalId`.


```solidity
function castVote(uint256 proposalId_, uint8 support_) external returns (uint256 weight_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`proposalId_`|`uint256`||
|`support_`|`uint8`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`weight_`|`uint256`|weight     The number of votes cast.|


### castVotes

Allows the caller to cast votes on multiple proposals.


```solidity
function castVotes(uint256[] calldata proposalIds_, uint8[] calldata supportList_) external returns (uint256 weight_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`proposalIds_`|`uint256[]`||
|`supportList_`|`uint8[]`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`weight_`|`uint256`|weight      The number of votes cast for each proposal (the same for all of them).|


### castVoteWithReason

Allows the caller to cast a vote with reason on a proposal with id `proposalId`.


```solidity
function castVoteWithReason(uint256 proposalId_, uint8 support_, string calldata reason_)
    external
    returns (uint256 weight_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`proposalId_`|`uint256`||
|`support_`|`uint8`||
|`reason_`|`string`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`weight_`|`uint256`|weight     The number of votes cast.|


### castVotesWithReason

Allows the caller to cast votes with reason on multiple proposals.


```solidity
function castVotesWithReason(
    uint256[] calldata proposalIds_,
    uint8[] calldata supportList_,
    string[] calldata reasonList_
) external returns (uint256 weight_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`proposalIds_`|`uint256[]`||
|`supportList_`|`uint8[]`||
|`reasonList_`|`string[]`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`weight_`|`uint256`|weight      The number of votes cast for each proposal (the same for all of them).|


### castVoteBySig

Allows a signer to cast a vote on a proposal with id `proposalId` via an ECDSA secp256k1 signature.


```solidity
function castVoteBySig(uint256 proposalId_, uint8 support_, uint8 v_, bytes32 r_, bytes32 s_)
    external
    returns (uint256 weight_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`proposalId_`|`uint256`||
|`support_`|`uint8`||
|`v_`|`uint8`||
|`r_`|`bytes32`||
|`s_`|`bytes32`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`weight_`|`uint256`|weight     The number of votes cast.|


### castVoteBySig

Allows a signer to cast a vote on a proposal with id `proposalId` via an ECDSA secp256k1 signature.


```solidity
function castVoteBySig(address voter_, uint256 proposalId_, uint8 support_, bytes memory signature_)
    external
    returns (uint256 weight_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`voter_`|`address`||
|`proposalId_`|`uint256`||
|`support_`|`uint8`||
|`signature_`|`bytes`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`weight_`|`uint256`|weight     The number of votes cast.|


### castVotesBySig

Allows a signer to cast votes on multiple proposals via an ECDSA secp256k1 signature.


```solidity
function castVotesBySig(
    uint256[] calldata proposalIds_,
    uint8[] calldata supportList_,
    uint8 v_,
    bytes32 r_,
    bytes32 s_
) external returns (uint256 weight_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`proposalIds_`|`uint256[]`||
|`supportList_`|`uint8[]`||
|`v_`|`uint8`||
|`r_`|`bytes32`||
|`s_`|`bytes32`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`weight_`|`uint256`|weight      The number of votes cast for each proposal (the same for all of them).|


### castVotesBySig

Allows a signer to cast votes on multiple proposals via an ECDSA secp256k1 signature.


```solidity
function castVotesBySig(
    address voter_,
    uint256[] calldata proposalIds_,
    uint8[] calldata supportList_,
    bytes memory signature_
) external returns (uint256 weight_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`voter_`|`address`||
|`proposalIds_`|`uint256[]`||
|`supportList_`|`uint8[]`||
|`signature_`|`bytes`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`weight_`|`uint256`|weight      The number of votes cast for each proposal (the same for all of them).|


### castVoteWithReasonBySig

Allows a signer to cast a vote with reason on a proposal with id `proposalId`
via an ECDSA secp256k1 signature.


```solidity
function castVoteWithReasonBySig(
    uint256 proposalId_,
    uint8 support_,
    string calldata reason_,
    uint8 v_,
    bytes32 r_,
    bytes32 s_
) external returns (uint256 weight_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`proposalId_`|`uint256`||
|`support_`|`uint8`||
|`reason_`|`string`||
|`v_`|`uint8`||
|`r_`|`bytes32`||
|`s_`|`bytes32`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`weight_`|`uint256`|weight     The number of votes cast.|


### castVoteWithReasonBySig

Allows a signer to cast a vote with reason on a proposal with id `proposalId`
via an ECDSA secp256k1 signature.


```solidity
function castVoteWithReasonBySig(
    address voter_,
    uint256 proposalId_,
    uint8 support_,
    string calldata reason_,
    bytes memory signature_
) external returns (uint256 weight_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`voter_`|`address`||
|`proposalId_`|`uint256`||
|`support_`|`uint8`||
|`reason_`|`string`||
|`signature_`|`bytes`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`weight_`|`uint256`|weight     The number of votes cast.|


### castVotesWithReasonBySig

Allows a signer to cast votes with reason on multiple proposals via an ECDSA secp256k1 signature.


```solidity
function castVotesWithReasonBySig(
    uint256[] calldata proposalIds_,
    uint8[] calldata supportList_,
    string[] calldata reasonList_,
    uint8 v_,
    bytes32 r_,
    bytes32 s_
) external returns (uint256 weight_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`proposalIds_`|`uint256[]`||
|`supportList_`|`uint8[]`||
|`reasonList_`|`string[]`||
|`v_`|`uint8`||
|`r_`|`bytes32`||
|`s_`|`bytes32`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`weight_`|`uint256`|weight      The number of votes cast for each proposal (the same for all of them).|


### castVotesWithReasonBySig

Allows a signer to cast votes with reason on multiple proposals via an ECDSA secp256k1 signature.


```solidity
function castVotesWithReasonBySig(
    address voter_,
    uint256[] calldata proposalIds_,
    uint8[] calldata supportList_,
    string[] calldata reasonList_,
    bytes memory signature_
) external returns (uint256 weight_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`voter_`|`address`||
|`proposalIds_`|`uint256[]`||
|`supportList_`|`uint8[]`||
|`reasonList_`|`string[]`||
|`signature_`|`bytes`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`weight_`|`uint256`|weight      The number of votes cast for each proposal (the same for all of them).|


### hashProposal

Returns the unique identifier for the proposal if it were created at this exact moment.


```solidity
function hashProposal(address[] memory, uint256[] memory, bytes[] memory callDatas_, bytes32)
    external
    view
    returns (uint256);
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
|`<none>`|`uint256`|The unique identifier for the proposal.|


### hashProposal

Returns the unique identifier for the proposal if it were created at this exact moment.


```solidity
function hashProposal(bytes memory callData_) external view returns (uint256);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`callData_`|`bytes`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint256`|The unique identifier for the proposal.|


### name

Returns the name of the contract.


```solidity
function name() external view returns (string memory);
```

### proposalDeadline

Returns the last clock value when voting on the proposal with identifier `proposalId` is allowed.


```solidity
function proposalDeadline(uint256 proposalId_) external view returns (uint256);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`proposalId_`|`uint256`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint256`|The last clock value when voting on the proposal is allowed.|


### proposalProposer

Returns the account that created the proposal with identifier `proposalId`.


```solidity
function proposalProposer(uint256 proposalId_) external view returns (address);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`proposalId_`|`uint256`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`address`|The address of the account that created the proposal.|


### proposalSnapshot

Returns the clock value used to retrieve voting power to vote on proposal with identifier `proposalId`.


```solidity
function proposalSnapshot(uint256 proposalId_) external view returns (uint256);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`proposalId_`|`uint256`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint256`|The clock value used to retrieve voting power.|


### CLOCK_MODE

Returns a machine-readable string description of the clock the contract is operating on.


```solidity
function CLOCK_MODE() external pure returns (string memory);
```

### COUNTING_MODE

module:voting

*A description of the possible "support" values for castVote and the way these votes are counted, meant to
be consumed by UIs to show correct vote options and interpret the results. The string is a URL-encoded
sequence of key-value pairs that each describe one aspect, for example `support=for,against&quorum=for`.
The string can be decoded by the standard URLSearchParams JavaScript class.*


```solidity
function COUNTING_MODE() external pure returns (string memory);
```

### proposalThreshold

Returns the required voting power an account needs to create a proposal.


```solidity
function proposalThreshold() external pure returns (uint256);
```

### clock

Returns the current timepoint according to the mode the contract is operating on.


```solidity
function clock() public view returns (uint48);
```

### getBallotDigest

Returns the ballot digest to be signed, via EIP-712, given an internal digest (i.e. hash struct).


```solidity
function getBallotDigest(uint256 proposalId_, uint8 support_) external view returns (bytes32);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`proposalId_`|`uint256`||
|`support_`|`uint8`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bytes32`|The digest to be signed.|


### getBallotsDigest

Returns the ballots digest to be signed, via EIP-712, given an internal digest (i.e. hash struct).


```solidity
function getBallotsDigest(uint256[] calldata proposalIds_, uint8[] calldata supportList_)
    external
    view
    returns (bytes32);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`proposalIds_`|`uint256[]`||
|`supportList_`|`uint8[]`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bytes32`|The digest to be signed.|


### getBallotWithReasonDigest

Returns the ballot with reason digest to be signed, via EIP-712,
given an internal digest (i.e. hash struct).


```solidity
function getBallotWithReasonDigest(uint256 proposalId_, uint8 support_, string calldata reason_)
    external
    view
    returns (bytes32);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`proposalId_`|`uint256`||
|`support_`|`uint8`||
|`reason_`|`string`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bytes32`|The digest to be signed.|


### getBallotsWithReasonDigest

Returns the ballots with reason digest to be signed, via EIP-712,
given an internal digest (i.e. hash struct).


```solidity
function getBallotsWithReasonDigest(
    uint256[] calldata proposalIds_,
    uint8[] calldata supportList_,
    string[] calldata reasonList_
) external view returns (bytes32);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`proposalIds_`|`uint256[]`||
|`supportList_`|`uint8[]`||
|`reasonList_`|`string[]`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bytes32`|The digest to be signed.|


### getVotes

Returns the voting power of `account` at clock value `timepoint`.


```solidity
function getVotes(address account_, uint256 timepoint_) public view returns (uint256);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account_`|`address`||
|`timepoint_`|`uint256`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint256`|The voting power of `account` at `timepoint`.|


### state

Returns the state of a proposal with identifier `proposalId`.


```solidity
function state(uint256 proposalId_) public view virtual returns (ProposalState);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`proposalId_`|`uint256`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`ProposalState`|The state of the proposal.|


### votingDelay

Returns the number of clock values that must elapse before voting begins for a newly created proposal.


```solidity
function votingDelay() public view returns (uint256);
```

### votingPeriod

Returns the number of clock values between the vote start and vote end.


```solidity
function votingPeriod() public view returns (uint256);
```

### _castVotes

*Cast votes on several proposals for `voter_`.*


```solidity
function _castVotes(
    address voter_,
    uint256[] calldata proposalIds_,
    uint8[] calldata supportList_,
    string[] memory reasonList_
) internal virtual returns (uint256 weight_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`voter_`|`address`|      The address of the voter.|
|`proposalIds_`|`uint256[]`|The list of unique proposal IDs being voted on.|
|`supportList_`|`uint8[]`|The list of support type per proposal IDs to cast.|
|`reasonList_`|`string[]`| The list of reason per proposal IDs to cast.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`weight_`|`uint256`|     The number of votes the voter cast on each proposal.|


### _castVote

*Cast votes on proposal for `voter_`.*


```solidity
function _castVote(address voter_, uint256 proposalId_, uint8 support_, string memory reason_)
    internal
    returns (uint256 weight_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`voter_`|`address`|     The address of the voter.|
|`proposalId_`|`uint256`|The unique identifier of the proposal.|
|`support_`|`uint8`|   The type of support to cast for the proposal.|
|`reason_`|`string`|    The reason for which the caller casts their vote, if any.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`weight_`|`uint256`|    The number of votes cast.|


### _castVote

*Cast `weight_` votes on a proposal with id `proposalId_` for `voter_`.*


```solidity
function _castVote(address voter_, uint256 weight_, uint256 proposalId_, uint8 support_, string memory reason_)
    internal
    virtual;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`voter_`|`address`|     The address of the voter.|
|`weight_`|`uint256`|    The number of votes the voter is casting.|
|`proposalId_`|`uint256`|The unique identifier of the proposal.|
|`support_`|`uint8`|   The type of support to cast for the proposal.|
|`reason_`|`string`|    The reason for which the caller casts their vote, if any.|


### _createProposal

*Creates a new proposal with the given parameters.*


```solidity
function _createProposal(uint256 proposalId_, uint16 voteStart_) internal virtual;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`proposalId_`|`uint256`|The unique identifier of the proposal.|
|`voteStart_`|`uint16`| The epoch at which the proposal will start collecting votes.|


### _execute

*Executes a proposal given its call data and voteStart (which are unique to it).*


```solidity
function _execute(bytes memory callData_, uint16 voteStart_) internal virtual returns (uint256 proposalId_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`callData_`|`bytes`|  The call data to execute.|
|`voteStart_`|`uint16`| The epoch at which the proposal started collecting votes.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`proposalId_`|`uint256`|The unique identifier of the proposal that matched the criteria.|


### _propose

*Internal handler for making proposals.*


```solidity
function _propose(
    address[] memory targets_,
    uint256[] memory values_,
    bytes[] memory callDatas_,
    string memory description_
) internal returns (uint256 proposalId_, uint16 voteStart_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`targets_`|`address[]`|    An array of addresses that will be called upon the execution.|
|`values_`|`uint256[]`|     An array of ETH amounts that will be sent to each respective target upon execution.|
|`callDatas_`|`bytes[]`|  An array of call data used to call each respective target upon execution.|
|`description_`|`string`|The string of the description of the proposal.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`proposalId_`|`uint256`| The unique identifier of the proposal.|
|`voteStart_`|`uint16`|  The timepoint at which voting on the proposal begins, inclusively.|


### _tryExecute

*This function tries to execute a proposal based on the call data and a range of possible vote starts.
This is needed due to the fact that proposalId's are generated based on the call data and vote start
time, and so an executed function will need this in order to attempt to find and execute a proposal given
a known range of possible vote start times which depends on how the inheriting implementation
determines the vote start time and expiry of proposals based on the time of the proposal creation.*


```solidity
function _tryExecute(bytes memory callData_, uint16 latestVoteStart_, uint16 earliestVoteStart_)
    internal
    returns (uint256 proposalId_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`callData_`|`bytes`|         An array of call data used to call each respective target upon execution.|
|`latestVoteStart_`|`uint16`|  The most recent vote start to use in attempting to search for the proposal.|
|`earliestVoteStart_`|`uint16`|The least recent vote start to use in attempting to search for the proposal.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`proposalId_`|`uint256`|       The unique identifier of the most recent proposal that matched the criteria.|


### _clock

*Returns the current timepoint according to the mode the contract is operating on.*


```solidity
function _clock() internal view returns (uint16);
```

### _getTotalSupply

*Returns the vote token's total supply at `timepoint`.*


```solidity
function _getTotalSupply(uint16 timepoint_) internal view returns (uint256);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`timepoint_`|`uint16`|The clock value at which to query the vote token's total supply.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint256`|The vote token's total supply at the `timepoint` clock value.|


### _voteStart

*Returns the timepoint at which voting would start for a proposal created in current timepoint.*


```solidity
function _voteStart() internal view returns (uint16);
```

### _getVoteEnd

*Returns the timepoint at which voting would end given a timepoint at which voting would start.*


```solidity
function _getVoteEnd(uint16 voteStart_) internal view returns (uint16);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`voteStart_`|`uint16`|The clock value at which voting would start, inclusively.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint16`|The clock value at which voting would end, inclusively.|


### _getBallotDigest

*Returns the ballot digest to be signed, via EIP-712, given an internal digest (i.e. hash struct).*


```solidity
function _getBallotDigest(uint256 proposalId_, uint8 support_) internal view returns (bytes32);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`proposalId_`|`uint256`|The unique proposal ID being voted on.|
|`support_`|`uint8`|   The type of support to cast for the proposal.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bytes32`|The digest to be signed.|


### _getBallotsDigest

*Returns the ballots digest to be signed, via EIP-712, given an internal digest (i.e. hash struct).*


```solidity
function _getBallotsDigest(bytes32 proposalIdsHash_, bytes32 supportListHash_) internal view returns (bytes32);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`proposalIdsHash_`|`bytes32`|The hash of the list of unique proposal IDs being voted on.|
|`supportListHash_`|`bytes32`|The hash of the list of support type per proposal IDs to cast.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bytes32`|The digest to be signed.|


### _getBallotWithReasonDigest

*Returns the ballot with reason digest to be signed, via EIP-712,
given an internal digest (i.e. hash struct).*


```solidity
function _getBallotWithReasonDigest(uint256 proposalId_, uint8 support_, string calldata reason_)
    internal
    view
    returns (bytes32);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`proposalId_`|`uint256`|The unique proposal ID being voted on.|
|`support_`|`uint8`|   The type of support to cast for the proposal.|
|`reason_`|`string`|    The reason for which the caller casts their vote, if any.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bytes32`|The digest to be signed.|


### _getBallotsWithReasonDigest

*Returns the ballots digest to be signed, via EIP-712, given an internal digest (i.e. hash struct).*


```solidity
function _getBallotsWithReasonDigest(bytes32 proposalIdsHash_, bytes32 supportListHash_, bytes32 reasonListHash_)
    internal
    view
    returns (bytes32);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`proposalIdsHash_`|`bytes32`|The hash of the list of unique proposal IDs being voted on.|
|`supportListHash_`|`bytes32`|The hash of the list of support type per proposal IDs to cast.|
|`reasonListHash_`|`bytes32`| The hash of the list of reason per proposal IDs to cast.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bytes32`|The digest to be signed.|


### _getReasonListHash

*Returns the hash of the reason list to be used in the ballots digest.*


```solidity
function _getReasonListHash(string[] calldata reasonList_) internal pure returns (bytes32);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`reasonList_`|`string[]`|The list of reasons to hash.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bytes32`|The hash of the reason list.|


### _hashProposal

*Returns the unique identifier for the proposal if it were created at this exact moment.*


```solidity
function _hashProposal(bytes memory callData_) internal view returns (uint256);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`callData_`|`bytes`|The single call data used to call this governor upon execution of a proposal.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint256`|The unique identifier for the proposal.|


### _hashProposal

*Returns the unique identifier for the proposal if it were to have a given vote start timepoint.*


```solidity
function _hashProposal(bytes memory callData_, uint16 voteStart_) internal view returns (uint256);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`callData_`|`bytes`| The single call data used to call this governor upon execution of a proposal.|
|`voteStart_`|`uint16`|The clock value at which voting would start, inclusively.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint256`|The unique identifier for the proposal.|


### _revertIfNotSelf

*Reverts if the caller is not the contract itself.*


```solidity
function _revertIfNotSelf() internal view;
```

### _votingDelay

*Returns the number of clock values that must elapse before voting begins for a newly created proposal.*


```solidity
function _votingDelay() internal view virtual returns (uint16);
```

### _votingPeriod

*Returns the number of clock values between the vote start and vote end.*


```solidity
function _votingPeriod() internal view virtual returns (uint16);
```

### _revertIfInvalidCalldata

*All proposals target this contract itself, and must call one of the listed functions to be valid.*


```solidity
function _revertIfInvalidCalldata(bytes memory callData_) internal pure virtual;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`callData_`|`bytes`|The call data to check.|


## Structs
### Proposal
Proposal struct for storing all relevant proposal information.


```solidity
struct Proposal {
    uint16 voteStart;
    bool executed;
    address proposer;
    uint16 thresholdRatio;
    uint16 quorumRatio;
    uint256 noWeight;
    uint256 yesWeight;
}
```

**Properties**

|Name|Type|Description|
|----|----|-----------|
|`voteStart`|`uint16`|     The epoch at which voting begins, inclusively.|
|`executed`|`bool`|      Whether or not the proposal has been executed.|
|`proposer`|`address`|      The address of the proposer.|
|`thresholdRatio`|`uint16`|The ratio of yes votes required for a proposal to succeed.|
|`quorumRatio`|`uint16`|   The ratio of total votes required for a proposal to succeed.|
|`noWeight`|`uint256`|      The total number of votes against the proposal.|
|`yesWeight`|`uint256`|     The total number of votes for the proposal.|

