# MToken
[Git Source](https://github.com/MZero-Labs/protocol/blob/3382fb7336bbc7276e0c3f51da451c9fa6e0016f/src/MToken.sol)

**Inherits:**
[IMToken](/src/interfaces/IMToken.sol/interface.IMToken.md), [ContinuousIndexing](/src/abstract/ContinuousIndexing.sol/abstract.ContinuousIndexing.md), ERC20Extended

**Author:**
M^0 Labs

ERC20 M Token.


## State Variables
### minterGateway
The address of the Minter Gateway contract.


```solidity
address public immutable minterGateway;
```


### ttgRegistrar
The address of the TTG Registrar contract.


```solidity
address public immutable ttgRegistrar;
```


### totalNonEarningSupply
The total non-earning supply of M Token.


```solidity
uint240 public totalNonEarningSupply;
```


### principalOfTotalEarningSupply
The principal of the total earning supply of M Token.


```solidity
uint112 public principalOfTotalEarningSupply;
```


### _balances
The balance of M for non-earner or principal of earning M balance for earners.


```solidity
mapping(address account => MBalance balance) internal _balances;
```


## Functions
### onlyMinterGateway

*Modifier to check if caller is Minter Gateway.*


```solidity
modifier onlyMinterGateway();
```

### constructor

Constructs the M Token contract.


```solidity
constructor(address ttgRegistrar_, address minterGateway_) ContinuousIndexing() ERC20Extended("M by M^0", "MONEY", 6);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`ttgRegistrar_`|`address`|The address of the TTG Registrar contract.|
|`minterGateway_`|`address`|    The address of Minter Gateway.|


### mint

Mints tokens.


```solidity
function mint(address account_, uint256 amount_) external onlyMinterGateway;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account_`|`address`||
|`amount_`|`uint256`||


### burn

Burns tokens.


```solidity
function burn(address account_, uint256 amount_) external onlyMinterGateway;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account_`|`address`||
|`amount_`|`uint256`||


### startEarning

Starts earning for caller if allowed by TTG.


```solidity
function startEarning() external;
```

### stopEarning

Stops earning for caller.


```solidity
function stopEarning() external;
```

### rateModel

The address of TTG approved earner rate model.


```solidity
function rateModel() public view returns (address rateModel_);
```

### earnerRate

The current value of earner rate in basis points.


```solidity
function earnerRate() public view returns (uint32 earnerRate_);
```

### totalEarningSupply

The total earning supply of M Token.


```solidity
function totalEarningSupply() public view returns (uint240 totalEarningSupply_);
```

### totalSupply

Returns the amount of tokens in existence.


```solidity
function totalSupply() external view returns (uint256 totalSupply_);
```

### principalBalanceOf

The principal of an earner M token balance.


```solidity
function principalBalanceOf(address account_) external view returns (uint240 balance_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account_`|`address`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`balance_`|`uint240`|The principal balance of the account.|


### balanceOf

Returns the amount of tokens owned by `account`.


```solidity
function balanceOf(address account_) external view returns (uint256 balance_);
```

### isEarning

Checks if account is an earner.


```solidity
function isEarning(address account_) external view returns (bool isEarning_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account_`|`address`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`isEarning_`|`bool`|True if account is an earner, false otherwise.|


### currentIndex

The current index that would be written to storage if `updateIndex` is called.


```solidity
function currentIndex() public view override(ContinuousIndexing, IContinuousIndexing) returns (uint128);
```

### _addEarningAmount

*Adds principal to `_balances` of an earning account.*


```solidity
function _addEarningAmount(address account_, uint112 principalAmount_) internal;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account_`|`address`|        The account to add principal to.|
|`principalAmount_`|`uint112`|The principal amount to add.|


### _addNonEarningAmount

*Adds amount to `_balances` of a non-earning account.*


```solidity
function _addNonEarningAmount(address account_, uint240 amount_) internal;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account_`|`address`|The account to add amount to.|
|`amount_`|`uint240`| The amount to add.|


### _burn

*Burns amount of earning or non-earning M from account.*


```solidity
function _burn(address account_, uint256 amount_) internal;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account_`|`address`|The account to burn from.|
|`amount_`|`uint256`| The present amount to burn.|


### _mint

*Mints amount of earning or non-earning M to account.*


```solidity
function _mint(address recipient_, uint256 amount_) internal;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`recipient_`|`address`|The account to mint to.|
|`amount_`|`uint256`|   The present amount to mint.|


### _startEarning

*Starts earning for account.*


```solidity
function _startEarning(address account_) internal;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account_`|`address`|The account to start earning for.|


### _stopEarning

*Stops earning for account.*


```solidity
function _stopEarning(address account_) internal;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account_`|`address`|The account to stop earning for.|


### _subtractEarningAmount

*Subtracts principal from `_balances` of an earning account.*


```solidity
function _subtractEarningAmount(address account_, uint112 principalAmount_) internal;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account_`|`address`|        The account to subtract principal from.|
|`principalAmount_`|`uint112`|The principal amount to subtract.|


### _subtractNonEarningAmount

*Subtracts amount from `_balances` of a non-earning account.*


```solidity
function _subtractNonEarningAmount(address account_, uint240 amount_) internal;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account_`|`address`|The account to subtract amount from.|
|`amount_`|`uint240`| The amount to subtract.|


### _transfer

*Transfer M between both earning and non-earning accounts.*


```solidity
function _transfer(address sender_, address recipient_, uint256 amount_) internal override;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`sender_`|`address`|   The account to transfer from. It can be either earning or non-earning account.|
|`recipient_`|`address`|The account to transfer to. It can be either earning or non-earning account.|
|`amount_`|`uint256`|   The present amount to transfer.|


### _transferAmountInKind

*Transfer M between same earning status accounts.*


```solidity
function _transferAmountInKind(address sender_, address recipient_, uint240 amount_) internal;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`sender_`|`address`|   The account to transfer from.|
|`recipient_`|`address`|The account to transfer to.|
|`amount_`|`uint240`|   The amount (present or principal) to transfer.|


### _getPresentAmount

*Returns the present amount (rounded down) given the principal amount, using the current index.
All present amounts are rounded down in favor of the protocol.*


```solidity
function _getPresentAmount(uint112 principalAmount_) internal view returns (uint240);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`principalAmount_`|`uint112`|The principal amount.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint240`|The present amount.|


### _getPresentAmount

*Returns the present amount (rounded down) given the principal amount and an index.
All present amounts are rounded down in favor of the protocol, since they are assets.*


```solidity
function _getPresentAmount(uint112 principalAmount_, uint128 index_) internal pure returns (uint240);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`principalAmount_`|`uint112`|The principal amount.|
|`index_`|`uint128`|          An index|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint240`|The present amount.|


### _isApprovedEarner

*Checks if earner was approved by TTG.*


```solidity
function _isApprovedEarner(address account_) internal view returns (bool);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account_`|`address`|   The account to check.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bool`|True if approved, false otherwise.|


### _rate

*Gets the current earner rate from TTG approved rate model contract.*


```solidity
function _rate() internal view override returns (uint32 rate_);
```
**Returns**

|Name|Type|Description|
|----|----|-----------|
|`rate_`|`uint32`|The current earner rate.|


### _revertIfInsufficientAmount

*Reverts if the amount of a `mint` or `burn` is equal to 0.*


```solidity
function _revertIfInsufficientAmount(uint256 amount_) internal pure;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`amount_`|`uint256`|Amount to check.|


### _revertIfInvalidRecipient

*Reverts if the recipient of a `mint` or `transfer` is address(0).*


```solidity
function _revertIfInvalidRecipient(address recipient_) internal pure;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`recipient_`|`address`|Address of the recipient to check.|


### _revertIfNotApprovedEarner

*Reverts if account is not approved earner.*


```solidity
function _revertIfNotApprovedEarner(address account_) internal view;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account_`|`address`|The account to check.|


## Structs
### MBalance
MToken balance struct.


```solidity
struct MBalance {
    bool isEarning;
    uint240 rawBalance;
}
```

**Properties**

|Name|Type|Description|
|----|----|-----------|
|`isEarning`|`bool`| True if the account is earning, false otherwise.|
|`rawBalance`|`uint240`|Balance (for a non earning account) or balance principal (for an earning account).|

