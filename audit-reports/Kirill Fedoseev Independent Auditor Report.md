# M^0 Protocol Security Review

Date: **08.03.24**

Produced by **Kirill Fedoseev** (telegram: [kfedoseev](http://t.me/kfedoseev),
twitter: [@k1rill_fedoseev](http://twitter.com/k1rill_fedoseev))

## Introduction

An independent security review of the M^0 Protocol was conducted by **kfedoseev** from 19.02.24 to 23.02.24. The
fixes review was conducted from 26.02.24 to 08.03.24. The following methods were used for conducting a security review:

- Manual source code review
- Manual penetration testing
- Manual audit fixes review

## Disclaimer

No security review can guarantee or verify the absence of vulnerabilities. This security review is a time-bound process
where I tried to identify as many potential issues and vulnerabilities as possible, using my personal expertise in the
smart contract development and review.

## About M^0 Protocol

The core M^0 protocol is a coordination layer for permissioned actors to generate M. M is a fungible token that can
be generated by locking Eligible Collateral in a secure off-chain facility. The protocol enforces a common set of rules
and safety procedures for the management of M.

## Observations and Limitations

- M^0 Protocol security ultimately depends on the correctness of financial incentives established in the TTG
  governance module and active presence of at least one honest validator.
- M^0 TTG is an immutable dual-token governance model, with voting rights being issued algorithmically to
  participating members over time.
- M^0 TTG has a reset functionality, which redeploys all contracts related to accounting of voting rights.
  - Such extreme action effectively makes the old POWER token worthless.
  - Old POWER balances held in non-wallet (e.g. AMM / Lending pools) contracts are very likely being forfeited in the
    process.
  - Most recent old POWER token transfers may be left unaccounted in the new POWER deployment due to how epoch
    boundaries work.
- M^0 TTG standard governor participants are financially incentivized to create and pass at least 1 proposal per
  epoch, so that POWER and ZERO rewards are not forfeited for them. This will likely cause appearance of end-of-epoch
  liveliness no-op proposals in all empty voting epochs.

## Severity classification

| **Severity**           | **Impact: High** | **Impact: Medium** | **Impact: Low** |
| ---------------------- | ---------------- | ------------------ | --------------- |
| **Likelihood: High**   | Critical         | High               | Medium          |
| **Likelihood: Medium** | High             | Medium             | Low             |
| **Likelihood: Low**    | Medium           | Low                | Low             |

**Impact** - the economic, technical, reputation or other damage to the protocol implied from a successful exploit.

**Likelihood** - the probability that a particular finding or vulnerability gets exploited.

**Severity** - the overall criticality of the particular finding.

## Scope summary

Reviewed commits:

- Common -
  [0a0cae40c2c88625cb455fd41bb2a5740f85a7d3](https://github.com/MZero-Labs/common/tree/0a0cae40c2c88625cb455fd41bb2a5740f85a7d3)
- Protocol -
  [5e5a48776c8470edd12a58cd94feeef198d827df](https://github.com/MZero-Labs/protocol/tree/5e5a48776c8470edd12a58cd94feeef198d827df)
- TTG -
  [da995f377b1d84e6368c488abaabee10fcc3cfaa](https://github.com/MZero-Labs/ttg/tree/da995f377b1d84e6368c488abaabee10fcc3cfaa)

Reviewed fixes commits:

- Common -
  [2ba852c44e02e3bee58cafea3ce7964022bd4486](https://github.com/MZero-Labs/common/tree/2ba852c44e02e3bee58cafea3ce7964022bd4486)
- Protocol -
  [2e9f5cd32b292d3dea71ba1dfff0b2b68cab9467](https://github.com/MZero-Labs/protocol/tree/2e9f5cd32b292d3dea71ba1dfff0b2b68cab9467)
- TTG -
  [7581622f35d64820bac667580cb9690982298eb2](https://github.com/MZero-Labs/ttg/tree/7581622f35d64820bac667580cb9690982298eb2)

Reviewed contracts:

- `common/src/**`
- `protocol/src/**`
- `ttg/src/**`

---

# Findings Summary

| ID     | Title                                                                       | Severity      | Status       |
| ------ | --------------------------------------------------------------------------- | ------------- | ------------ |
| [H-01] | Validator signatures can be double counted                                  | High          | Fixed        |
| [M-01] | Missing `Approval` event in `permit` implementation                         | Medium        | Fixed        |
| [M-02] | Validator signatures allow for retrieval amounts to be manipulated          | Medium        | Acknowledged |
| [L-01] | Incorrect max cap for the mint ratio                                        | Low           | Fixed        |
| [L-02] | Possible overflow in `convertToBasisPoints`                                 | Low           | Fixed        |
| [L-03] | Incorrect bound for return value of `_getUnrealizedInflation`               | Low           | Fixed        |
| [L-04] | Function `_castVotes` return value is inconsistent in `ThresholdGovernor`   | Low           | Acknowledged |
| [I-01] | One of function `isValidECDSASignature` overloads is unused                 | Informational | Fixed        |
| [I-02] | Inconsistent error handling in `_revertIfInvalidSignature`                  | Informational | Fixed        |
| [I-03] | ERC20 metadata storage for `name()` and `symbol()` can be made immutable    | Informational | Acknowledged |
| [I-04] | Empty implementation of `balanceOf` in `ERC20Extended`                      | Informational | Fixed        |
| [I-05] | Typos, errors and duplicates in NatSpec comments                            | Informational | Fixed        |
| [I-06] | Redundant usage of `min40IgnoreZero`                                        | Informational | Fixed        |
| [I-07] | Lack of key rotation mechanism for validators and minters                   | Informational | Acknowledged |
| [I-08] | Redundant usage of `_getDefaultIfZero`                                      | Informational | Fixed        |
| [I-09] | Proposal in `ThresholdGovernance` can be executed twice                     | Informational | Acknowledged |
| [I-10] | Function `_castVote` for non-existent proposal reverts with different error | Informational | Fixed        |

Note: several low-severity and informational findings were identified but not included in the final report, as they were
considered as duplicates from the prior audit reports available for M^0 Protocol and team has already acknowledged or
accepted them earlier.

# Security & Economic Findings

## [H-01] Validator signatures can be double counted

Recent refactoring in `MinterGateway` introduced the vulnerability in the signature validation mechanism.
Function `_verifyValidatorSignatures` is supposed to check that enough signatures from the given array belong to the
correct set of distinct validators. Validators and signatures must be validated to go strictly in the increasing order,
however the order is not validated for validators not approved by the TTG, allowing for correct signatures to be double
counted.

See the following unit test in `MinterGateway.t.sol` for more details:

```solidity
function test_updateCollateral_invalidSignatureOrder() external {
    _ttgRegistrar.updateConfig(TTGRegistrarReader.UPDATE_COLLATERAL_VALIDATOR_THRESHOLD, 2);

    uint256 collateral = 100;
    uint256[] memory retrievalIds = new uint256[](0);
    uint256 timestamp = block.timestamp;

    bytes memory signature1_ = _getCollateralUpdateSignature(
        address(_minterGateway),
        _minter1,
        collateral,
        retrievalIds,
        bytes32(0),
        timestamp,
        _validator1Pk
    );

    address[] memory validators = new address[](3);
    validators[0] = _validator1;
    validators[1] = address(0xdead);
    validators[2] = _validator1;

    bytes[] memory signatures = new bytes[](3);
    signatures[0] = signature1_;
    signatures[1] = new bytes(0);
    signatures[2] = signature1_;

    uint256[] memory timestamps = new uint256[](3);
    timestamps[0] = timestamp;
    timestamps[1] = timestamp;
    timestamps[2] = timestamp;

    vm.expectRevert(IMinterGateway.InvalidSignatureOrder.selector);

    vm.prank(_minter1);
    _minterGateway.updateCollateral(collateral, retrievalIds, bytes32(0), validators, timestamps, signatures);
}
```

### Recommendation

Revert back the refactoring made in `_verifyValidatorSignatures` preventing the correct address order validation.

## [M-01] Missing `Approval` event in `permit` implementation

Implementation of `permit` contradicts `EIP-2612` as it does not emit the `Approval` event.

### Recommendation

Emit `Approval` event every time a successful permit is used to set an allowance.

## [M-02] Validator signatures allow for retrieval amounts to be manipulated

Validators are signing the digest for collateral updates calculated in `_getUpdateCollateralDigest`. The digest depends
on the retrieval ids but not on the retrievals themselves. There is also no any built-in delay between potential calls
to `proposeRetrieval` and `updateCollateral`, which makes the following manipulation possible:

1. Minter with 1,000 collateral submits a retrieval for 100 units. Retrieval is assigned id #1.
2. Minter request the collateral update attestation from the validators.
3. Validators quickly sign the digest off-chain and provide the minter with the signatures, attesting for a new
   collateral value of 900 and resolution of retrieval id #1.
4. Network re-orgs the transaction from minter with `proposeRetrieval` call due to a deep block re-org.
5. Minter quickly replaces their transaction with `proposeRetrieval` call with a new retrieval for 500.
6. Minter call `updateCollateral` with collateral value of 900 and resolution of retrieval id #1 for 500. Previously
   given validator signatures are accepted as the digest haven't changed along with the retrieval amount.
7. Updated minter state now records 900 remaining collateral, while 500 collateral is subject to redemption based on the
   observed `RetrievalCreated` and `RetrievalResolved` events.

### Recommendation

Include individual or total retrieval amounts in the signed digest to make such validator signature re-use not possible.

## [L-01] Incorrect max cap for the mint ratio

Value of `mintRatio()` set in the TTG is stored uncapped, while the actual value being used in the `MinterGateway` is
capped to prevent overflow when multiplying `uint240` by it.

The correct cap seems to be `65_000` in basis points, which is equal to `650%`. The `SIXTY_FIVE` constant incorrectly
sets it to `650_000` though.

### Recommendation

Update the `SIXTY_FIVE` constant definition:

```diff
-/// @dev 10,000% in basis points.
-uint32 public constant SIXTY_FIVE = 65 * uint32(ONE);
+/// @dev 650% in basis points.
+uint32 public constant SIXTY_FIVE = 65_000;
```

Update the NatSpec comment in `maxAllowedActiveOwedMOf` interface definition:

```diff
/**
 * @notice The max allowed active owed M of minter taking into account collateral amount and retrieval proposals.
 * @dev    This is the only present value that requires a `uint256` since it is the result of a multiplication
-*         between a `uint240` and a value that has a max of `1,000,000` (the mint ratio).
+*         between a `uint240` and a value that has a max of `65,000` (the mint ratio).
 */
function maxAllowedActiveOwedMOf(address minter) external view returns (uint256);
```

## [L-02] Possible overflow in `convertToBasisPoints`

Function `convertToBasisPoints` uses an unsafe `uint32` type conversion which may lead to a truncated result being used.
As the rest of the code correctly assumes that the return type of `convertToBasisPoints` is `uint40`, consider changing
the type used inside the function body.

### Recommendation

Change the type used inside the function `convertToBasisPoints` to `uint40`:

```diff
 function convertToBasisPoints(uint64 input) internal pure returns (uint40) {
     unchecked {
-        return uint32((uint256(input) * BPS_SCALED_ONE) / EXP_SCALED_ONE);
+        return uint40((uint256(input) * BPS_SCALED_ONE) / EXP_SCALED_ONE);
     }
 }
```

Alternatively, consider using the `uint32` return type alongside the following optimization in `getSafeEarnerRate`:

```diff
 uint256 expRate_ = (uint256(lnResult_) * ContinuousIndexingMath.SECONDS_PER_YEAR) / confidenceInterval_;

-if (expRate_ > type(uint64).max) return type(uint32).max;
+if (expRate_ > type(uint32).max * EXP_SCALED_ONE / BPS_SCALED_ONE) return type(uint32).max;

 // NOTE: Do not need to do `UIntMath.safe256` because it is known that `lnResult_` will not be negative.
-uint40 safeRate_ = ContinuousIndexingMath.convertToBasisPoints(uint64(expRate_));
+return ContinuousIndexingMath.convertToBasisPoints(uint64(expRate_));

-return (safeRate_ > type(uint32).max) ? type(uint32).max : uint32(safeRate_);
```

## [L-03] Incorrect bound for return value of `_getUnrealizedInflation`

Function `_getUnrealizedInflation` upper bounds its return value at `type(uint240).max` two times within the unchecked
block:

```solidity
unchecked {
    uint256 inflatedBalance_ = uint256(balance_) + inflation_;

    // Cap inflation to `type(uint240).max`.
    if (inflatedBalance_ >= type(uint240).max) return type(uint240).max;

    uint256 newInflation_ = uint256(inflation_) + _getInflation(uint240(inflatedBalance_));

    // Cap inflation to `type(uint240).max`.
    if (newInflation_ >= type(uint240).max) return type(uint240).max;

    inflation_ = uint240(newInflation_); // Accumulate compounded inflation.
}
```

The first bound is incorrect since a relatively small value of `inflation_` that leads to the `uint240` overflow
in `inflatedBalance_` can lead to the returned inflation value of `type(uint240).max`.

The second bound is incorrect, since it may lead to the `uint240` overflow whenever inflation is added to the balance in
parent functions.

Returned `inflation_` is then added to the account balance using `_addUnchecked` in `_sync` function and may lead to
undesired overflow errors.

### Recommendation

Instead of bounding the `inflation_` at `type(uint240).max`, consider bounding it at `type(uint240).max - balance_` so
that the new balance value can't overflow.

## [L-04] Function `_castVotes` return value is inconsistent in `ThresholdGovernor`

Functions from `IBatchGovernor` for casting multiple votes at once are supposed to return amount of cast votes.
Natspec suggests that this amount is the same for all proposals. In `ThresholdGovernor`, however, this may not be the
case if executed proposals were started during two different consecutive epochs. In such case, the return value is
ambiguous.

### Recommendation

Remove return values from functions `_castVotes`, `castVotes` and `castVotesBySig`.

## Informational & Gas Optimizations

## [I-01] One of function `isValidECDSASignature` overloads is unused

Function `isValidECDSASignature(address signer, bytes32 digest, uint8 v, bytes32 r, bytes32 s)` overload is not used in
the rest of the codebase, except unit tests. Therefore, it can be safely removed.

## [I-02] Inconsistent error handling in `_revertIfInvalidSignature`

Implementation of `EIP712` has 3 function overloads for handling error in invalid signatures:

```solidity
function _revertIfInvalidSignature(address signer_, bytes32 digest_, bytes memory signature_) internal view {
    if (!SignatureChecker.isValidSignature(signer_, digest_, signature_)) revert InvalidSignature();
}

function _revertIfInvalidSignature(address signer_, bytes32 digest_, bytes32 r_, bytes32 vs_) internal pure {
    _revertIfError(SignatureChecker.validateECDSASignature(signer_, digest_, r_, vs_));
}

function _revertIfInvalidSignature(address signer_, bytes32 digest_, uint8 v_, bytes32 r_, bytes32 s_) internal pure {
    _revertIfError(SignatureChecker.validateECDSASignature(signer_, digest_, v_, r_, s_));
}
```

The first function overload reverts only with the `InvalidSignature` error, despite a more specific error may be
identified in the underlying functions. This behaviour is also inconsistent with remaining `_revertIfInvalidSignature`
overloads, which throw an exact reason the signature was deemed invalid for.

## [I-03] ERC20 metadata storage for `name()` and `symbol()` can be made immutable

Although solidity does not directly allow immutable values of dynamic types (e.g. `string`), these can be still made
immutable if stored as `bytes32` instead.
See https://github.com/compound-finance/comet/blob/22cf923b6263177555272dde8b0791703895517d/contracts/CometExt.sol as an
example implementation of such approach.

Consider implementing a similar optimization, if gas usage of `name()` and `symbol()` accessors and contract deployment
is worth the increase in code complexity.

## [I-04] Empty implementation of `balanceOf` in `ERC20Extended`

Contract `ERC20Extended` contains the following implementation of `balanceOf`:

```solidity
/// @inheritdoc IERC20
function balanceOf(address account_) external view virtual returns (uint256) {}
```

It's not recommended to leave such empty implementations in the abstract contracts, as they can lead to incorrect
behaviour in downstream contracts, if not properly overridden.

Consider to keep implementation missing, similar to how it's done for `totalSupply`:

```solidity
/// @inheritdoc IERC20
function totalSupply() external view virtual returns (uint256);
```

## [I-05] Typos, errors and duplicates in NatSpec comments

In the `IMinterGateway.sol`:

```diff
-/// @notice The timestamp after which an additional penalty for a missed update interval will bee charged.
+/// @notice The timestamp after which an additional penalty for a missed update interval will be charged.
 function collateralPenaltyDeadlineOf(address minter) external view returns (uint40);
```

In the `IMinterRateModel.sol`:

```diff
-/// @notice The base rate of the Earner Rate Model.
+/// @notice The base rate of the Minter Rate Model.
 function baseRate() external view returns (uint256);
```

In the `MinterGateway.sol`:

```diff
 /**
  * @notice Deactivates an active minter.
- * @dev    MUST revert if the minter is not an approved minter.
+ * @dev    MUST revert if the minter is still approved.
  * @dev    MUST revert if the minter is not active.
  * @param  minter        The address of the minter to deactivate.
  * @return inactiveOwedM The inactive owed M for the deactivated minter.
  */
 function deactivateMinter(address minter) external returns (uint240 inactiveOwedM);
```

In the `IEpochBasedVoteToken.sol`, `error AmountExceedsUint240` is unused:

```diff
-/// @notice Revert message when an number being casted to a uint240 exceeds the maximum uint240 value.
-error AmountExceedsUint240();
```

In the `IStandardGovernor.sol`:

```diff
 /**
  * @notice Sends the proposal fee for proposal `proposalId` to the vault, if it is Defeated or Expired.
- * @param  proposalId The minimum amount of tokens the caller is interested in buying.
+ * @param  proposalId The unique identifier of the proposal.
  */
 function sendProposalFeeToVault(uint256 proposalId) external;
```

In the `IRegistrar.sol` and `Registrar.sol`:

```diff
-/// @title A book of record of SPOG-specific contracts and arbitrary key-value pairs and lists.
+/// @title A book of record of TTG-specific contracts and arbitrary key-value pairs and lists.
```

In the `EpochBasedInflationaryVoteToken.sol`:

```diff
 /**
- * @dev    Returns the balance of `account_` plus any inflation that in unrealized before `epoch_`.
+ * @dev    Returns the balance of `account_` plus any inflation that is unrealized before `epoch_`.
  * @param  account_ The account to get the balance for.
  * @param  epoch_   The epoch to get the balance at.
- * @return The balance of `account_` plus any inflation that in unrealized before `epoch_`.
+ * @return The balance of `account_` plus any inflation that is unrealized before `epoch_`.
  */
 function _getBalance(address account_, uint16 epoch_) internal view virtual override returns (uint240) {
```

In the `IPowerToken.sol`, `error DivideUpOverflow()` is redundant, since `z < x` can't be without unchecked prior
computation:

```diff
 function _divideUp(uint256 x, uint256 y) internal pure returns (uint256 z) {
     if (y == 0) revert DivisionByZero();

     z = (x * ONE) + y;

-    if (z < x) revert DivideUpOverflow();

     unchecked {
         z = (z - 1) / y;
     }
 }
```

## [I-06] Redundant usage of `min40IgnoreZero`

The only place in the code where `min40IgnoreZero` is used is `_verifyValidatorSignatures`. However, as timestamps are
no longer allowed to be zero (due to `ZeroTimestamp` error check), `min40IgnoreZero` can be replaced with
simpler `min40`. As timestamps are also pre-validated against `uint40(block.timestamp)` value, safe cast is also
redundant. Finally, the `min40IgnoreZero` implementation itself can be pruned from the `UintMath` library as no longer
used in the codebase.

```diff
-minTimestamp_ = UIntMath.min40IgnoreZero(minTimestamp_, UIntMath.safe40(timestamps_[index_]));
+minTimestamp_ = UIntMath.min40(minTimestamp_, uint40(timestamps_[index_]));
```

## [I-07] Lack of key rotation mechanism for validators and minters

TTG registrar manages the list of whitelisted validators and minters. TTG registrar in its turn is controlled by a set
of governance contracts implementing different token voting schemes. Despite being a good option from the security
standpoint, this design lacks a speed of action in the event of key compromise of some validators or minters.

Although this can be managed on the implementation side of a specific validator/minter through various on-chain proxy
structures, a good addition to the security of the protocol may be a set of function allowing entities themselves to
rotate/forfeit their addresses and private keys. These emergency function may allow to act much faster compared to the
regular governance process in the event of potential key compromise.

## [I-08] Redundant usage of `_getDefaultIfZero`

As `AccountSnap` structs in `_delegatees` list can no longer contain `address(0)` value in the actual storage, the
following usages of `_getDefaultIfZero` can be simplified in `EpochBasedVoteToken.sol`:

```diff
// in function _setDelegatee

-// `oldDelegatee_` will be `delegator_` (the default) if it was retrieved as `address(0)`.
-oldDelegatee_ = _getDefaultIfZero(latestDelegateeSnap_.account, delegator_);
+oldDelegatee_ = latestDelegateeSnap_.account;

// in function _getDelegatee

 // Keep going back until we find the first snap with a startingEpoch less than or equal to `epoch_`. This snap
-// has the account applicable to `epoch_`. If we exhaust the array, then the delegatee is address(0).
+// has the account applicable to `epoch_`. If we exhaust the array, then the delegatee is the `account_` itself.
 while (index_ > 0) {
     AccountSnap storage accountSnap_ = _unsafeAccess(delegateeSnaps_, --index_);

-    if (accountSnap_.startingEpoch <= epoch_) return _getDefaultIfZero(accountSnap_.account, account_);
+    if (accountSnap_.startingEpoch <= epoch_) return accountSnap_.account;
 }
```

## [I-09] Proposal in `ThresholdGovernance` can be executed twice

In `ThresholdGovernance`, same proposal can be executed twice during 2 consecutive epochs, if two proposals with
identical calldata are submitted during epochs `N` and `N + 1`, and then both reach the voting quorum during
epoch `N + 1`. In such case, `execute` can be called twice with the same calldata.

No negative impact of such behaviour was identified. However, extra attention may be required if any on-chain contract
integrations for proposals executions will be developed.

## [I-10] Function `_castVote` for non-existent proposal reverts with different error

Whenever function `_castVote` is called for non-existent proposals, one may expect it to revert
with `ProposalDoesNotExist` error or similar. However, in reality it will underflow
in `_proposals[proposalId_].voteStart - 1` within the unchecked block and then revert with `NotPastTimepoint` error
while trying to call `getPastVotes` using `65535` as a timepoint.

Consider reverting with the correct `ProposalDoesNotExist` error instead.