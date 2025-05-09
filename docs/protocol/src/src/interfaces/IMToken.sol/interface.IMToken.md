# IMToken
[Git Source](https://github.com/MZero-Labs/protocol/blob/3382fb7336bbc7276e0c3f51da451c9fa6e0016f/src/interfaces/IMToken.sol)

**Inherits:**
[IContinuousIndexing](/src/interfaces/IContinuousIndexing.sol/interface.IContinuousIndexing.md), IERC20Extended

**Author:**
M^0 Labs


## Functions
### mint

Mints tokens.


```solidity
function mint(address account, uint256 amount) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account`|`address`|The address of account to mint to.|
|`amount`|`uint256`| The amount of M Token to mint.|


### burn

Burns tokens.


```solidity
function burn(address account, uint256 amount) external;
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account`|`address`|The address of account to burn from.|
|`amount`|`uint256`| The amount of M Token to burn.|


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

### minterGateway

The address of the Minter Gateway contract.


```solidity
function minterGateway() external view returns (address);
```

### ttgRegistrar

The address of the TTG Registrar contract.


```solidity
function ttgRegistrar() external view returns (address);
```

### rateModel

The address of TTG approved earner rate model.


```solidity
function rateModel() external view returns (address);
```

### earnerRate

The current value of the earner rate in basis points.


```solidity
function earnerRate() external view returns (uint32);
```

### principalBalanceOf

The principal of an earner M token balance.


```solidity
function principalBalanceOf(address account) external view returns (uint240);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account`|`address`|The account to get the principal balance of.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`uint240`|The principal balance of the account.|


### principalOfTotalEarningSupply

The principal of the total earning supply of M Token.


```solidity
function principalOfTotalEarningSupply() external view returns (uint112);
```

### totalEarningSupply

The total earning supply of M Token.


```solidity
function totalEarningSupply() external view returns (uint240);
```

### totalNonEarningSupply

The total non-earning supply of M Token.


```solidity
function totalNonEarningSupply() external view returns (uint240);
```

### isEarning

Checks if account is an earner.


```solidity
function isEarning(address account) external view returns (bool);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account`|`address`|The account to check.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`bool`|True if account is an earner, false otherwise.|


## Events
### StartedEarning
Emitted when account starts being an M earner.


```solidity
event StartedEarning(address indexed account);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account`|`address`|The account that started earning.|

### StoppedEarning
Emitted when account stops being an M earner.


```solidity
event StoppedEarning(address indexed account);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account`|`address`|The account that stopped earning.|

## Errors
### InsufficientBalance
Emitted when there is insufficient balance to decrement from `account`.


```solidity
error InsufficientBalance(address account, uint256 rawBalance, uint256 amount);
```

**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account`|`address`|    The account with insufficient balance.|
|`rawBalance`|`uint256`| The raw balance of the account.|
|`amount`|`uint256`|     The amount to decrement the `rawBalance` by.|

### IsApprovedEarner
Emitted when calling `stopEarning` for an account approved as earner by TTG.


```solidity
error IsApprovedEarner();
```

### NotApprovedEarner
Emitted when calling `startEarning` for an account not approved as earner by TTG.


```solidity
error NotApprovedEarner();
```

### NotMinterGateway
Emitted when calling `mint`, `burn` not by Minter Gateway.


```solidity
error NotMinterGateway();
```

### OverflowsPrincipalOfTotalSupply
Emitted when principal of total supply (earning and non-earning) will overflow a `type(uint112).max`.


```solidity
error OverflowsPrincipalOfTotalSupply();
```

### ZeroMinterGateway
Emitted in constructor if Minter Gateway is 0x0.


```solidity
error ZeroMinterGateway();
```

### ZeroTTGRegistrar
Emitted in constructor if TTG Registrar is 0x0.


```solidity
error ZeroTTGRegistrar();
```

