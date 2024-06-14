# PowerToken
[Git Source](https://github.com/MZero-Labs/ttg/blob/0d2761f8db14b390e923f59bdae9799fbf9adf2c/src/PowerToken.sol)

**Inherits:**
[IPowerToken](/src/interfaces/IPowerToken.sol/interface.IPowerToken.md), [EpochBasedInflationaryVoteToken](/src/abstract/EpochBasedInflationaryVoteToken.sol/abstract.EpochBasedInflationaryVoteToken.md)

**Author:**
M^0 Labs


## State Variables
### _AUCTION_PERIODS
*The number of auction periods in an epoch.*


```solidity
uint40 internal constant _AUCTION_PERIODS = 100;
```


### INITIAL_SUPPLY
Returns the initial supply of the token.


```solidity
uint240 public constant INITIAL_SUPPLY = 10_000;
```


### bootstrapToken
Returns the address of the token in which token balances and voting powers are bootstrapped.


```solidity
address public immutable bootstrapToken;
```


### standardGovernor
Returns the address of the Standard Governor.


```solidity
address public immutable standardGovernor;
```


### vault
Returns the address of the Vault.


```solidity
address public immutable vault;
```


### bootstrapEpoch
Returns the epoch from which token balances and voting powers are bootstrapped.


```solidity
uint16 public immutable bootstrapEpoch;
```


### _bootstrapSupply
*The total supply of the bootstrap token at the bootstrap epoch.*


```solidity
uint240 internal immutable _bootstrapSupply;
```


### _nextCashTokenStartingEpoch
*The starting epoch of the next cash token.*


```solidity
uint16 internal _nextCashTokenStartingEpoch;
```


### _cashToken
*The address of the cash token required to buy from the token auction.*


```solidity
address internal _cashToken;
```


### _nextCashToken
*The address of the next cash token.*


```solidity
address internal _nextCashToken;
```


### _nextTargetSupplyStartingEpoch
*The starting epoch of the next target supply.*


```solidity
uint16 internal _nextTargetSupplyStartingEpoch;
```


### _targetSupply
*The current target supply of the token.*


```solidity
uint240 internal _targetSupply;
```


### _nextTargetSupply
*The next target supply of the token.*


```solidity
uint240 internal _nextTargetSupply = INITIAL_SUPPLY;
```


## Functions
### onlyStandardGovernor

*Reverts if the caller is not the Standard Governor.*


```solidity
modifier onlyStandardGovernor();
```

### constructor

Constructs a new Power Token contract.


```solidity
constructor(address bootstrapToken_, address standardGovernor_, address cashToken_, address vault_)
    EpochBasedInflationaryVoteToken("Power Token", "POWER", 0, ONE / 10);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`bootstrapToken_`|`address`|  The address of the token to bootstrap balances and voting powers from.|
|`standardGovernor_`|`address`|The address of the Standard Governor contract to delegate control to.|
|`cashToken_`|`address`|       The address of the token to auction the unowned inflated supply for.|
|`vault_`|`address`|           The address of the vault to transfer cash tokens to.|


### buy

Allows a caller to buy `amount` tokens from the auction.


```solidity
function buy(uint256 minAmount_, uint256 maxAmount_, address destination_, uint16 expiryEpoch_)
    external
    returns (uint240 amount_, uint256 cost_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`minAmount_`|`uint256`||
|`maxAmount_`|`uint256`||
|`destination_`|`address`||
|`expiryEpoch_`|`uint16`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`amount_`|`uint240`|amount      The amount of token bought.|
|`cost_`|`uint256`|cost        The total cash token cost of the purchase.|


### markNextVotingEpochAsActive

Marks the next voting epoch as targeted for inflation.


```solidity
function markNextVotingEpochAsActive() external onlyStandardGovernor;
```

### markParticipation

Marks `delegatee` as having participated in the current epoch, thus receiving voting power inflation.


```solidity
function markParticipation(address delegatee_) external onlyStandardGovernor;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`delegatee_`|`address`||


### setNextCashToken

Queues the cash token that will take effect from the next epoch onward.


```solidity
function setNextCashToken(address nextCashToken_) external onlyStandardGovernor;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`nextCashToken_`|`address`||


### amountToAuction

Returns the amount of tokens that can be bought in the auction.


```solidity
function amountToAuction() public view returns (uint240);
```

### cashToken

Returns the address of the cash token required to buy from the token auction.


```solidity
function cashToken() public view returns (address);
```

### getCost

Returns the total cost, in cash token, of purchasing `amount` tokens from the auction.


```solidity
function getCost(uint256 amount_) public view returns (uint256);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`amount_`|`uint256`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint256`|The total cost, in cash token, of `amount` tokens.|


### targetSupply

Returns the target supply, which helps determine the amount of tokens up for auction.

*Auction curve:
- During every auction period (1/100th of an epoch) the price starts at some "leftPoint" and decreases
linearly, with time, to some "rightPoint" (which is half of that "leftPoint"). This is done by
computing the weighted average between the "leftPoint" and "rightPoint" for the time remaining in
the auction period.
- For the next auction period, the new "leftPoint" is half of the previous period's "leftPoint"
(which also equals the previous period's "rightPoint").
- Combined, this results in the price decreasing by half every auction period at a macro level, but
decreasing linearly at a micro-level during each period, without any jumps.
Relative price computation:
- Since the parameters of this auction are fixed forever (there are no mutable auction parameters and
this is not an upgradeable contract), and the token supply is expected to increase relatively
quickly and consistently, the result would be that the price Y for some Z% of the total supply would
occur earlier and earlier in the auction.
- Instead, the desired behavior is that after X seconds into the auction, there will be a price Y for
some Z% of the total supply. In other words, it will always cost 572,662,306,133 cash tokens to buy
1% of the previous epoch's total supply with 5 days left in the auction period.
- To achieve this, the price is instead computed per basis point of the last epoch's total supply.*


```solidity
function targetSupply() public view returns (uint256);
```

### _bootstrap

*Bootstrap the account's balance and voting power from the bootstrap token.*


```solidity
function _bootstrap(address account_) internal;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account_`|`address`|The account to bootstrap.|


### _delegate

*Delegate voting power from `delegator_` to `newDelegatee_`.*


```solidity
function _delegate(address delegator_, address newDelegatee_) internal override;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`delegator_`|`address`|   The address of the account delegating voting power.|
|`newDelegatee_`|`address`|The address of the account receiving voting power.|


### _sync

*Syncs `account_` so that its balance Snap array in storage, reflects their unrealized inflation.*


```solidity
function _sync(address account_) internal override;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account_`|`address`|The address of the account to sync.|


### _getBalance

*Returns the balance of `account_` plus any inflation that is unrealized before `epoch_`.*


```solidity
function _getBalance(address account_, uint16 epoch_) internal view override returns (uint240);
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


### _getBootstrapBalance

*This is the portion of the initial supply commensurate with
the account's portion of the bootstrap supply.*


```solidity
function _getBootstrapBalance(address account_, uint16 epoch_) internal view returns (uint240);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account_`|`address`|The account to get the bootstrap balance for.|
|`epoch_`|`uint16`|  The epoch to get the bootstrap balance at.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint240`|The bootstrap balance of `account_` at `epoch_`.|


### _getTotalSupply

*Returns the total supply at `epoch_`.*


```solidity
function _getTotalSupply(uint16 epoch_) internal view override returns (uint240);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`epoch_`|`uint16`|The epoch to get the total supply at.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint240`|The total supply at `epoch_`.|


### _getVotes

*Returns the amount of votes of `account_` plus any inflation that should be realized at `epoch_`.*


```solidity
function _getVotes(address account_, uint16 epoch_) internal view override returns (uint240);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account_`|`address`|The account to get the votes for.|
|`epoch_`|`uint16`|  The epoch to get the votes at.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint240`|The votes of `account_` at `epoch_`.|


### _getInternalOrBootstrap

*Returns the amount of balance/votes for `account_` at clock value `epoch_`.*


```solidity
function _getInternalOrBootstrap(
    address account_,
    uint16 epoch_,
    function(address, uint16) internal view returns (uint240) getter_
) internal view returns (uint240);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account_`|`address`|The account to get the balance/votes for.|
|`epoch_`|`uint16`|  The epoch to get the balance/votes at.|
|`getter_`|`function (address, uint16) internal view returns (uint240)`| An internal view function that returns the balance/votes that are internally tracked.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint240`|The balance/votes of `account_` (plus any inflation that should be realized) at `epoch_`.|


### _getLastSync

*Returns the epoch of the last sync of `account_` at or before `epoch_`.*


```solidity
function _getLastSync(address account_, uint16 epoch_) internal view override returns (uint16);
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


### _getTargetSupply

*Returns the target supply of the token at the current epoch.*


```solidity
function _getTargetSupply() internal view returns (uint240);
```

### _revertIfNotStandardGovernor

*Reverts if the caller is not the Standard Governor.*


```solidity
function _revertIfNotStandardGovernor() internal view;
```

### _divideUp

*Helper function to calculate `x` / `y`, rounded up.*

*Inspired by USM (https://github.com/usmfum/USM/blob/master/contracts/WadMath.sol)*


```solidity
function _divideUp(uint256 x, uint256 y) internal pure returns (uint256 z);
```

