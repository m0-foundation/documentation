# IDeployer
[Git Source](https://github.com/MZero-Labs/ttg/blob/0d2761f8db14b390e923f59bdae9799fbf9adf2c/src/interfaces/IDeployer.sol)

**Author:**
M^0 Labs


## Functions
### nonce

Returns the nonce used to pre deterministically compute the address of the next deployed contract.


```solidity
function nonce() external view returns (uint256);
```

### lastDeploy

Returns the address of the last contract deployed by this contract.


```solidity
function lastDeploy() external view returns (address);
```

### nextDeploy

Returns the address of the next contract this contract will deploy.


```solidity
function nextDeploy() external view returns (address);
```

