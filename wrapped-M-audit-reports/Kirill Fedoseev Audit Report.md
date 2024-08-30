# M^0 Wrapped M Token Security Review

Date: **09.08.24**

Produced by **Kirill Fedoseev** (telegram: [kfedoseev](http://t.me/kfedoseev),
twitter: [@k1rill_fedoseev](http://twitter.com/k1rill_fedoseev))

## Introduction

An independent security review of the M^0 Wrapped M token contract was conducted by **kfedoseev** from 04.07.24 to
12.07.24. The fixes review was conducted intermittently from 16.07.24 to 09.08.24. The following methods were used for
conducting a security review:

- Manual source code review

## Disclaimer

No security review can guarantee or verify the absence of vulnerabilities. This security review is a time-bound process
where I tried to identify as many potential issues and vulnerabilities as possible, using my personal expertise in the
smart contract development and review.

## About M^0 Wrapped M Token

Wrapped M Token is a non-rebasing, non yield-bearing ERC20 token wrapper. Instead of continuously rebasing yield,
whitelisted earners are able to claim at discrete intervals or redirect all of their yield to a different
address.

## Observations and Limitations

* Wrapped M Token contract is upgradable via the TTG governance. Few important upgradability concerns are highlighted
  in **[L-02]**. Registrar key-value pair controlling the upgrade process can be directly altered through
  **StandardGovernor** or **EmergencyGovernor**, or indirectly thorough the **ZeroGovernor**. Upgradability is
  controlled by the implementation contract and can be forfeited in the future as part of one of the upgrades.
* Yield redirection rules are exclusively controlled by the TTG governance. TTG governance is expected to avoid creation
  of long yield redirection chains and loops, as such may completely break transfers to addresses involved in such
  chains.

## Severity classification

| **Severity**           | **Impact: High** | **Impact: Medium** | **Impact: Low** |
|------------------------|------------------|--------------------|-----------------|
| **Likelihood: High**   | Critical         | High               | Medium          |
| **Likelihood: Medium** | High             | Medium             | Low             |
| **Likelihood: Low**    | Medium           | Low                | Low             |

**Impact** - the economic, technical, reputation or other damage to the protocol implied from a successful exploit.

**Likelihood** - the probability that a particular finding or vulnerability gets exploited.

**Severity** - the overall criticality of the particular finding.

## Scope summary

Reviewed commits:

* [85b8959aac0e5e268a92946ba7933df3c597818f](https://github.com/m0-foundation/wrapped-m-token/commit/85b8959aac0e5e268a92946ba7933df3c597818f)

Reviewed fixes commits:

* [88c54bb06728e58d9e061997297876687dd9fa55](https://github.com/m0-foundation/wrapped-m-token/commit/88c54bb06728e58d9e061997297876687dd9fa55)

Reviewed contracts:

- `src/interfaces/IMigratable.sol`
- `src/interfaces/IMTokenLike.sol`
- `src/interfaces/IRegistrarLike.sol`
- `src/interfaces/IWrappedMToken.sol`
- `src/libs/IndexingMath.sol`
- `src/Migratable.sol`
- `src/Proxy.sol`
- `src/WrappedMToken.sol`

---

# Findings Summary

| ID     | Title                                                                                   | Severity      | Status       |
|--------|-----------------------------------------------------------------------------------------|---------------|--------------|
| [H-01] | Unrestricted access to `stopEarningM`                                                   | High          | Fixed        |
| [H-02] | Incorrect bit math used in `_updateIndex`                                               | High          | Fixed        |
| [H-03] | Unchecked underflow in `_claim`                                                         | High          | Fixed        |
| [M-01] | Contract may still account for an already stopped yield                                 | Medium        | Acknowledged | 
| [M-02] | Missing `Transfer` event in `_claim`                                                    | Medium        | Fixed        |
| [L-01] | No status check for `delegatecall` in `Migratable`                                      | Low           | Fixed        |
| [L-02] | No builtin replay protection for migrations in `Migratable`                             | Low           | Acknowledged |
| [I-01] | Gas-optimize `index_` calculation in `_getBalanceInfo`                                  | Informational | Fixed        |
| [I-02] | Gas-optimize `bytes32` constants by using `uint256` instead                             | Informational | Fixed        |
| [I-03] | Restrict transfers to the token contract                                                | Informational | Acknowledged |
| [I-04] | Gas-optimize balance manipulation functions                                             | Informational | Acknowledged |
| [I-05] | Unchecked overflow in `divide240By128Down`, `divide240by112Down` and `divide240By128Up` | Informational | Fixed        |
| [I-06] | Redundant `safe240` checks in `multiply112By128Down` and `multiply112By128Up`           | Informational | Fixed        |
| [I-07] | Unused functions                                                                        | Informational | Fixed        |
| [I-08] | Inefficient implementation of `transfer` between active earners                         | Informational | Fixed        |

# Security & Economic Findings

## [H-01] Unrestricted access to `stopEarningM`

Function `stopEarningM` disables yield earning system-wide for all Wrapped M holders. Function is permissionless, thus
should only be callable if the TTG governance removed Wrapped M contract from the earners whitelist.

### Recommendation

Use a different variation of `stopEarning` function, which additionally checks if the caller is removed from the earners
whitelist:

```diff
function stopEarningM() external onlyWhenEarning {
    mIndexWhenEarningStopped = currentIndex();

-   IMTokenLike(mToken).stopEarning();
+   IMTokenLike(mToken).stopEarning(address(this));
}
```

## [H-02] Incorrect bit math used in `_updateIndex`

Wrapped M contract stores user balances in bit-packed struct. For earners, the struct contains 4 parts encoded in a
single 32-byte slot:

1. 1 byte (uint8) - `isEarning` flag, `true` for all earners.
2. 1 byte (uint8) - currently zero, reserved.
3. 16 bytes (uint128) - last synced principal index.
4. 14 bytes (uint112) - last synced principal.

Function `_updateIndex` uses incorrect offsets when operating on the index field.

### Recommendation

Update the `_updateIndex` function as follows:

```diff
-unwrapped_ &= ~(uint256(type(uint112).max) << 128);
+unwrapped_ &= ~(uint256(type(uint128).max) << 112);
```

## [H-03] Unchecked underflow in `_claim`

Function `_claim` updates current user balance using `_setBalanceInfo` based on the change in `currentIndex()`.
Principal is not supposed to change as part of this operation, however due to the current rounding implementation it may
actually decrease. If the principal decrease is not compensated enough by the increase in updated `currentIndex()`, then
`endingBalance_` may end up being less than the `startingBalance_`. This, in turn, will lead to an underflow inside the
`unchecked` block in the following piece of code, which may eventually lead to the broken values being saved in the
contract storage and used in emitted events:

```solidity
function _claim(address account_, uint128 currentIndex_) internal returns (uint240 yield_) {
    (bool isEarner_, uint128 index_, uint112 principal_, uint240 startingBalance_) = _getBalanceInfo(account_);

    // ...

    _setBalanceInfo(
        account_,
        true,
        currentIndex_,
        IndexingMath.getPresentAmountRoundedDown(principal_, currentIndex_)
    );

    // ...
    (, , , uint240 endingBalance_) = _getBalanceInfo(account_);

    unchecked {
        yield_ = endingBalance_ - startingBalance_;
        // ...
```

### Recommendation

Don't update principal value as part of the `claim_` function, update only `index` values instead.

## [M-01] Contract may still account for an already stopped yield

M token contract allows anyone to stop earner's yield by calling a `stopEarning(address)`, whenever earner address is
removed by the TTG from the earners whitelist.

If the Wrapped M contract is ever removed from the earners whitelist, and the respective `stopEarning(address)` on the M
token contract directly, Wrapped M token will immediately stop earning yield. However, Wrapped M holders will continue
to earn yield based on internal Wrapped M accounting logic using continuously increasing `currentIndex()`,
until `stopEarningM()` is called on the Wrapped M contract.

This situation may lead to an insolvency with remained Wrapped M holders, as withdrawals are being fulfilled in the FCFS
order.

### Recommendation

Use a different "index" accounting method based on the actual M balance difference (i.e.
track `M.balanceOf(address(this))` instead of `M.currentIndex()`).

Alternative solution is to introduce a small buffer (e.g. 0.1% or ~1 week of interest) in `excess()` calculation. Such
buffer will absorb any interest differences for a time being, until `stopEarningM()` is properly called.

## [M-02] Missing `Transfer` event in `_claim`

One of the branches in `_claim` function of `WrappedMToken` responsible for handling overridden yield recipients, does
not emit a necessary mint-like `Transfer` event. Missing emit of `Transfer` might break external accounting tools and
lead to incorrect balance being displayed in various UIs.

### Recommendation

Add missing emit as follows:

```diff
if (claimOverrideRecipient_ == address(0)) {
    emit Claimed(account_, account_, yield_);
    emit Transfer(address(0), account_, yield_);
} else {
    emit Claimed(account_, claimOverrideRecipient_, yield_);
+   emit Transfer(address(0), account_, yield_);

    // NOTE: Watch out for a long chain of earning claim override recipients.
    _transfer(account_, claimOverrideRecipient_, yield_, currentIndex_);
}
```

## [L-01] No status check for `delegatecall` in `Migratable`

Call to migrator contract using `delegatecall` in `_migrate` can silently fail on revert or out-of-gas error, as it's
status is not being validated.

### Recommendation

Revert call to `_migrate`, if underlying `delegatecall` failed for any reason, as suggested by the compiler:

```diff
-migrator_.delegatecall("");
+(bool status, ) = migrator_.delegatecall("");
+require(status);
```

## [L-02] No builtin replay protection for migrations in `Migratable`

Function `migrate()` in `Migratable` is not protected against replayed migrations, as the same migration can be applied
repeatedly until the TTG unsets the corresponding registrar value with the migrator address. This may lead to undesired
duplicated `Migrated` and `Upgraded` events triggering some external monitoring tools without reason, or problems with
non-idempotent migrations (i.e. migrations containing some non-trivial logic beyond implementation address update).

### Recommendation

Consider adopting one or multiple of the following solutions:

1. Explicitly require implementation address to change during the migration process, so
   that `newImplementation_ != oldImplementation_`. This, however, may break migrators that are not designed to change
   the implementation address.
2. Record a bool `used` flag for each utilized migrator contract, so that no contract approved by TTG may be used more
   than once.
3. Document a formal requirement for a migrator contract to include necessary replay-protection logic inside its own
   code. (e.g. check and match return values of `implementation()` or other public getters inside the migrator
   contract, or require to change the migrator prefix constant version in each subsequent implementation).

# Informational & Gas Optimizations

## [I-01] Gas-optimize `index_` calculation in `_getBalanceInfo`

Consider a more gas-optimal and simple way for extracting index from the tightly-packed `BalanceInfo` struct.

```diff
-index_ = uint128((unwrapped_ << 8) >> 120);
+index_ = uint128(unwrapped_ >> 112);
```

## [I-02] Gas-optimize `bytes32` constants by using `uint256` instead

Contract `Proxy` and `Migratable` use `bytes32` constants for storing respective ERC1967 slot values. Solidity does not
allow using `bytes32` values inside assembly blocks, which leads to local variables and stack operation consuming extra
gas. However, if `uint256` is used instead of `bytes32`, no such restrictions apply.

Consider doing the following refactor in `Proxy` contract (and similar in `Migratable`):

```diff
    //...
-   bytes32 private constant _IMPLEMENTATION_SLOT =
-       bytes32(0x360894a13ba1a3210667c828492db98dca3e2076cc3735a920a3ca505d382bbc);
+   uint256 private constant _IMPLEMENTATION_SLOT =
+       0x360894a13ba1a3210667c828492db98dca3e2076cc3735a920a3ca505d382bbc;

    constructor(address implementation_) {
        if (implementation_ == address(0)) revert();

-       bytes32 slot_ = _IMPLEMENTATION_SLOT;
-
        assembly {
-           sstore(slot_, implementation_)
+           sstore(_IMPLEMENTATION_SLOT, implementation_)
        }
    }

    fallback() external payable virtual {
-       bytes32 slot_ = _IMPLEMENTATION_SLOT;
-       bytes32 implementation_;
-       
        assembly {
-           implementation_ := sload(slot_)
+           let implementation_ := sload(_IMPLEMENTATION_SLOT)
            // ...
```

## [I-03] Restrict transfers to the token contract

Transfers of ERC20 tokens to the address of the token contract itself is a common pitfall in the EVM world. Some tokens
intentionally restrict such possibility. In case of Wrapped M, it also creates a wierd edge-case, where Wrapped M
accounts for its own yield first on the whole M balance of the contract, and then on the balance of Wrapped M of itself.

There was no evidence found that this leads to any accounting problems, however, it may be worth restricting sending
Wrapped M tokens to the address of the Wrapped M contract to avoid it altogether (e.g. by adding and extra check
to `_revertIfInvalidRecipient`).

## [I-04] Gas-optimize balance manipulation functions

There are 4 different functions for managing user balance changes in the
codebase: `_addNonEarningAmount`, `_subtractNonEarningAmount`, `_addEarningAmount`, `_subtractEarningAmount`.

These function are being used in the same pattern more than once, and it seems they may be refactored in a shorter and
more gas-optimal way. For example, consider implementing the following functions instead of the above 4:

```solidity
function _addAmount(address account_, uint240 amount_) internal {
    (bool isEarning_, , , uint240 balance_) = _getBalanceInfo(account_);
    
    unchecked {
        if (isEarning_) {
            uint128 currentIndex_ = currentIndex();
            _claim(account_, currentIndex_);
            (, , , balance_) = _getBalanceInfo(account_);
            _setBalanceInfo(account_, true, currentIndex_, balance_ + amount_);
            _addTotalEarningSupply(amount_, currentIndex_);
        } else {
            _setBalanceInfo(account_, false, 0, balance_ + amount_);
            totalNonEarningSupply += amount_;
        }
    }
}

function _subtractAmount(address account_, uint240 amount_) internal {
    (bool isEarning_, , , uint240 balance_) = _getBalanceInfo(account_);

    unchecked {
        if (isEarning_) {
            uint128 currentIndex_ = currentIndex();
            _claim(account_, currentIndex_);
            (, , , balance_) = _getBalanceInfo(account_);

            if (balance_ < amount_) revert InsufficientBalance(account_, balance_, amount_);

            _setBalanceInfo(account_, true, currentIndex_, balance_ - amount_);
            _subtractTotalEarningSupply(amount_, currentIndex_);
        } else {
            if (balance_ < amount_) revert InsufficientBalance(account_, balance_, amount_);

            _setBalanceInfo(account_, false, 0, balance_ - amount_);
            totalNonEarningSupply -= amount_;
        }
    }
}
```

## [I-05] Unchecked overflow in `divide240By128Down`, `divide240by112Down` and `divide240By128Up`

Function `divide240By128Down`, `divide240by112Down` and `divide240By128Up` could technically return incorrect results
due to unchecked multiplication overflow.

Due to how they are currently being used, it's not supposed to happen. However, to avoid errors in future code depending
on the same library, consider adding a comment similar to the one in the original M Token:

```solidity
// NOTE: While `uint256(x) * EXP_SCALED_ONE` can technically overflow, these divide/multiply functions are
//       only used for the purpose of principal/present amount calculations for continuous indexing, and
//       so for an `x` to be large enough to overflow this, it would have to be a possible result of
//       `multiplyDown` or `multiplyUp`, which would already satisfy
//       `uint256(x) * EXP_SCALED_ONE < type(uint240).max`.
```

## [I-06] Redundant `safe240` checks in `multiply112By128Down` and `multiply112By128Up`

Functions `multiply112By128Down` and `multiply112By128Up` multiply `uint112` by `uint128` value, which can't lead to
a `uint240` overflow. Therefore `UIntMath.safe240` cast is unnecessary there and can be removed.

## [I-07] Unused functions

Functions `getPrincipalAmountRoundedUp` and `divide240By128Up` are unused and therefore can be safely removed.

## [I-08] Inefficient implementation of `transfer` between active earners

Whenever transfer is performed between two active earners, both addresses are first updated using up-to-date index
information. This allows to perform a transfer directly in principal amounts to avoid multiple truncation errors along
the way. However, current implementation performs multiple conversions between principal and present amounts:

1. First we convert sender's stored principal balance to present amount.
2. Then we subtract transfer amount and convert sender's present amount back to the principal amount.
3. Then we convert receiver's stored principal balance to present amount.
4. Then we add transfer amount and convert receiver's present amount back to the principal amount.

Each step involves a small truncation error, while all of them can be avoided if transfer is performed in principal
amount directly.

For instance, take a look at the following test involving a self-transfer:

```solidity
function test_transferToSelf() external {
   _wrappedMToken.setPrincipalOfTotalEarningSupply(909);
   _wrappedMToken.setIndexOfTotalEarningSupply(_currentIndex);

   _wrappedMToken.setAccountOf(_alice, true, _currentIndex, 1_000);

   _mToken.setCurrentIndex(_currentIndex * 5 / 3); // 1833333447838

   _wrappedMToken.claimFor(_alice);

   assertEq(_wrappedMToken.balanceOf(_alice), 1666);
   vm.prank(_alice);
   _wrappedMToken.transfer(_alice, 500);
   assertEq(_wrappedMToken.balanceOf(_alice), 1662); // loss of 4 wei can be avoided, if we transfer 273 principal wei directly
}
```
