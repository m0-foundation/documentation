# IERC6372
[Git Source](https://github.com/MZero-Labs/ttg/blob/0d2761f8db14b390e923f59bdae9799fbf9adf2c/src/abstract/interfaces/IERC6372.sol)

**Author:**
M^0 Labs

*The interface as defined by EIP-6372: https://eips.ethereum.org/EIPS/eip-6372*


## Functions
### CLOCK_MODE

Returns a machine-readable string description of the clock the contract is operating on.


```solidity
function CLOCK_MODE() external view returns (string memory);
```

### clock

Returns the current timepoint according to the mode the contract is operating on.


```solidity
function clock() external view returns (uint48);
```

