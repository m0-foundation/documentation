# TTGRegistrarReader
[Git Source](https://github.com/MZero-Labs/protocol/blob/3382fb7336bbc7276e0c3f51da451c9fa6e0016f/src/libs/TTGRegistrarReader.sol)

**Author:**
M^0 Labs


## State Variables
### EARNER_RATE_MODEL
The name of parameter in TTG that defines the earner rate model contract.


```solidity
bytes32 internal constant EARNER_RATE_MODEL = "earner_rate_model";
```


### EARNERS_LIST
The earners list name in TTG.


```solidity
bytes32 internal constant EARNERS_LIST = "earners";
```


### EARNERS_LIST_IGNORED
The ignore earners list flag name in TTG.


```solidity
bytes32 internal constant EARNERS_LIST_IGNORED = "earners_list_ignored";
```


### MINT_DELAY
The name of parameter in TTG that defines the time to wait for mint request to be processed


```solidity
bytes32 internal constant MINT_DELAY = "mint_delay";
```


### MINT_RATIO
The name of parameter in TTG that defines the mint ratio.


```solidity
bytes32 internal constant MINT_RATIO = "mint_ratio";
```


### MINT_TTL
The name of parameter in TTG that defines the time while mint request can still be processed


```solidity
bytes32 internal constant MINT_TTL = "mint_ttl";
```


### MINTER_FREEZE_TIME
The name of parameter in TTG that defines the time to freeze minter


```solidity
bytes32 internal constant MINTER_FREEZE_TIME = "minter_freeze_time";
```


### MINTER_RATE_MODEL
The name of parameter in TTG that defines the minter rate model contract.


```solidity
bytes32 internal constant MINTER_RATE_MODEL = "minter_rate_model";
```


### MINTERS_LIST
The minters list name in TTG.


```solidity
bytes32 internal constant MINTERS_LIST = "minters";
```


### PENALTY_RATE
The name of parameter in TTG that defines the penalty rate.


```solidity
bytes32 internal constant PENALTY_RATE = "penalty_rate";
```


### UPDATE_COLLATERAL_INTERVAL
The name of parameter in TTG that required interval to update collateral.


```solidity
bytes32 internal constant UPDATE_COLLATERAL_INTERVAL = "update_collateral_interval";
```


### UPDATE_COLLATERAL_VALIDATOR_THRESHOLD
The name of parameter that defines number of signatures required for a successful collateral update


```solidity
bytes32 internal constant UPDATE_COLLATERAL_VALIDATOR_THRESHOLD = "update_collateral_threshold";
```


### VALIDATORS_LIST
The validators list name in TTG.


```solidity
bytes32 internal constant VALIDATORS_LIST = "validators";
```


## Functions
### getEarnerRateModel

Gets the earner rate model contract address.


```solidity
function getEarnerRateModel(address registrar_) internal view returns (address);
```

### getMintDelay

Gets the mint delay.


```solidity
function getMintDelay(address registrar_) internal view returns (uint256);
```

### getMinterFreezeTime

Gets the minter freeze time.


```solidity
function getMinterFreezeTime(address registrar_) internal view returns (uint256);
```

### getMinterRateModel

Gets the minter rate model contract address.


```solidity
function getMinterRateModel(address registrar_) internal view returns (address);
```

### getMintTTL

Gets the mint TTL.


```solidity
function getMintTTL(address registrar_) internal view returns (uint256);
```

### getMintRatio

Gets the mint ratio.


```solidity
function getMintRatio(address registrar_) internal view returns (uint256);
```

### getUpdateCollateralInterval

Gets the update collateral interval.


```solidity
function getUpdateCollateralInterval(address registrar_) internal view returns (uint256);
```

### getUpdateCollateralValidatorThreshold

Gets the update collateral validator threshold.


```solidity
function getUpdateCollateralValidatorThreshold(address registrar_) internal view returns (uint256);
```

### isApprovedEarner

Checks if the given earner is approved.


```solidity
function isApprovedEarner(address registrar_, address earner_) internal view returns (bool);
```

### isEarnersListIgnored

Checks if the `earners_list_ignored` exists.


```solidity
function isEarnersListIgnored(address registrar_) internal view returns (bool);
```

### isApprovedMinter

Checks if the given minter is approved.


```solidity
function isApprovedMinter(address registrar_, address minter_) internal view returns (bool);
```

### isApprovedValidator

Checks if the given validator is approved.


```solidity
function isApprovedValidator(address registrar_, address validator_) internal view returns (bool);
```

### getPenaltyRate

Gets the penalty rate.


```solidity
function getPenaltyRate(address registrar_) internal view returns (uint256);
```

### getVault

Gets the vault contract address.


```solidity
function getVault(address registrar_) internal view returns (address);
```

### toAddress

Converts given bytes32 to address.


```solidity
function toAddress(bytes32 input_) internal pure returns (address);
```

### _contains

Checks if the given list contains the given account.


```solidity
function _contains(address registrar_, bytes32 listName_, address account_) private view returns (bool);
```

### _get

Gets the value of the given key.


```solidity
function _get(address registrar_, bytes32 key_) private view returns (bytes32);
```

