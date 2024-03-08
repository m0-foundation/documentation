# EpochBasedInflationaryVoteToken
[Git Source](https://github.com/MZero-Labs/ttg/blob/0d2761f8db14b390e923f59bdae9799fbf9adf2c/src/abstract/EpochBasedInflationaryVoteToken.sol)

**Inherits:**
[IEpochBasedInflationaryVoteToken](/src/abstract/interfaces/IEpochBasedInflationaryVoteToken.sol/interface.IEpochBasedInflationaryVoteToken.md), [EpochBasedVoteToken](/src/abstract/EpochBasedVoteToken.sol/abstract.EpochBasedVoteToken.md)

**Author:**
M^0 Labs


## State Variables
### ONE
Returns 100% in basis point, to be used to correctly ascertain the participation inflation rate.


```solidity
uint16 public constant ONE = 10_000;
```


### participationInflation
Returns the participation inflation rate used to inflate tokens for participation.


```solidity
uint16 public immutable participationInflation;
```


### _participations
*A mapping of delegatees to their participation snaps, marking epochs in which they have participated.*


```solidity
mapping(address delegatee => VoidSnap[] participationSnaps) internal _participations;
```


## Functions
### notDuringVoteEpoch

*Reverts if the current epoch is a voting epoch.*


```solidity
modifier notDuringVoteEpoch();
```

### onlyDuringVoteEpoch

*Reverts if the current epoch is not a voting epoch.*


```solidity
modifier onlyDuringVoteEpoch();
```

### constructor

Constructs a new EpochBasedInflationaryVoteToken contract.


```solidity
constructor(string memory name_, string memory symbol_, uint8 decimals_, uint16 participationInflation_)
    EpochBasedVoteToken(name_, symbol_, decimals_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`name_`|`string`|                  The name of the token.|
|`symbol_`|`string`|                The symbol of the token.|
|`decimals_`|`uint8`|              The decimals of the token.|
|`participationInflation_`|`uint16`|The participation inflation rate used to inflate tokens for participation.|


### sync

*Syncs `account` so that its balance Snap array in storage, reflects their unrealized inflation.*


```solidity
function sync(address account_) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account_`|`address`||


### hasParticipatedAt

Returns whether `delegatee` has participated in voting during clock value `epoch`.


```solidity
function hasParticipatedAt(address delegatee_, uint256 epoch_) external view returns (bool);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`delegatee_`|`address`||
|`epoch_`|`uint256`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bool`|Whether `delegatee` has participated in voting during `epoch`.|


### _delegate

*Delegate voting power from `delegator_` to `newDelegatee_`.*


```solidity
function _delegate(address delegator_, address newDelegatee_) internal virtual override notDuringVoteEpoch;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`delegator_`|`address`|   The address of the account delegating voting power.|
|`newDelegatee_`|`address`|The address of the account receiving voting power.|


### _markParticipation

*Allows for the inflation of a delegatee's voting power (and total supply) up to one time per epoch.*


```solidity
function _markParticipation(address delegatee_) internal onlyDuringVoteEpoch;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`delegatee_`|`address`|The address of the account being marked as having participated.|


### _mint

*Mint `amount_` tokens to `recipient_`.*


```solidity
function _mint(address recipient_, uint256 amount_) internal override notDuringVoteEpoch;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`recipient_`|`address`|The address of the account to mint tokens to.|
|`amount_`|`uint256`|   The amount of tokens to mint.|


### _sync

*Syncs `account_` so that its balance Snap array in storage, reflects their unrealized inflation.*


```solidity
function _sync(address account_) internal virtual;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account_`|`address`|The address of the account to sync.|


### _transfer

*Transfers `amount_` tokens from `sender_` to `recipient_`.*


```solidity
function _transfer(address sender_, address recipient_, uint256 amount_) internal override notDuringVoteEpoch;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`sender_`|`address`|   The address of the account to transfer tokens from.|
|`recipient_`|`address`|The address of the account to transfer tokens to.|
|`amount_`|`uint256`|   The amount of tokens to transfer.|


### _update

*Update a storage VoidSnap array to contain the current epoch as the latest snap.*


```solidity
function _update(VoidSnap[] storage voidSnaps_, uint16 epoch_) internal returns (bool updated_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`voidSnaps_`|`VoidSnap[]`|The storage pointer to a VoidSnap array to update.|
|`epoch_`|`uint16`|    The epoch to write as the latest element of the VoidSnap array.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`updated_`|`bool`|  Whether the VoidSnap array was updated, and thus did not already contain the current epoch.|


### _getBalance

*Returns the balance of `account_` plus any inflation that in unrealized before `epoch_`.*


```solidity
function _getBalance(address account_, uint16 epoch_) internal view virtual override returns (uint240);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account_`|`address`|The account to get the balance for.|
|`epoch_`|`uint16`|  The epoch to get the balance at.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint240`|The balance of `account_` plus any inflation that is unrealized before `epoch_`.|


### _getBalanceWithoutUnrealizedInflation

*Returns the balance of `account_` at `epoch_` without any unrealized inflation.*


```solidity
function _getBalanceWithoutUnrealizedInflation(address account_, uint16 epoch_)
    internal
    view
    virtual
    returns (uint240);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account_`|`address`|The account to get the balance for.|
|`epoch_`|`uint16`|  The epoch to get the balance at.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint240`|The balance of `account_` at `epoch` without any unrealized inflation.|


### _getInflation

*Returns the inflation of `amount` due to participation inflation.*


```solidity
function _getInflation(uint240 amount_) internal view returns (uint240);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`amount_`|`uint240`|The amount to determine inflation for.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint240`|The inflation of `amount` due to participation inflation.|


### _getLastSync

*Returns the epoch of the last sync of `account_` at or before `epoch_`.
Override this function in order to return the "default"/starting epoch if the account has never synced.*


```solidity
function _getLastSync(address account_, uint16 epoch_) internal view virtual returns (uint16);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account_`|`address`|The account to get the last sync for.|
|`epoch_`|`uint16`|  The epoch to get the last sync at or before.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint16`|The epoch of the last sync of `account_` at or before `epoch_`.|


### _hasParticipatedAt

*Returns whether `delegatee_` has participated during the clock value `epoch_`.*


```solidity
function _hasParticipatedAt(address delegatee_, uint16 epoch_) internal view returns (bool);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`delegatee_`|`address`|The account whose participation is being queried.|
|`epoch_`|`uint16`|    The epoch at which to determine participation.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bool`|Whether `delegatee_` has participated during the clock value `epoch_`.|


### _getUnrealizedInflation

*Returns the unrealized inflation for `account_` from their last sync to the epoch before `lastEpoch_`.*


```solidity
function _getUnrealizedInflation(address account_, uint16 lastEpoch_) internal view returns (uint240 inflation_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account_`|`address`|  The account being queried.|
|`lastEpoch_`|`uint16`|The last epoch at which to determine unrealized inflation, not inclusive.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`inflation_`|`uint240`|The total unrealized inflation that has yet to be synced.|


### _revertIfInVoteEpoch

*Reverts if the current epoch is a voting epoch.*


```solidity
function _revertIfInVoteEpoch() internal view;
```

### _revertIfNotInVoteEpoch

*Reverts if the current epoch is not a voting epoch.*


```solidity
function _revertIfNotInVoteEpoch() internal view;
```

### _isVotingEpoch

*Returns whether the clock value `epoch_` is a voting epoch or not.*


```solidity
function _isVotingEpoch(uint16 epoch_) internal pure returns (bool);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`epoch_`|`uint16`|Some clock value.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bool`|Whether the epoch is a voting epoch.|


### _unsafeAccess

*Returns the VoidSnap in an array at a given index without doing bounds checking.*


```solidity
function _unsafeAccess(VoidSnap[] storage voidSnaps_, uint256 index_)
    internal
    pure
    returns (VoidSnap storage voidSnap_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`voidSnaps_`|`VoidSnap[]`|The array of VoidSnaps to parse.|
|`index_`|`uint256`|    The index of the VoidSnap to return.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`voidSnap_`|`VoidSnap`| The VoidSnap at `index_`.|


## Structs
### VoidSnap
*A 32-byte struct containing a starting epoch that merely marks that something occurred in this epoch.*


```solidity
struct VoidSnap {
    uint16 startingEpoch;
}
```

