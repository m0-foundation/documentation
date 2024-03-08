# IEpochBasedInflationaryVoteToken
[Git Source](https://github.com/MZero-Labs/ttg/blob/0d2761f8db14b390e923f59bdae9799fbf9adf2c/src/abstract/interfaces/IEpochBasedInflationaryVoteToken.sol)

**Inherits:**
[IEpochBasedVoteToken](/src/abstract/interfaces/IEpochBasedVoteToken.sol/interface.IEpochBasedVoteToken.md)

**Author:**
M^0 Labs


## Functions
### sync

*Syncs `account` so that its balance Snap array in storage, reflects their unrealized inflation.*


```solidity
function sync(address account) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account`|`address`|The address of the account to sync.|


### hasParticipatedAt

Returns whether `delegatee` has participated in voting during clock value `epoch`.


```solidity
function hasParticipatedAt(address delegatee, uint256 epoch) external view returns (bool);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`delegatee`|`address`|The address of a delegatee with voting power.|
|`epoch`|`uint256`|    The epoch number as a clock value.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bool`|Whether `delegatee` has participated in voting during `epoch`.|


### participationInflation

Returns the participation inflation rate used to inflate tokens for participation.


```solidity
function participationInflation() external view returns (uint16);
```

### ONE

Returns 100% in basis point, to be used to correctly ascertain the participation inflation rate.


```solidity
function ONE() external pure returns (uint16);
```

## Events
### Sync
Emitted when `account` is manually synced.


```solidity
event Sync(address indexed account);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account`|`address`|The address of an account that is synced.|

## Errors
### AlreadyParticipated
Revert message when trying to mark an account as participated in an epoch where it already participated.


```solidity
error AlreadyParticipated();
```

### FutureEpoch
Revert message when the proposed epoch is larger than the current epoch.


```solidity
error FutureEpoch(uint16 currentEpoch, uint16 epoch);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`currentEpoch`|`uint16`|The current epoch clock value.|
|`epoch`|`uint16`|       The handled epoch clock value.|

### InflationTooHigh
Revert message when trying to construct contact with inflation above 100%.


```solidity
error InflationTooHigh();
```

### NotVoteEpoch
Revert message when trying to perform an action not allowed outside of designated voting epochs.


```solidity
error NotVoteEpoch();
```

### VoteEpoch
Revert message when trying to perform an action not allowed during designated voting epochs.


```solidity
error VoteEpoch();
```

