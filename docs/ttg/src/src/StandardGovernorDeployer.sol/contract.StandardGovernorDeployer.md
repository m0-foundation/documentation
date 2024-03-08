# StandardGovernorDeployer
[Git Source](https://github.com/MZero-Labs/ttg/blob/0d2761f8db14b390e923f59bdae9799fbf9adf2c/src/StandardGovernorDeployer.sol)

**Inherits:**
[IStandardGovernorDeployer](/src/interfaces/IStandardGovernorDeployer.sol/interface.IStandardGovernorDeployer.md)

**Author:**
M^0 Labs


## State Variables
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
### onlyZeroGovernor

*Throws if called by any contract other than the Zero Governor.*


```solidity
modifier onlyZeroGovernor();
```

### constructor

Constructs a new StandardGovernorDeployer contract.


```solidity
constructor(address zeroGovernor_, address registrar_, address vault_, address zeroToken_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`zeroGovernor_`|`address`|The address of the ZeroGovernor contract.|
|`registrar_`|`address`|   The address of the Registrar contract.|
|`vault_`|`address`|       The address of the Vault contract.|
|`zeroToken_`|`address`|   The address of the ZeroToken contract.|


### deploy

Deploys a new instance of a Standard Governor.


```solidity
function deploy(
    address powerToken_,
    address emergencyGovernor_,
    address cashToken_,
    uint256 proposalFee_,
    uint256 maxTotalZeroRewardPerActiveEpoch_
) external onlyZeroGovernor returns (address);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`powerToken_`|`address`||
|`emergencyGovernor_`|`address`||
|`cashToken_`|`address`||
|`proposalFee_`|`uint256`||
|`maxTotalZeroRewardPerActiveEpoch_`|`uint256`||

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`<none>`|`address`|The address of the deployed Standard Governor.|


### nextDeploy

Returns the address of the next contract this contract will deploy.


```solidity
function nextDeploy() external view returns (address);
```

