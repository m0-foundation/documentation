# EpochBasedVoteToken
[Git Source](https://github.com/MZero-Labs/ttg/blob/0d2761f8db14b390e923f59bdae9799fbf9adf2c/src/abstract/EpochBasedVoteToken.sol)

**Inherits:**
[IEpochBasedVoteToken](/src/abstract/interfaces/IEpochBasedVoteToken.sol/interface.IEpochBasedVoteToken.md), [ERC5805](/src/abstract/ERC5805.sol/abstract.ERC5805.md), ERC20Extended

**Author:**
M^0 Labs


## State Variables
### _totalSupplies
*Store the total supply per epoch.*


```solidity
AmountSnap[] internal _totalSupplies;
```


### _balances
*Store the balance per epoch per account.*


```solidity
mapping(address account => AmountSnap[] balanceSnaps) internal _balances;
```


### _delegatees
*Store the delegatee per epoch per account.*


```solidity
mapping(address account => AccountSnap[] delegateeSnaps) internal _delegatees;
```


### _votingPowers
*Store the voting power per epoch per delegatee.*


```solidity
mapping(address delegatee => AmountSnap[] votingPowerSnaps) internal _votingPowers;
```


## Functions
### constructor

Constructs a new EpochBasedVoteToken contract.


```solidity
constructor(string memory name_, string memory symbol_, uint8 decimals_) ERC20Extended(name_, symbol_, decimals_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`name_`|`string`|    The name of the token.|
|`symbol_`|`string`|  The symbol of the token.|
|`decimals_`|`uint8`|The decimals of the token.|


### delegateBySig

Changes the voting power delegation for `account` to `delegatee`.


```solidity
function delegateBySig(address account_, address delegatee_, uint256 nonce_, uint256 expiry_, bytes memory signature_)
    external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account_`|`address`||
|`delegatee_`|`address`||
|`nonce_`|`uint256`||
|`expiry_`|`uint256`||
|`signature_`|`bytes`||


### balanceOf

Returns the amount of tokens owned by `account`.


```solidity
function balanceOf(address account_) external view returns (uint256);
```

### getDelegationDigest

Returns the digest to be signed, via EIP-712, given an internal digest (i.e. hash struct).


```solidity
function getDelegationDigest(address delegatee_, uint256 nonce_, uint256 expiry_) external view returns (bytes32);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`delegatee_`|`address`||
|`nonce_`|`uint256`||
|`expiry_`|`uint256`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bytes32`|The digest to be signed.|


### pastBalanceOf

Returns the token balance of `account` at a past clock value `epoch`.


```solidity
function pastBalanceOf(address account_, uint256 epoch_) external view returns (uint256);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account_`|`address`||
|`epoch_`|`uint256`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint256`|The token balance `account` at `epoch`.|


### clock

Returns the current timepoint according to the mode the contract is operating on.


```solidity
function clock() external view returns (uint48 clock_);
```

### delegates

Returns the delegatee the voting power of `account` is delegated to.


```solidity
function delegates(address account_) external view returns (address);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account_`|`address`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`address`|The address of the account the voting power of `account` will be delegated to.|


### pastDelegates

Returns the delegatee of `account` at a past clock value `epoch`.


```solidity
function pastDelegates(address account_, uint256 epoch_) external view returns (address);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account_`|`address`||
|`epoch_`|`uint256`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`address`|The delegatee of the voting power of `account` at `epoch`.|


### getVotes

Returns the total voting power of `account`.


```solidity
function getVotes(address account_) external view returns (uint256);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account_`|`address`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint256`|The total voting power of `account`.|


### getPastVotes

Returns the total voting power of `account` at a past clock value `timepoint`.


```solidity
function getPastVotes(address account_, uint256 epoch_) external view returns (uint256);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account_`|`address`||
|`epoch_`|`uint256`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint256`|The total voting power of `account` at clock value `timepoint`.|


### totalSupply

Returns the amount of tokens in existence.


```solidity
function totalSupply() external view returns (uint256);
```

### pastTotalSupply

Returns the total token supply at a past clock value `epoch`.


```solidity
function pastTotalSupply(uint256 epoch_) external view returns (uint256);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`epoch_`|`uint256`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint256`|The total token supply at `epoch`.|


### CLOCK_MODE

Returns a machine-readable string description of the clock the contract is operating on.


```solidity
function CLOCK_MODE() external pure returns (string memory clockMode_);
```

### _addBalance

*Add `amount_` to the balance of `account_`, using unchecked math.*


```solidity
function _addBalance(address account_, uint240 amount_) internal;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account_`|`address`|The address of the account to add the balance to.|
|`amount_`|`uint240`| The amount to add to the balance.|


### _addTotalSupply

*Add `amount_` to the total supply, using checked math.*


```solidity
function _addTotalSupply(uint240 amount_) internal;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`amount_`|`uint240`|The amount to add to the total supply.|


### _addVotingPower

*Add `amount_` to the voting power of `account_`, using unchecked math.*


```solidity
function _addVotingPower(address account_, uint240 amount_) internal;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account_`|`address`|The address of the account to add the voting power to.|
|`amount_`|`uint240`| The amount to add to the voting power.|


### _delegate

*Set a new delegatee for `delegator_`.*


```solidity
function _delegate(address delegator_, address newDelegatee_) internal virtual override;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`delegator_`|`address`|   The address of the account delegating voting power.|
|`newDelegatee_`|`address`|The address of the account receiving voting power.|


### _mint

*Mint `amount_` tokens to `recipient_`.*


```solidity
function _mint(address recipient_, uint256 amount_) internal virtual;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`recipient_`|`address`|The address of the account to mint tokens to.|
|`amount_`|`uint256`|   The amount of tokens to mint.|


### _removeBalance

*Subtract `amount_` from the balance of `account_`, using checked math.*


```solidity
function _removeBalance(address account_, uint240 amount_) internal;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account_`|`address`|The address of the account to subtract the balance from.|
|`amount_`|`uint240`| The amount to subtract from the balance.|


### _removeVotingPower

*Subtract `amount_` of voting power from the balance of `account_`, using checked math.*


```solidity
function _removeVotingPower(address account_, uint240 amount_) internal;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account_`|`address`|The address of the account to subtract the voting power from.|
|`amount_`|`uint240`| The amount of voting power to subtract.|


### _setDelegatee

*Set a new delegatee for `delegator_`.*


```solidity
function _setDelegatee(address delegator_, address delegatee_) internal returns (address oldDelegatee_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`delegator_`|`address`|   The address of the account delegating voting power.|
|`delegatee_`|`address`|   The address of the account receiving voting power.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`oldDelegatee_`|`address`|The address of the previous delegatee of `delegator_`.|


### _transfer

*Transfer `amount_` tokens from `sender_` to `recipient_`.*


```solidity
function _transfer(address sender_, address recipient_, uint256 amount_) internal virtual override;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`sender_`|`address`|   The address of the account to transfer tokens from.|
|`recipient_`|`address`|The address of the account to transfer tokens to.|
|`amount_`|`uint256`|   The amount of tokens to transfer.|


### _update

*Update a storage AmountSnap by `amount_` given `operation_`.*


```solidity
function _update(
    AmountSnap[] storage amountSnaps_,
    function(uint240, uint240) internal pure returns (uint240) operation_,
    uint240 amount_
) internal returns (uint240 oldAmount_, uint240 newAmount_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`amountSnaps_`|`AmountSnap[]`|The storage pointer to an AmountSnap array to update.|
|`operation_`|`function (uint240, uint240) internal pure returns (uint240)`|  The operation to perform on the old and new amounts.|
|`amount_`|`uint240`|     The amount to update the Snap by.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`oldAmount_`|`uint240`|  The previous latest amount of the Snap array.|
|`newAmount_`|`uint240`|  The new latest amount of the Snap array.|


### _updateBalance

*Update the balance of `account_` by `amount_` given `operation_`.*


```solidity
function _updateBalance(
    address account_,
    function(uint240, uint240) internal pure returns (uint240) operation_,
    uint240 amount_
) internal;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account_`|`address`|  The address of the account to update the balance of.|
|`operation_`|`function (uint240, uint240) internal pure returns (uint240)`|The operation to perform on the old and new amounts.|
|`amount_`|`uint240`|   The amount to update the balance by.|


### _updateVotingPower

*Update the voting power of `delegatee_` by `amount_` given `operation_`.*


```solidity
function _updateVotingPower(
    address delegatee_,
    function(uint240, uint240) internal pure returns (uint240) operation_,
    uint240 amount_
) internal;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`delegatee_`|`address`|The address of the account to update the voting power of.|
|`operation_`|`function (uint240, uint240) internal pure returns (uint240)`|The operation to perform on the old and new amounts.|
|`amount_`|`uint240`|   The amount to update the voting power by.|


### _clock

*Returns the current timepoint according to the mode the contract is operating on.*


```solidity
function _clock() internal view returns (uint16);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint16`|Current timepoint.|


### _getBalance

*Get the balance of `account_` at `epoch_`.*


```solidity
function _getBalance(address account_, uint16 epoch_) internal view virtual returns (uint240);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account_`|`address`|The address of the account to get the balance of.|
|`epoch_`|`uint16`|  The epoch to get the balance at.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint240`|The balance of `account_` at `epoch_`.|


### _getDelegatee

*Get the delegatee of `account_` at `epoch_`.*

*The delegatee is the account itself (the default) if the retrieved delegatee is address(0).*


```solidity
function _getDelegatee(address account_, uint256 epoch_) internal view virtual returns (address);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account_`|`address`|The address of the account to get the delegatee of.|
|`epoch_`|`uint256`|  The epoch to get the delegatee at.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`address`|The delegatee of `account_` at `epoch_`.|


### _getTotalSupply

*Get the total supply at `epoch_`.*


```solidity
function _getTotalSupply(uint16 epoch_) internal view virtual returns (uint240);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`epoch_`|`uint16`|The epoch to get the total supply at.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint240`|The total supply at `epoch_`.|


### _getValueAt

*Get the value of an AmountSnap array at a given epoch.*


```solidity
function _getValueAt(AmountSnap[] storage amountSnaps_, uint16 epoch_) internal view returns (uint240);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`amountSnaps_`|`AmountSnap[]`|The array of AmountSnaps to get the value of.|
|`epoch_`|`uint16`|      The epoch to get the value at.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint240`|The value of the AmountSnap array at `epoch_`.|


### _getVotes

*The votes of `account_` at `epoch_`.*


```solidity
function _getVotes(address account_, uint16 epoch_) internal view virtual returns (uint240);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account_`|`address`|The address of the account to get the votes of.|
|`epoch_`|`uint16`|  The epoch to get the votes at.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint240`|The votes of `account_` at `epoch_`.|


### _revertIfNotPastTimepoint

*Revert if `epoch_` is not in the past.*


```solidity
function _revertIfNotPastTimepoint(uint16 epoch_) internal view;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`epoch_`|`uint16`|The epoch to check.|


### _revertIfInvalidRecipient

*Reverts if the recipient of a `mint` or `transfer` is address(0).*


```solidity
function _revertIfInvalidRecipient(address recipient_) internal pure;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`recipient_`|`address`|Address of the recipient to check.|


### _add

*Add `b_` to `a_`, using checked math.*


```solidity
function _add(uint240 a_, uint240 b_) internal pure returns (uint240);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`a_`|`uint240`|The amount to add to.|
|`b_`|`uint240`|The amount to add.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint240`|The sum of `a_` and `b_`.|


### _addUnchecked

*Add `b_` to `a_`, using unchecked math.*


```solidity
function _addUnchecked(uint240 a_, uint240 b_) internal pure returns (uint240);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`a_`|`uint240`|The amount to add to.|
|`b_`|`uint240`|The amount to add.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint240`|The sum of `a_` and `b_`.|


### _getDefaultIfZero

*Return `default_` if `input_` is equal to address(0), else return `input_`.*


```solidity
function _getDefaultIfZero(address input_, address default_) internal pure returns (address);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`input_`|`address`|  The input address.|
|`default_`|`address`|The default address.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`address`|The input address if not equal to the zero address, else the default address.|


### _sub

*Subtract `b_` from `a_`, using checked math.*


```solidity
function _sub(uint240 a_, uint240 b_) internal pure returns (uint240);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`a_`|`uint240`|The amount to subtract from.|
|`b_`|`uint240`|The amount to subtract.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint240`|The difference of `a_` and `b_`.|


### _unsafeAccess

*Returns the AmountSnap in an array at a given index without doing bounds checking.*


```solidity
function _unsafeAccess(AmountSnap[] storage amountSnaps_, uint256 index_)
    internal
    pure
    returns (AmountSnap storage amountSnap_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`amountSnaps_`|`AmountSnap[]`|The array of AmountSnaps to parse.|
|`index_`|`uint256`|      The index of the AmountSnap to return.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`amountSnap_`|`AmountSnap`| The AmountSnap at `index_`.|


### _unsafeAccess

*Returns the AccountSnap in an array at a given index without doing bounds checking.*


```solidity
function _unsafeAccess(AccountSnap[] storage accountSnaps_, uint256 index_)
    internal
    pure
    returns (AccountSnap storage accountSnap_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`accountSnaps_`|`AccountSnap[]`|The array of AccountSnaps to parse.|
|`index_`|`uint256`|       The index of the AccountSnap to return.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`accountSnap_`|`AccountSnap`| The AccountSnap at `index_`.|


## Structs
### AccountSnap
*A 32-byte struct containing a starting epoch and an address that is valid until the next AccountSnap.*


```solidity
struct AccountSnap {
    uint16 startingEpoch;
    address account;
}
```

### AmountSnap
*A 32-byte struct containing a starting epoch and an amount that is valid until the next AmountSnap.*


```solidity
struct AmountSnap {
    uint16 startingEpoch;
    uint240 amount;
}
```

