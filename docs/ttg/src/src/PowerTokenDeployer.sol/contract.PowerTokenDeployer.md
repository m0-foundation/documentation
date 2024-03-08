# PowerTokenDeployer
[Git Source](https://github.com/MZero-Labs/ttg/blob/0d2761f8db14b390e923f59bdae9799fbf9adf2c/src/PowerTokenDeployer.sol)

**Inherits:**
[IPowerTokenDeployer](/src/interfaces/IPowerTokenDeployer.sol/interface.IPowerTokenDeployer.md)

**Author:**
M^0 Labs


## State Variables
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


### lastDeploy
Returns the address of the last contract deployed by this contract.


```solidity
address public lastDeploy;
```


### nonce
Returns the nonce used to pre deterministically compute the address of the next deployed contract.


```solidity
uint256 public nonce;
```


## Functions
### constructor

Constructs a new PowerTokenDeployer contract.


```solidity
constructor(address zeroGovernor_, address vault_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`zeroGovernor_`|`address`|The address of the ZeroGovernor contract.|
|`vault_`|`address`|       The address of the Vault contract.|


### deploy

Deploys a new instance of a Power Token.

*Callable only by the Zero Governor.*


```solidity
function deploy(address bootstrapToken_, address standardGovernor_, address cashToken_) external returns (address);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`bootstrapToken_`|`address`||
|`standardGovernor_`|`address`||
|`cashToken_`|`address`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`address`|The address of the deployed Emergency Governor.|


### nextDeploy

Returns the address of the next contract this contract will deploy.


```solidity
function nextDeploy() external view returns (address);
```

