# StatefulERC712
[Git Source](https://github.com/MZero-Labs/common/blob/9da96e78d24aadd41ee6f776b7b028203782b632/src/StatefulERC712.sol)

**Inherits:**
[IStatefulERC712](/src/interfaces/IStatefulERC712.sol/interface.IStatefulERC712.md), [ERC712Extended](/src/ERC712Extended.sol/abstract.ERC712Extended.md)

**Author:**
M^0 Labs

*An abstract implementation to satisfy stateful EIP-712 with nonces.*


## State Variables
### nonces
Returns the next nonce to be used in a signature by `account`.


```solidity
mapping(address account => uint256 nonce) public nonces;
```


## Functions
### constructor

Construct the StatefulERC712 contract.


```solidity
constructor(string memory name_) ERC712Extended(name_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`name_`|`string`|The name of the contract.|


