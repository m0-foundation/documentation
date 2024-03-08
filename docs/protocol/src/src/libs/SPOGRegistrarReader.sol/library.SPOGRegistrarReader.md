# SPOGRegistrarReader
[Git Source](https://github.com/MZero-Labs/protocol/blob/45d6176ce6231b36efc0c52a2961774481e32ec1/src/libs/SPOGRegistrarReader.sol)


## State Variables
### BASE_EARNER_RATE
The name of parameter in SPOG that defines the base earner rate.


```solidity
bytes32 internal constant BASE_EARNER_RATE = "base_earner_rate";
```


### BASE_MINTER_RATE
The name of parameter in SPOG that defines the base minter rate.


```solidity
bytes32 internal constant BASE_MINTER_RATE = "base_minter_rate";
```


### EARNER_RATE_MODEL
The name of parameter in SPOG that defines the earner rate model contract.


```solidity
bytes32 internal constant EARNER_RATE_MODEL = "earner_rate_model";
```


### EARNERS_LIST
The earners list name in SPOG.


```solidity
bytes32 internal constant EARNERS_LIST = "earners";
```


### EARNERS_LIST_IGNORED
The earners list name in SPOG.


```solidity
bytes32 internal constant EARNERS_LIST_IGNORED = "earners_list_ignored";
```


### MINT_DELAY
The name of parameter in SPOG that defines the time to wait for mint request to be processed


```solidity
bytes32 internal constant MINT_DELAY = "mint_delay";
```


### MINT_RATIO
The name of parameter in SPOG that defines the mint ratio.


```solidity
bytes32 internal constant MINT_RATIO = "mint_ratio";
```


### MINT_TTL
The name of parameter in SPOG that defines the time while mint request can still be processed


```solidity
bytes32 internal constant MINT_TTL = "mint_ttl";
```


### MINTER_FREEZE_TIME
The name of parameter in SPOG that defines the time to freeze minter


```solidity
bytes32 internal constant MINTER_FREEZE_TIME = "minter_freeze_time";
```


### MINTER_RATE_MODEL
The name of parameter in SPOG that defines the minter rate model contract.


```solidity
bytes32 internal constant MINTER_RATE_MODEL = "minter_rate_model";
```


### MINTERS_LIST
The minters list name in SPOG.


```solidity
bytes32 internal constant MINTERS_LIST = "minters";
```


### MINTER_RATE
The name of parameter in SPOG that defines the minter rate.


```solidity
bytes32 internal constant MINTER_RATE = "minter_rate";
```


### PENALTY_RATE
The name of parameter in SPOG that defines the penalty rate.


```solidity
bytes32 internal constant PENALTY_RATE = "penalty_rate";
```


### UPDATE_COLLATERAL_INTERVAL
The name of parameter in SPOG that required interval to update collateral.


```solidity
bytes32 internal constant UPDATE_COLLATERAL_INTERVAL = "updateCollateral_interval";
```


### UPDATE_COLLATERAL_VALIDATOR_THRESHOLD
The name of parameter that defines number of signatures required for successful collateral update


```solidity
bytes32 internal constant UPDATE_COLLATERAL_VALIDATOR_THRESHOLD = "updateCollateral_threshold";
```


### VALIDATORS_LIST
The validators list name in SPOG.


```solidity
bytes32 internal constant VALIDATORS_LIST = "validators";
```


## Functions
### getBaseEarnerRate


```solidity
function getBaseEarnerRate(address registrar_) internal view returns (uint256 rate_);
```

### getBaseMinterRate


```solidity
function getBaseMinterRate(address registrar_) internal view returns (uint256 rate_);
```

### getEarnerRateModel


```solidity
function getEarnerRateModel(address registrar_) internal view returns (address rateModel_);
```

### getMintDelay


```solidity
function getMintDelay(address registrar_) internal view returns (uint256 queueTime_);
```

### getMinterFreezeTime


```solidity
function getMinterFreezeTime(address registrar_) internal view returns (uint256 freezeTime_);
```

### getMinterRate


```solidity
function getMinterRate(address registrar_) internal view returns (uint256 rate_);
```

### getMinterRateModel


```solidity
function getMinterRateModel(address registrar_) internal view returns (address rateModel_);
```

### getMintTTL


```solidity
function getMintTTL(address registrar_) internal view returns (uint256 timeToLive_);
```

### getMintRatio


```solidity
function getMintRatio(address registrar_) internal view returns (uint256 ratio_);
```

### getUpdateCollateralInterval


```solidity
function getUpdateCollateralInterval(address registrar_) internal view returns (uint256 interval_);
```

### getUpdateCollateralValidatorThreshold


```solidity
function getUpdateCollateralValidatorThreshold(address registrar_) internal view returns (uint256 quorum_);
```

### isApprovedEarner


```solidity
function isApprovedEarner(address registrar_, address earner_) internal view returns (bool isApproved_);
```

### isEarnersListIgnored


```solidity
function isEarnersListIgnored(address registrar_) internal view returns (bool isIgnored_);
```

### isApprovedMinter


```solidity
function isApprovedMinter(address registrar_, address minter_) internal view returns (bool isApproved_);
```

### isApprovedValidator


```solidity
function isApprovedValidator(address registrar_, address validator_) internal view returns (bool isApproved_);
```

### getPenaltyRate


```solidity
function getPenaltyRate(address registrar_) internal view returns (uint256 penalty_);
```

### getVault


```solidity
function getVault(address registrar_) internal view returns (address vault_);
```

### toAddress


```solidity
function toAddress(bytes32 input_) internal pure returns (address output_);
```

### toBytes32


```solidity
function toBytes32(address input_) internal pure returns (bytes32 output_);
```

### _contains


```solidity
function _contains(address registrar_, bytes32 listName_, address account_) private view returns (bool contains_);
```

### _get


```solidity
function _get(address registrar_, bytes32 key_) private view returns (bytes32 value_);
```

### _toAddress


```solidity
function _toAddress(bytes32 input_) private pure returns (address output_);
```

