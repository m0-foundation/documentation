# StandardGovernor
[Git Source](https://github.com/MZero-Labs/ttg/blob/0d2761f8db14b390e923f59bdae9799fbf9adf2c/src/StandardGovernor.sol)

**Inherits:**
[IStandardGovernor](/src/interfaces/IStandardGovernor.sol/interface.IStandardGovernor.md), [BatchGovernor](/src/abstract/BatchGovernor.sol/abstract.BatchGovernor.md)

**Author:**
M^0 Labs


## State Variables
### emergencyGovernor
Returns the address of the Emergency Governor.


```solidity
address public immutable emergencyGovernor;
```


### registrar
Returns the address of the Registrar.


```solidity
address public immutable registrar;
```


### vault
Returns the address of the Vault.


```solidity
address public immutable vault;
```


### zeroGovernor
Returns the address of the Zero Governor.


```solidity
address public immutable zeroGovernor;
```


### zeroToken
Returns the address of the Zero Token.


```solidity
address public immutable zeroToken;
```


### maxTotalZeroRewardPerActiveEpoch
Returns the maximum amount of Zero Token that can be rewarded to all vote casters per active epoch.


```solidity
uint256 public immutable maxTotalZeroRewardPerActiveEpoch;
```


### cashToken
Returns the address of the Cash Token.


```solidity
address public cashToken;
```


### proposalFee
Returns the required amount of cashToken it costs an account to create a proposal.


```solidity
uint256 public proposalFee;
```


### _proposalFees
*The proposal fee info per proposal ID.*


```solidity
mapping(uint256 proposalId => ProposalFeeInfo proposalFee) internal _proposalFees;
```


### numberOfProposalsAt
*The amount of proposals per epoch.*


```solidity
mapping(uint256 epoch => uint256 count) public numberOfProposalsAt;
```


### numberOfProposalsVotedOnAt
*The amount of proposals a voter has voted on per epoch.*


```solidity
mapping(address voter => mapping(uint256 epoch => uint256 count)) public numberOfProposalsVotedOnAt;
```


## Functions
### onlyZeroGovernor

*Revert if the caller is not the Zero Governor.*


```solidity
modifier onlyZeroGovernor();
```

### onlySelfOrEmergencyGovernor

*Revert if the caller is not the Standard Governor nor the Emergency Governor.*


```solidity
modifier onlySelfOrEmergencyGovernor();
```

### constructor

Constructs a new StandardGovernor contract.


```solidity
constructor(
    address voteToken_,
    address emergencyGovernor_,
    address zeroGovernor_,
    address cashToken_,
    address registrar_,
    address vault_,
    address zeroToken_,
    uint256 proposalFee_,
    uint256 maxTotalZeroRewardPerActiveEpoch_
) BatchGovernor("StandardGovernor", voteToken_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`voteToken_`|`address`|                       The address of the Vote Token contract.|
|`emergencyGovernor_`|`address`|               The address of the Emergency Governor contract.|
|`zeroGovernor_`|`address`|                    The address of the Zero Governor contract.|
|`cashToken_`|`address`|                       The address of the Cash Token contract.|
|`registrar_`|`address`|                       The address of the Registrar contract.|
|`vault_`|`address`|                           The address of the Vault contract.|
|`zeroToken_`|`address`|                       The address of the Zero Token contract.|
|`proposalFee_`|`uint256`|                     The proposal fee.|
|`maxTotalZeroRewardPerActiveEpoch_`|`uint256`|The maximum amount of zero tokens to reward per active epoch.|


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
) external override returns (uint256 proposalId_);
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


### setCashToken

Set the cash token and proposal fee to be used to create proposals going forward.


```solidity
function setCashToken(address newCashToken_, uint256 newProposalFee_) external onlyZeroGovernor;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`newCashToken_`|`address`||
|`newProposalFee_`|`uint256`||


### sendProposalFeeToVault

Sends the proposal fee for proposal `proposalId` to the vault, if it is Defeated or Expired.


```solidity
function sendProposalFeeToVault(uint256 proposalId_) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`proposalId_`|`uint256`||


### addToList

One of the valid proposals. Adds `account` to `list` at the Registrar.


```solidity
function addToList(bytes32 list_, address account_) external onlySelf;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`list_`|`bytes32`||
|`account_`|`address`||


### removeFromList

One of the valid proposals. Removes `account` to `list` at the Registrar.


```solidity
function removeFromList(bytes32 list_, address account_) external onlySelf;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`list_`|`bytes32`||
|`account_`|`address`||


### removeFromAndAddToList

One of the valid proposals. Removes `accountToRemove` and adds `accountToAdd` to `list` at the Registrar.


```solidity
function removeFromAndAddToList(bytes32 list_, address accountToRemove_, address accountToAdd_) external onlySelf;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`list_`|`bytes32`||
|`accountToRemove_`|`address`||
|`accountToAdd_`|`address`||


### setKey

One of the valid proposals. Sets `key` to `value` at the Registrar.


```solidity
function setKey(bytes32 key_, bytes32 value_) external onlySelf;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`key_`|`bytes32`||
|`value_`|`bytes32`||


### setProposalFee

One of the valid proposals. Sets the proposal fee of the Standard Governor.


```solidity
function setProposalFee(uint256 newProposalFee_) external onlySelfOrEmergencyGovernor;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`newProposalFee_`|`uint256`||


### getProposal

Returns all the proposal details for a proposal with identifier `proposalId`.


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
        address proposer_
    );
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`proposalId_`|`uint256`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`voteStart_`|`uint48`|voteStart  The first clock value when voting on the proposal is allowed.|
|`voteEnd_`|`uint48`|voteEnd    The last clock value when voting on the proposal is allowed.|
|`state_`|`ProposalState`|state      The state of the proposal.|
|`noVotes_`|`uint256`|noVotes    The amount of votes cast against the proposal.|
|`yesVotes_`|`uint256`|yesVotes   The amount of votes cast for the proposal.|
|`proposer_`|`address`|proposer   The address of the account that created the proposal.|


