# ContractHelper
[Git Source](https://github.com/MZero-Labs/common/blob/9da96e78d24aadd41ee6f776b7b028203782b632/src/ContractHelper.sol)

**Author:**
M^0 Labs

*See the following sources for very similar implementations:
- https://github.com/foundry-rs/forge-std/blob/914702ae99c92fcc41db5128ae57d24a11be4a39/src/Script.sol
- https://github.com/foundry-rs/forge-std/blob/578968243529db44acffcb802196ccab9b54db88/src/StdUtils.sol#L90
- https://github.com/SoulWallet/soul-wallet-contract/blob/develop/script/DeployHelper.sol#L133
- https://github.com/nomoixyz/vulcan/blob/f67740f8a9c846a543aebf29433ad69c3f0ff337/src/_internal/Accounts.sol#L118
- https://github.com/chainlight-io/publications/blob/887d6fe1a4f53573de6b89dbecba0c91b091dba2/ctf-writeups/paradigm2023/dropper/Solve.s.sol#L29
- https://github.com/HerodotusDev/herodotus-evm/blob/a0e9c8be1a17838633d3dcdd54b72682f7654abd/src/lib/CREATE.sol#L5
- https://github.com/Polymarket/ctf-exchange/blob/2745c3017400dbc1925711005fe76b018b999155/src/dev/util/Predictor.sol#L9
- https://github.com/delegatexyz/delegate-market/blob/2418182fe81491114370287412926b57c1ddbd94/script/ComputeAddress.s.sol#L5
Note that this implementation, as do many others, assumes an account does not have a nonce greater than 0xffffffff.
If this is not the case, the address of the contract deployed by the account with the given nonce will be incorrect.*


## Functions
### getContractFrom

Returns the expected address of a contract deployed by `account_` with transaction count `nonce_`.


```solidity
function getContractFrom(address account_, uint256 nonce_) internal pure returns (address contract_);
```
**Parameters**

|Name|Type|Description|
|----|----|-----------|
|`account_`|`address`| The address of the account deploying a contract.|
|`nonce_`|`uint256`|   The nonce used in the deployment transaction.|

**Returns**

|Name|Type|Description|
|----|----|-----------|
|`contract_`|`address`|The expected address of the deployed contract.|


