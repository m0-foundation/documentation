# IERC712Extended
[Git Source](https://github.com/MZero-Labs/common/blob/9da96e78d24aadd41ee6f776b7b028203782b632/src/interfaces/IERC712Extended.sol)

**Inherits:**
[IERC712](/src/interfaces/IERC712.sol/interface.IERC712.md)

**Author:**
M^0 Labs

*The additional interface as defined by EIP-5267: https://eips.ethereum.org/EIPS/eip-5267*


## Functions
### eip712Domain

Returns the fields and values that describe the domain separator used by this contract for EIP-712.


```solidity
function eip712Domain()
    external
    view
    returns (
        bytes1 fields,
        string memory name,
        string memory version,
        uint256 chainId,
        address verifyingContract,
        bytes32 salt,
        uint256[] memory extensions
    );
```

## Events
### EIP712DomainChanged
MAY be emitted to signal that the domain could have changed.


```solidity
event EIP712DomainChanged();
```