### getProposalFee

Returns the proposal fee information.


```solidity
function getProposalFee(uint256 proposalId_) external view returns (address cashToken_, uint256 fee_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`proposalId_`|`uint256`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`cashToken_`|`address`|cashToken  The address of the cash token for this particular proposal fee.|
|`fee_`|`uint256`|amount     The amount of cash token of the proposal fee.|


### hasVotedOnAllProposals

Returns whether `voter` has voted on all proposals in `epoch`.


```solidity
function hasVotedOnAllProposals(address voter_, uint256 epoch_) external view returns (bool);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`voter_`|`address`||
|`epoch_`|`uint256`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bool`|Whether `voter` has voted on all proposals in `epoch`.|


### quorum

Returns the minimum number of eligible (COUNTING_MODE) votes for a proposal to succeed.


```solidity
function quorum() external pure returns (uint256);
```

### quorum

Returns the minimum number of eligible (COUNTING_MODE) votes for a proposal to succeed.


```solidity
function quorum(uint256) external pure returns (uint256);
```

### state

Returns the state of a proposal with identifier `proposalId`.


```solidity
function state(uint256 proposalId_) public view override(BatchGovernor, IGovernor) returns (ProposalState);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`proposalId_`|`uint256`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`ProposalState`|The state of the proposal.|


### _castVotes

*Cast votes on several proposals for `voter_`.*


```solidity
function _castVotes(
    address voter_,
    uint256[] calldata proposalIds_,
    uint8[] calldata supportList_,
    string[] memory reasonList_
) internal override returns (uint256 weight_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`voter_`|`address`|      The address of the voter.|
|`proposalIds_`|`uint256[]`|The unique identifiers of the proposals.|
|`supportList_`|`uint8[]`|The type of support to cast for each proposal.|
|`reasonList_`|`string[]`| The list of reason per proposal IDs to cast.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`weight_`|`uint256`|     The number of votes the voter cast on each proposal.|


### _addToList

*Adds `account` to `list` at the Registrar.*


```solidity
function _addToList(bytes32 list_, address account_) internal;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`list_`|`bytes32`|   The key for some list.|
|`account_`|`address`|The address of some account to be added.|


### _castVote

*Cast `weight_` votes on a proposal with id `proposalId_` for `voter_`.*


```solidity
function _castVote(address voter_, uint256 weight_, uint256 proposalId_, uint8 support_, string memory reason_)
    internal
    override;
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
function _createProposal(uint256 proposalId_, uint16 voteStart_) internal override;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`proposalId_`|`uint256`|The unique identifier of the proposal.|
|`voteStart_`|`uint16`| The epoch at which the proposal will start collecting votes.|


### _removeFromList

*Removes `account_` from `list_` at the Registrar.*


```solidity
function _removeFromList(bytes32 list_, address account_) internal;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`list_`|`bytes32`|   The key for some list.|
|`account_`|`address`|The address of some account to be removed.|


### _setCashToken

*Set cash token to `newCashToken_`.*


```solidity
function _setCashToken(address newCashToken_) internal;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`newCashToken_`|`address`|The address of the new cash token.|


### _setProposalFee

*Set proposal fee to `newProposalFee_`.*


```solidity
function _setProposalFee(uint256 newProposalFee_) internal;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`newProposalFee_`|`uint256`|The new proposal fee.|


### _transfer

*Transfer `amount_` of `token_` to `to_`.*


```solidity
function _transfer(address token_, address to_, uint256 amount_) internal;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`token_`|`address`| The address of the token to transfer.|
|`to_`|`address`|    The address of the recipient.|
|`amount_`|`uint256`|The amount of tokens to transfer.|


### _votingDelay

*Returns the number of clock values that must elapse before voting begins for a newly created proposal.*


```solidity
function _votingDelay() internal view override returns (uint16);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint16`|The voting delay.|


### _revertIfInvalidCalldata

*All proposals target this contract itself, and must call one of the listed functions to be valid.*


```solidity
function _revertIfInvalidCalldata(bytes memory callData_) internal pure override;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`callData_`|`bytes`|The call data to check.|


### _votingPeriod

*Returns the number of clock values between the vote start and vote end.*


```solidity
function _votingPeriod() internal pure override returns (uint16);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint16`|The voting period.|


## Structs
### ProposalFeeInfo
The proposal fee info.


```solidity
struct ProposalFeeInfo {
    address cashToken;
    uint256 fee;
}
```

**Properties**

|Name|Type|Description|
|----|----|-----------|
|`cashToken`|`address`|The address of the cash token used to pay the fee.|
|`fee`|`uint256`|      The amount of the fee per proposal.|

