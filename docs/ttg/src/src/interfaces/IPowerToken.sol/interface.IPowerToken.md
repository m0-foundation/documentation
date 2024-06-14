# IPowerToken
[Git Source](https://github.com/MZero-Labs/ttg/blob/0d2761f8db14b390e923f59bdae9799fbf9adf2c/src/interfaces/IPowerToken.sol)

**Inherits:**
[IEpochBasedInflationaryVoteToken](/src/abstract/interfaces/IEpochBasedInflationaryVoteToken.sol/interface.IEpochBasedInflationaryVoteToken.md)

**Author:**
M^0 Labs


## Functions
### buy

Allows a caller to buy `amount` tokens from the auction.


```solidity
function buy(uint256 minAmount, uint256 maxAmount, address destination, uint16 expiryEpoch)
    external
    returns (uint240 amount, uint256 cost);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`minAmount`|`uint256`|  The minimum amount of tokens the caller is interested in buying.|
|`maxAmount`|`uint256`|  The maximum amount of tokens the caller is interested in buying.|
|`destination`|`address`|The address of the account to send the bought tokens.|
|`expiryEpoch`|`uint16`|The epoch number at the end of which the buy order expires.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`amount`|`uint240`|     The amount of token bought.|
|`cost`|`uint256`|       The total cash token cost of the purchase.|


### markNextVotingEpochAsActive

Marks the next voting epoch as targeted for inflation.


```solidity
function markNextVotingEpochAsActive() external;
```

### markParticipation

Marks `delegatee` as having participated in the current epoch, thus receiving voting power inflation.


```solidity
function markParticipation(address delegatee) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`delegatee`|`address`|The address of the account being marked as having participated.|


### setNextCashToken

Queues the cash token that will take effect from the next epoch onward.


```solidity
function setNextCashToken(address nextCashToken) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`nextCashToken`|`address`|The address of the cash token taking effect from the next epoch onward.|


### amountToAuction

Returns the amount of tokens that can be bought in the auction.


```solidity
function amountToAuction() external view returns (uint240);
```

### bootstrapEpoch

Returns the epoch from which token balances and voting powers are bootstrapped.


```solidity
function bootstrapEpoch() external view returns (uint16);
```

### bootstrapToken

Returns the address of the token in which token balances and voting powers are bootstrapped.


```solidity
function bootstrapToken() external view returns (address);
```

### cashToken

Returns the address of the cash token required to buy from the token auction.


```solidity
function cashToken() external view returns (address);
```

### getCost

Returns the total cost, in cash token, of purchasing `amount` tokens from the auction.


```solidity
function getCost(uint256 amount) external view returns (uint256);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`amount`|`uint256`|Some amount of tokens.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint256`|The total cost, in cash token, of `amount` tokens.|


### standardGovernor

Returns the address of the Standard Governor.


```solidity
function standardGovernor() external view returns (address);
```

### targetSupply

Returns the target supply, which helps determine the amount of tokens up for auction.


```solidity
function targetSupply() external view returns (uint256);
```

### vault

Returns the address of the Vault.


```solidity
function vault() external view returns (address);
```

### INITIAL_SUPPLY

Returns the initial supply of the token.


```solidity
function INITIAL_SUPPLY() external pure returns (uint240);
```

## Events
### Buy
Emitted when `buyer` has bought `amount` tokens from the auction, as a total cash token value of `cost`.


```solidity
event Buy(address indexed buyer, uint240 amount, uint256 cost);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`buyer`|`address`| The address of the account that bought tokens from the auction.|
|`amount`|`uint240`|The amount of tokens bought.|
|`cost`|`uint256`|  The total cash token cost of the purchase.|

### NextCashTokenSet
Emitted when the cash token is queued to become `nextCashToken` at the start of epoch `startingEpoch`.


```solidity
event NextCashTokenSet(uint16 indexed startingEpoch, address indexed nextCashToken);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`startingEpoch`|`uint16`|The epoch number as a clock value in which the new cash token takes effect.|
|`nextCashToken`|`address`|The address of the cash token taking effect at `startingEpoch`.|

### Tagline
Emitted in the constructor at deployment.


```solidity
event Tagline(string tagline);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`tagline`|`string`|The tagline of the contract.|

### TargetSupplyInflated
Emitted when the target supply is queued to become `targetSupply` at the start of epoch `targetEpoch`.


```solidity
event TargetSupplyInflated(uint16 indexed targetEpoch, uint240 indexed targetSupply);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`targetEpoch`|`uint16`| The epoch number as a clock value in which the new target supply takes effect.|
|`targetSupply`|`uint240`|The target supply taking effect at `startingEpoch`.|

## Errors
### BootstrapSupplyTooLarge
Revert message when the total supply of the bootstrap token is larger than `type(uint240).max`.


```solidity
error BootstrapSupplyTooLarge();
```

### BootstrapSupplyZero
Revert message when the total supply of the bootstrap token is 0.


```solidity
error BootstrapSupplyZero();
```

### InsufficientAuctionSupply
Revert message when the amount available for auction is less than the minimum requested to buy.


```solidity
error InsufficientAuctionSupply(uint240 amountToAuction, uint240 minAmountRequested);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`amountToAuction`|`uint240`|   The amount available for auction.|
|`minAmountRequested`|`uint240`|The minimum amount that was requested to buy.|

### InvalidBootstrapTokenAddress
Revert message when the Bootstrap Token specified in the constructor is address(0).


```solidity
error InvalidBootstrapTokenAddress();
```

### InvalidCashTokenAddress
Revert message when the Cash Token specified in the constructor is address(0).


```solidity
error InvalidCashTokenAddress();
```

### InvalidStandardGovernorAddress
Revert message when the Standard Governor specified in the constructor is address(0).


```solidity
error InvalidStandardGovernorAddress();
```

### InvalidVaultAddress
Revert message when the Vault specified in the constructor is address(0).


```solidity
error InvalidVaultAddress();
```

### NotStandardGovernor
Revert message when the caller is not the Standard Governor.


```solidity
error NotStandardGovernor();
```

### TransferFromFailed
Revert message when a token transferFrom fails.


```solidity
error TransferFromFailed();
```

### DivisionByZero
Revert message when auction calculations use zero as denominator.


```solidity
error DivisionByZero();
```

### ExpiredBuyOrder
Revert message when the buy order has expired using epoch-based expiration clock.


```solidity
error ExpiredBuyOrder();
```

### ZeroPurchaseAmount
Revert message when the buy order has zero maximum and minimum amounts.


```solidity
error ZeroPurchaseAmount();
```

### SyncBeforeBootstrap
Revert message when trying to sync to an epoch that is before the bootstrap epoch.


```solidity
error SyncBeforeBootstrap(uint16 bootstrapEpoch, uint16 epoch);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`bootstrapEpoch`|`uint16`|The bootstrap epoch.|
|`epoch`|`uint16`|         The epoch attempting to be synced to, not inclusively.|

