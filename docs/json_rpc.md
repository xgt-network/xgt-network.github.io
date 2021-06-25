# XGT JSON RPC API documents

#### Table of contents
  * [Block API](#block_api)
  * [Chain API](#chain-api)
  * [Contract API](#contract-api)
  * [Database API](#database-api)
  * [Transaction API](#transaction-api)
  * [Wallet by Key API](#wallet-by-key-api)
  * [Wallet History API](#wallet-history-api)
### Transaction
The structural properties of an unsigned transaction.
#### Fields
* UInt16 `ref_block_num` - _Last two bytes of a block in the merkel tree, used to prevent replay attacks_
* UInt32 `ref_block_prefix` - _Four bytes of the block ID, offset by four bytes, used to prevent replay attacks_
* time_point `expiration` - _Expiration time of the transaction_
* vector\<operation\> `operations` - _A list of [Operations](#operation) contained in the transaction_
* extensions_type `extensions`
#### Example
```javascript
{
  'ref_block_num': 5337,
  'ref_block_prefix': 1010101010,
  'expiration': '2020-01-20T20:20:20',
  'operations': [
    [
      'vote',
      {
        'author': 'XGT123456',
        'permlink': 'some-permalink',
        'voter': 'XGT123456',
        'weight': 10000
      }
    ]
  ],
  'extensions': [],
  'signatures': [],
}
```

---

### Signed Transaction
The structural properties of a signed transaction.
#### Fields
* UInt16 `ref_block_num` - _Last two bytes of a block in the merkel tree, used to prevent replay attacks_
* UInt32 `ref_block_prefix` - _Four bytes of the block ID, offset by four bytes, used to prevent replay attacks_
* time_point `expiration` - _Expiration time of the transaction_
* vector\<operation\> `operations` - _List of [Operations](#operation) contained in the transaction_
* extensions_type `extensions`
* vector\<signature_type\> `signatures` - _List of singatures for the transaction_
#### Example
```javascript
{
  'ref_block_num': 5337,
  'ref_block_prefix': 1010101010,
  'expiration': '2020-01-20T20:20:20',
  'operations': [
    [
      'vote',
      {
        'author': 'XGT123456',
        'permlink': 'some-permalink',
        'voter': 'XGT123456',
        'weight': 10000
      }
    ]
  ],
  'extensions': [],
  'signatures': ['494ddd2e51fdf6c4cd5a8d941...'],
}
```

### Block
A block is a committed list of transactions, signed by a witness. It references some given merkel parent. Transactions must be signed (see [Transactions](#transaction)).

```javascript
"block":{
  "previous": "000...",
  "timestamp": '2020-01-20T20:20:20',
  "witness":"",
  "transaction_merkle_root": "000..",
  "extensions": [],
  "witness_signature": "0fe4...",
  "transactions":[]
}
```

---

### Operation
An operation is a tuple of a string and a dictionary. See the operations manual for more information, 
including a list of operations and sample operation formats.
#### Fields
* String `op_name` - _a snake-cased name for an operation_
* Dictionary `op` - _a potentially nested dictionary containing the operation data_
#### Example

```javascript
['comment', {}]
```
## Plugin: Block API

Namespace: `block_api`

### Procedure: get\_block\_header
Returns block header information for specified block.
#### Arguments
* uint32\_t `block_num` - _Block number._
#### Returns
* block\_header `header` - _Header information for specified block or null if block not found._

### Procedure: get\_block
Returns block information for specified block.
#### Arguments
* uint32\_t `block_num` - _Block number._
#### Returns
* api\_signed\_block\_object `block` - _Block information for specified block or null if block not found._
## Plugin: Chain API

Namespace: `chain_api`

### Procedure: push_block
Push a block to the chain.
#### Arguments
* signed_block `block` - _The block to be pushed to the chain._
* bool `currently_syncing` - _description, default false_
#### Returns
* bool `success` - _true if the block was successfully pushed, false otherwise._
* String `error` - _An error if present, null otherwise_
```javascript
// some example code
```

---

### Procedure: push_transaction
Push a transaction to the chain.
#### Arguments
* signed_transaction `tx` - _The transaction to push to the chain_
#### Returns
* bool `success` - _True if the tx was successfully pushed, false otherwise._
* String `error` - _An error if present, null otherwise_
```javascrip
// some example code
```
## Plugin: Contract API

Namespace: `contract_api`

[//]: # (TODO Procedure: get_contract
        args: bool example = true
        return: bool example = true
)

[//]: # (TODO Procedure: list_owner_contracts
        args: bool example = true
        return: bool example = true
)
## Plugin: Database API

## Globals

Namespace:  `database_api`

### Procedure:  get_config
Retrieves compile-time constants.
#### Example JSON Payload Format
```javascript
{}
```
#### Example JSON Response
```javascript
{
  "IS_TEST_NET": false,
  "SMT_MAX_VOTABLE_ASSETS": 2,
  "SMT_VESTING_WITHDRAW_INTERVAL_SECONDS": 604800,
  "SMT_UPVOTE_LOCKOUT": 43200,
  "SMT_EMISSION_MIN_INTERVAL_SECONDS": 21600,
  "SMT_EMIT_INDEFINITELY": 4294967295,
  "SMT_MAX_NOMINAL_VOTES_PER_DAY": 1000,
  "SMT_MAX_VOTES_PER_REGENERATION": 7000,
  "SMT_DEFAULT_VOTES_PER_REGEN_PERIOD": 50,
  "SMT_DEFAULT_PERCENT_CURATION_REWARDS": 2500,
  "SMT_INITIAL_VESTING_PER_UNIT": 1000000,
  "SMT_BALLAST_SUPPLY_PERCENT": 10,
  "SMT_MAX_ICO_TIERS": 10,
  "SBD_SYMBOL": {
    "nai": "@@000000013",
    "precision": 3
  },
  "XGT_SYMBOL": {
    "nai": "@@000000021",
    "precision": 3
  },
  "VESTS_SYMBOL": {
    "nai": "@@000000037",
    "precision": 6
  },
  "SBD_SYMBOL_STR": "SBD",
  "XGT_SYMBOL_STR": "XGT",
  "VESTS_SYMBOL_STR": "VESTS",
  "XGT_INITIAL_VOTE_POWER_RATE": 40,
  "XGT_REDUCED_VOTE_POWER_RATE": 10,
  "XGT_100_PERCENT": 10000,
  "XGT_1_PERCENT": 100,
  "XGT_ACCOUNT_RECOVERY_REQUEST_EXPIRATION_PERIOD": "86400000000",
  "XGT_ACTIVE_CHALLENGE_COOLDOWN": "86400000000",
  "XGT_ACTIVE_CHALLENGE_FEE": {
    "amount": "2000",
    "precision": 3,
    "nai": "@@000000021"
  },
  "XGT_ADDRESS_PREFIX": "XGT",
  "XGT_APR_PERCENT_MULTIPLY_PER_BLOCK": "102035135585887",
  "XGT_APR_PERCENT_MULTIPLY_PER_HOUR": "119577151364285",
  "XGT_APR_PERCENT_MULTIPLY_PER_ROUND": "133921203762304",
  "XGT_APR_PERCENT_SHIFT_PER_BLOCK": 87,
  "XGT_APR_PERCENT_SHIFT_PER_HOUR": 77,
  "XGT_APR_PERCENT_SHIFT_PER_ROUND": 83,
  "XGT_BANDWIDTH_AVERAGE_WINDOW_SECONDS": 604800,
  "XGT_BANDWIDTH_PRECISION": 1000000,
  "XGT_BENEFICIARY_LIMIT": 128,
  "XGT_BLOCKCHAIN_PRECISION": 1000,
  "XGT_BLOCKCHAIN_PRECISION_DIGITS": 3,
  "XGT_BLOCKCHAIN_HARDFORK_VERSION": "0.23.0",
  "XGT_BLOCKCHAIN_VERSION": "0.23.0",
  "XGT_BLOCK_INTERVAL": 3,
  "XGT_BLOCKS_PER_DAY": 28800,
  "XGT_BLOCKS_PER_HOUR": 1200,
  "XGT_BLOCKS_PER_YEAR": 10512000,
  "XGT_CASHOUT_WINDOW_SECONDS": 604800,
  "XGT_CHAIN_ID": "4e08b752aff5f66e1339cb8c0a8bca14c4ebb238655875db7dade86349091197",
  "XGT_COMMENT_REWARD_FUND_NAME": "comment",
  "XGT_COMMENT_TITLE_LIMIT": 256,
  "XGT_CONTENT_APR_PERCENT": 3875,
  "XGT_CONTENT_CONSTANT_HF0": "2000000000000",
  "XGT_CONTENT_CONSTANT_HF21": "2000000000000",
  "XGT_CONTENT_REWARD_PERCENT_HF16": 7500,
  "XGT_CONTENT_REWARD_PERCENT_HF21": 6500,
  "XGT_CONVERSION_DELAY": "302400000000",
  "XGT_CONVERSION_DELAY_PRE_HF_16": "604800000000",
  "XGT_CREATE_ACCOUNT_WITH_XGT_MODIFIER": 30,
  "XGT_CURATE_APR_PERCENT": 3875,
  "XGT_CUSTOM_OP_DATA_MAX_LENGTH": 8192,
  "XGT_CUSTOM_OP_ID_MAX_LENGTH": 32,
  "XGT_DEFAULT_SBD_INTEREST_RATE": 1000,
  "XGT_DOWNVOTE_POOL_PERCENT_HF21": 2500,
  "XGT_EQUIHASH_K": 6,
  "XGT_EQUIHASH_N": 140,
  "XGT_FEED_HISTORY_WINDOW": 84,
  "XGT_FEED_HISTORY_WINDOW_PRE_HF_16": 168,
  "XGT_FEED_INTERVAL_BLOCKS": 1200,
  "XGT_GENESIS_TIME": "2020-04-14T04:53:35",
  "XGT_HARDFORK_REQUIRED_WITNESSES": 17,
  "XGT_HF21_CONVERGENT_LINEAR_RECENT_CLAIMS": "503600561838938636",
  "XGT_INFLATION_NARROWING_PERIOD": 250000,
  "XGT_INFLATION_RATE_START_PERCENT": 978,
  "XGT_INFLATION_RATE_STOP_PERCENT": 95,
  "XGT_INIT_MINER_NAME": "XGT0000000000000",
  "XGT_INIT_PUBLIC_KEY_STR": "XGT6LLegbAgLAy28EHrffBVuANFWcFgmqRMW13wBmTExqFE9SCkg4",
  "XGT_INIT_SUPPLY": "250000000000",
  "XGT_SBD_INIT_SUPPLY": "7000000000",
  "XGT_INIT_TIME": "1970-01-01T00:00:00",
  "XGT_IRREVERSIBLE_THRESHOLD": 7500,
  "XGT_LIQUIDITY_APR_PERCENT": 750,
  "XGT_LIQUIDITY_REWARD_BLOCKS": 1200,
  "XGT_LIQUIDITY_REWARD_PERIOD_SEC": 3600,
  "XGT_LIQUIDITY_TIMEOUT_SEC": "604800000000",
  "XGT_MAX_ACCOUNT_CREATION_FEE": 1000000000,
  "XGT_MAX_ACCOUNT_NAME_LENGTH": 16,
  "XGT_MAX_ACCOUNT_WITNESS_VOTES": 30,
  "XGT_MAX_ASSET_WHITELIST_AUTHORITIES": 10,
  "XGT_MAX_AUTHORITY_MEMBERSHIP": 40,
  "XGT_MAX_BLOCK_SIZE": 393216000,
  "XGT_SOFT_MAX_BLOCK_SIZE": 2097152,
  "XGT_MAX_CASHOUT_WINDOW_SECONDS": 1209600,
  "XGT_MAX_COMMENT_DEPTH": 65535,
  "XGT_MAX_COMMENT_DEPTH_PRE_HF17": 6,
  "XGT_MAX_FEED_AGE_SECONDS": 604800,
  "XGT_MAX_INSTANCE_ID": "281474976710655",
  "XGT_MAX_MEMO_SIZE": 2048,
  "XGT_MAX_WITNESSES": 10,
  "XGT_MAX_VOTED_WITNESSES": 0,
  "XGT_MAX_MINER_WITNESSES": 10,
  "XGT_MAX_PERMLINK_LENGTH": 256,
  "XGT_MAX_PROXY_RECURSION_DEPTH": 4,
  "XGT_MAX_RATION_DECAY_RATE": 1000000,
  "XGT_MAX_RESERVE_RATIO": 20000,
  "XGT_MAX_SATOSHIS": "4611686018427387903",
  "XGT_MAX_SHARE_SUPPLY": "1000000000000000",
  "XGT_MAX_SIG_CHECK_DEPTH": 2,
  "XGT_MAX_SIG_CHECK_ACCOUNTS": 125,
  "XGT_MAX_TIME_UNTIL_EXPIRATION": 3600,
  "XGT_MAX_TRANSACTION_SIZE": 65536,
  "XGT_MAX_UNDO_HISTORY": 10000,
  "XGT_MAX_URL_LENGTH": 127,
  "XGT_MAX_VOTE_CHANGES": 5,
  "XGT_MAX_WITHDRAW_ROUTES": 10,
  "XGT_MAX_WITNESS_URL_LENGTH": 2048,
  "XGT_MIN_ACCOUNT_CREATION_FEE": 1,
  "XGT_MIN_ACCOUNT_NAME_LENGTH": 3,
  "XGT_MIN_BLOCK_SIZE_LIMIT": 65536,
  "XGT_MIN_BLOCK_SIZE": 115,
  "XGT_MIN_CONTENT_REWARD": {
    "amount": "1000",
    "precision": 3,
    "nai": "@@000000021"
  },
  "XGT_MIN_CURATE_REWARD": {
    "amount": "1000",
    "precision": 3,
    "nai": "@@000000021"
  },
  "XGT_MIN_PERMLINK_LENGTH": 0,
  "XGT_MIN_REPLY_INTERVAL": 20000000,
  "XGT_MIN_REPLY_INTERVAL_HF20": 3000000,
  "XGT_MIN_ROOT_COMMENT_INTERVAL": 300000000,
  "XGT_MIN_COMMENT_EDIT_INTERVAL": 3000000,
  "XGT_MIN_VOTE_INTERVAL_SEC": 3,
  "XGT_MINER_ACCOUNT": "XGT0000000000001",
  "XGT_MINER_PAY_PERCENT": 100,
  "XGT_MIN_FEEDS": 3,
  "XGT_MINING_REWARD": {
    "amount": "1000",
    "precision": 3,
    "nai": "@@000000021"
  },
  "XGT_MIN_LIQUIDITY_REWARD": {
    "amount": "1200000",
    "precision": 3,
    "nai": "@@000000021"
  },
  "XGT_MIN_LIQUIDITY_REWARD_PERIOD_SEC": 60000000,
  "XGT_MIN_PAYOUT_SBD": {
    "amount": "20",
    "precision": 3,
    "nai": "@@000000013"
  },
  "XGT_MIN_POW_REWARD": {
    "amount": "1000",
    "precision": 3,
    "nai": "@@000000021"
  },
  "XGT_MIN_PRODUCER_REWARD": {
    "amount": "1000",
    "precision": 3,
    "nai": "@@000000021"
  },
  "XGT_MIN_TRANSACTION_EXPIRATION_LIMIT": 15,
  "XGT_MIN_TRANSACTION_SIZE_LIMIT": 1024,
  "XGT_MIN_UNDO_HISTORY": 10,
  "XGT_NULL_ACCOUNT": "XGT0000000000002",
  "XGT_NUM_INIT_MINERS": 1,
  "XGT_RECOVERY_AUTH_HISTORY_TRACKING_START_BLOCK_NUM": 3186477,
  "XGT_RECOVERY_AUTH_RECOVERY_PERIOD": "2592000000000",
  "XGT_RECOVERY_CHALLENGE_COOLDOWN": "86400000000",
  "XGT_RECOVERY_CHALLENGE_FEE": {
    "amount": "30000",
    "precision": 3,
    "nai": "@@000000021"
  },
  "XGT_RECOVERY_UPDATE_LIMIT": 3600000000,
  "XGT_POST_AVERAGE_WINDOW": 86400,
  "XGT_POST_REWARD_FUND_NAME": "post",
  "XGT_POST_WEIGHT_CONSTANT": 1600000000,
  "XGT_POW_APR_PERCENT": 750,
  "XGT_PRODUCER_APR_PERCENT": 750,
  "XGT_PROXY_TO_SELF_ACCOUNT": "",
  "XGT_SBD_INTEREST_COMPOUND_INTERVAL_SEC": 2592000,
  "XGT_SECONDS_PER_YEAR": 31536000,
  "XGT_PROPOSAL_FUND_PERCENT_HF0": 0,
  "XGT_PROPOSAL_FUND_PERCENT_HF21": 1000,
  "XGT_RECENT_RSHARES_DECAY_TIME_HF19": "1296000000000",
  "XGT_RECENT_RSHARES_DECAY_TIME_HF17": "2592000000000",
  "XGT_REVERSE_AUCTION_WINDOW_SECONDS": 300,
  "XGT_ROOT_POST_PARENT": "",
  "XGT_SAVINGS_WITHDRAW_REQUEST_LIMIT": 100,
  "XGT_SAVINGS_WITHDRAW_TIME": "259200000000",
  "XGT_SBD_START_PERCENT_HF14": 200,
  "XGT_SBD_START_PERCENT_HF20": 900,
  "XGT_SBD_STOP_PERCENT_HF14": 500,
  "XGT_SBD_STOP_PERCENT_HF20": 1000,
  "XGT_SECOND_CASHOUT_WINDOW": 2592000,
  "XGT_SOFT_MAX_COMMENT_DEPTH": 255,
  "XGT_START_MINER_VOTING_BLOCK": 864000,
  "XGT_START_VESTING_BLOCK": 201600,
  "XGT_TEMP_ACCOUNT": "XGT0000000000003",
  "XGT_UPVOTE_LOCKOUT_SECONDS": 43200,
  "XGT_VESTING_FUND_PERCENT_HF16": 1500,
  "XGT_VESTING_WITHDRAW_INTERVALS": 13,
  "XGT_VESTING_WITHDRAW_INTERVAL_SECONDS": 604800,
  "XGT_VOTE_DUST_THRESHOLD": 50000000,
  "XGT_VOTING_MANA_REGENERATION_SECONDS": 432000,
  "XGT_VIRTUAL_SCHEDULE_LAP_LENGTH": "18446744073709551615",
  "XGT_VIRTUAL_SCHEDULE_LAP_LENGTH2": "340282366920938463463374607431768211455",
  "XGT_VOTES_PER_PERIOD_SMT_HF": 50,
  "XGT_MAX_LIMIT_ORDER_EXPIRATION": 2419200,
  "XGT_RD_MIN_DECAY_BITS": 6,
  "XGT_RD_MAX_DECAY_BITS": 32,
  "XGT_RD_DECAY_DENOM_SHIFT": 36,
  "XGT_RD_MAX_POOL_BITS": 64,
  "XGT_RD_MAX_BUDGET_1": "17179869183",
  "XGT_RD_MAX_BUDGET_2": 268435455,
  "XGT_RD_MAX_BUDGET_3": 2147483647,
  "XGT_RD_MAX_BUDGET": 268435455,
  "XGT_RD_MIN_DECAY": 64,
  "XGT_RD_MIN_BUDGET": 1,
  "XGT_RD_MAX_DECAY": 4294967295,
  "XGT_ACCOUNT_SUBSIDY_PRECISION": 10000,
  "XGT_WITNESS_SUBSIDY_BUDGET_PERCENT": 12500,
  "XGT_WITNESS_SUBSIDY_DECAY_PERCENT": 100000,
  "XGT_DEFAULT_ACCOUNT_SUBSIDY_DECAY": 347321,
  "XGT_DEFAULT_ACCOUNT_SUBSIDY_BUDGET": 797,
  "XGT_DECAY_BACKSTOP_PERCENT": 9000,
  "XGT_BLOCK_GENERATION_POSTPONED_TX_LIMIT": 5,
  "XGT_PENDING_TRANSACTION_EXECUTION_LIMIT": 200000,
  "XGT_TREASURY_ACCOUNT": "XGT0000000000004",
  "XGT_TREASURY_FEE": 10000,
  "XGT_PROPOSAL_MAINTENANCE_PERIOD": 3600,
  "XGT_PROPOSAL_MAINTENANCE_CLEANUP": 86400,
  "XGT_PROPOSAL_SUBJECT_MAX_LENGTH": 80,
  "XGT_PROPOSAL_MAX_IDS_NUMBER": 5,
  "XGT_NETWORK_TYPE": "mainnet",
  "XGT_DB_FORMAT_VERSION": "1"
}
```

---

### Procedure:  get_version
Returns version information and chain id of running node.
#### Example JSON Payload Format
```javascript
{}
```
#### Example JSON Response
```javascript
{
  "blockchain_version": "0.23.0",
  "steem_revision": "9fa5e99660ef4bd1080d94aa272675bc316781f6",
  "fc_revision": "9fa5e99660ef4bd1080d94aa272675bc316781f6",
  "chain_id": "4e08b752aff5f66e1339cb8c0a8bca14c4ebb238655875db7dade86349091197"
}
```

---

### Procedure:  get_dynamic_global_properties
Retrieves global properties.
#### Example JSON Payload Format
```javascript
{}
```
#### Example JSON Response
```javascript
{
  "id": 0,
  "head_block_number": 50,
  "head_block_id": "0000003289d845d2ec1c32f08ebd6831032bcdff",
  "time": "2020-05-02T12:39:06",
  "current_witness": "XGT0000000000000",
  "total_pow": "18446744073709551615",
  "num_pow_witnesses": 0,
  "virtual_supply": {
    "amount": "250000153357",
    "precision": 3,
    "nai": "@@000000021"
  },
  "current_supply": {
    "amount": "250000141757",
    "precision": 3,
    "nai": "@@000000021"
  },
  "confidential_supply": {
    "amount": "0",
    "precision": 3,
    "nai": "@@000000021"
  },
  "init_sbd_supply": {
    "amount": "7000000000",
    "precision": 3,
    "nai": "@@000000013"
  },
  "current_sbd_supply": {
    "amount": "11600",
    "precision": 3,
    "nai": "@@000000013"
  },
  "confidential_sbd_supply": {
    "amount": "0",
    "precision": 3,
    "nai": "@@000000013"
  },
  "total_vesting_fund_steem": {
    "amount": "66207",
    "precision": 3,
    "nai": "@@000000021"
  },
  "total_vesting_shares": {
    "amount": "1172891",
    "precision": 6,
    "nai": "@@000000037"
  },
  "total_reward_fund_steem": {
    "amount": "0",
    "precision": 3,
    "nai": "@@000000021"
  },
  "total_reward_shares2": "0",
  "pending_rewarded_vesting_shares": {
    "amount": "0",
    "precision": 6,
    "nai": "@@000000037"
  },
  "pending_rewarded_vesting_steem": {
    "amount": "0",
    "precision": 3,
    "nai": "@@000000021"
  },
  "sbd_interest_rate": 0,
  "sbd_print_rate": 10000,
  "maximum_block_size": 393216000,
  "required_actions_partition_percent": 0,
  "current_aslot": 527711,
  "recent_slots_filled": "1407374883553279",
  "participation_count": 49,
  "last_irreversible_block_num": 40,
  "target_votes_per_period": 10,
  "delegation_return_period": 432000,
  "reverse_auction_seconds": 300,
  "available_account_subsidies": 39850,
  "sbd_stop_percent": 1000,
  "sbd_start_percent": 900,
  "next_maintenance_time": "2020-05-02T13:36:35",
  "last_budget_time": "2020-05-02T12:36:35",
  "content_reward_percent": 6500,
  "vesting_reward_percent": 1500,
  "sps_fund_percent": 1000,
  "sps_interval_ledger": {
    "amount": "11368",
    "precision": 3,
    "nai": "@@000000013"
  },
  "downvote_pool_percent": 2500,
  "smt_creation_fee": {
    "amount": "1000",
    "precision": 3,
    "nai": "@@000000013"
  }
}
```

---

### Procedure:  get_witness_schedule
Retrieves witness schedule.
#### Example JSON Payload Format
```javascript
{}
```
#### Example JSON Response
```javascript
{
  "id": 0,
  "current_virtual_time": "0",
  "next_shuffle_block_num": 71,
  "current_shuffled_witnesses": [
    "XGT0000000000000",
    "XGT0000000000000",
    "XGT0000000000000",
    "XGT0000000000000",
    "XGT0000000000000",
    "XGT0000000000000",
    "XGT0000000000000",
    "XGT0000000000000",
    "XGT0000000000000",
    "XGT0000000000000"
  ],
  "num_scheduled_witnesses": 1,
  "elected_weight": 1,
  "timeshare_weight": 5,
  "miner_weight": 1,
  "witness_pay_normalization_factor": 2,
  "median_props": {
    "account_creation_fee": {
      "amount": "30",
      "precision": 3,
      "nai": "@@000000021"
    },
    "maximum_block_size": 131072,
    "sbd_interest_rate": 1000,
    "account_subsidy_budget": 797,
    "account_subsidy_decay": 347321
  },
  "majority_version": "0.0.0",
  "max_voted_witnesses": 0,
  "max_miner_witnesses": 10,
  "hardfork_required_witnesses": 17,
  "account_subsidy_rd": {
    "resource_unit": 10000,
    "budget_per_time_unit": 797,
    "pool_eq": 157691079,
    "max_pool_size": 157691079,
    "decay_params": {
      "decay_per_time_unit": 347321,
      "decay_per_time_unit_denom_shift": 36
    },
    "min_decay": 0
  },
  "account_subsidy_witness_rd": {
    "resource_unit": 10000,
    "budget_per_time_unit": 996,
    "pool_eq": 19706439,
    "max_pool_size": 19706439,
    "decay_params": {
      "decay_per_time_unit": 3473210,
      "decay_per_time_unit_denom_shift": 36
    },
    "min_decay": 0
  },
  "min_witness_account_subsidy_decay": 0
}
```

---

### Procedure:  get_hardfork_properties
Retrieves hard fork properties.
#### Example JSON Payload Format
```javascript
{}
```
#### Example JSON Response
```javascript
{
  "id": 0,
  "processed_hardforks": [
    "2020-04-14T04:53:35",
    "2016-04-25T17:30:00",
    "1970-01-01T00:00:00",
    "1970-01-01T00:00:00",
    "1970-01-01T00:00:00",
    "1970-01-01T00:00:00",
    "1970-01-01T00:00:00",
    "1970-01-01T00:00:00",
    "1970-01-01T00:00:00",
    "1970-01-01T00:00:00",
    "1970-01-01T00:00:00",
    "1970-01-01T00:00:00",
    "1970-01-01T00:00:00",
    "1970-01-01T00:00:00",
    "1970-01-01T00:00:00",
    "1970-01-01T00:00:00",
    "1970-01-01T00:00:00",
    "1970-01-01T00:00:00",
    "1970-01-01T00:00:00",
    "1970-01-01T00:00:00",
    "1970-01-01T00:00:00",
    "2019-08-27T15:00:00",
    "2019-08-29T15:00:00"
  ],
  "last_hardfork": 22,
  "current_hardfork_version": "0.22.0",
  "next_hardfork": "0.22.0",
  "next_hardfork_time": "2020-04-14T04:53:35"
}
```

---

### Procedure:  get_reward_funds
Retrieves reward funds.
#### Example JSON Payload Format
```javascript
{}
```
#### Example JSON Response
```javascript
{
  "funds": [
    {
      "id": 0,
      "name": "post",
      "reward_balance": {
        "amount": "208518",
        "precision": 3,
        "nai": "@@000000021"
      },
      "recent_claims": "340246401375486094597941380380970578510",
      "last_update": "2020-05-02T12:43:30",
      "content_constant": "2000000000000",
      "percent_curation_rewards": 5000,
      "percent_content_rewards": 10000,
      "author_reward_curve": "convergent_linear",
      "curation_reward_curve": "convergent_square_root"
    }
  ]
}
```

-------------------------------------------------------------------------------

## Witnesses

### Procedure:  list_witnesses
Return version information and chain_id of running node
#### Arguments
* UInt8 `start` - _ID of first witness to return._
* UInt8 `limit` - _Max # of witnesses to return._
* String `order` - _Order in which results should be sorted._
#### Example JSON Payload Format
```javascript
{
  "start": 0,
  "limit": 1,
  "order": "by_name"
}
```
#### Example JSON Response
```javascript
{
  "witnesses": [
    {
      "id": 0,
      "owner": "XGT0000000000000",
      "created": "1970-01-01T00:00:00",
      "url": "",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 451118,
      "last_confirmed_block_num": 555,
      "pow_worker": 0,
      "signing_key": "XGT6LLegbAgLAy28EHrffBVuANFWcFgmqRMW13wBmTExqFE9SCkg4",
      "props": {
        "account_creation_fee": {
          "amount": "30",
          "precision": 3,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072,
        "sbd_interest_rate": 1000,
        "account_subsidy_budget": 797,
        "account_subsidy_decay": 347321
      },
      "sbd_exchange_rate": {
        "base": {
          "amount": "0",
          "precision": 3,
          "nai": "@@000000021"
        },
        "quote": {
          "amount": "0",
          "precision": 3,
          "nai": "@@000000021"
        }
      },
      "last_sbd_exchange_update": "1970-01-01T00:00:00",
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.23.0",
      "hardfork_version_vote": "0.23.0",
      "hardfork_time_vote": "2020-08-21T00:46:40",
      "available_witness_account_subsidies": 536662
    }
  ]
}
```

---

### Procedure:  find_witnesses
Returns a list of witnesses corresponding to inputted wallet addresses.
#### Arguments
* Vector<String> `recoveries` - _List of wallet addresses to retreive associated witnesses._
#### Example JSON Payload Format
```javascript
{
  "recoveries": [
    "XGT0000000000000"
  ]
}
```
#### Example JSON Response
```javascript
{
  "witnesses": [
    {
      "id": 0,
      "owner": "XGT0000000000000",
      "created": "1970-01-01T00:00:00",
      "url": "",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 451046,
      "last_confirmed_block_num": 483,
      "pow_worker": 0,
      "signing_key": "XGT6LLegbAgLAy28EHrffBVuANFWcFgmqRMW13wBmTExqFE9SCkg4",
      "props": {
        "account_creation_fee": {
          "amount": "30",
          "precision": 3,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072,
        "sbd_interest_rate": 1000,
        "account_subsidy_budget": 797,
        "account_subsidy_decay": 347321
      },
      "sbd_exchange_rate": {
        "base": {
          "amount": "0",
          "precision": 3,
          "nai": "@@000000021"
        },
        "quote": {
          "amount": "0",
          "precision": 3,
          "nai": "@@000000021"
        }
      },
      "last_sbd_exchange_update": "1970-01-01T00:00:00",
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.23.0",
      "hardfork_version_vote": "0.23.0",
      "hardfork_time_vote": "2020-08-21T00:46:40",
      "available_witness_account_subsidies": 466736
    }
  ]
}
```

---

### Procedure:  list_witness_votes
Retrieves a list of witness votes.
#### Example JSON Payload Format
```javascript
{
  "start": 0,
  "limit": 1,
  "order": "by_name"
}
```
#### Example JSON Response
```javascript
{
  "witnesses": [
    {
      "id": 0,
      "owner": "XGT0000000000000",
      "created": "1970-01-01T00:00:00",
      "url": "",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 538762,
      "last_confirmed_block_num": 2,
      "pow_worker": 0,
      "signing_key": "XGT6LLegbAgLAy28EHrffBVuANFWcFgmqRMW13wBmTExqFE9SCkg4",
      "props": {
        "account_creation_fee": {
          "amount": "30",
          "precision": 3,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072,
        "sbd_interest_rate": 1000,
        "account_subsidy_budget": 797,
        "account_subsidy_decay": 347321
      },
      "sbd_exchange_rate": {
        "base": {
          "amount": "0",
          "precision": 3,
          "nai": "@@000000021"
        },
        "quote": {
          "amount": "0",
          "precision": 3,
          "nai": "@@000000021"
        }
      },
      "last_sbd_exchange_update": "1970-01-01T00:00:00",
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.23.0",
      "hardfork_version_vote": "0.23.0",
      "hardfork_time_vote": "2020-08-21T00:46:40",
      "available_witness_account_subsidies": 0
    }
  ]
}
```

---

### Procedure:  get_active_witnesses
Returns a list of active witnesses.
#### Example JSON Payload Format
```javascript
{}
```
#### Example JSON Response
```javascript
{
  "witnesses": [
    "XGT0000000000000",
    "XGT0000000000000",
    "XGT0000000000000",
    "XGT0000000000000",
    "XGT0000000000000",
    "XGT0000000000000",
    "XGT0000000000000",
    "XGT0000000000000",
    "XGT0000000000000",
    "XGT0000000000000"
  ]
}
```
-------------------------------------------------------------------------------

## Accounts

### Procedure:  list_accounts
List accounts ordered by specified key.
#### Arguments
* UInt8 `start` - _ID of first wallet to return._
* UInt8 `limit` - _Max number of results to return._
* String `order` - _Key by which to organize results._
#### Example JSON Payload Format
```javascript
{
  "start": 0,
  "limit": 1,
  "order": "by_name"
}
```
#### Example JSON Response
```javascript
```{
  "accounts": [
    {
      "id": 4,
      "name": "XGT0000000000000",
      "recovery": {
        "weight_threshold": 1,
        "account_auths": [

        ],
        "key_auths": [
          [
            "XGT6LLegbAgLAy28EHrffBVuANFWcFgmqRMW13wBmTExqFE9SCkg4",
            1
          ]
        ]
      },
      "money": {
        "weight_threshold": 1,
        "account_auths": [

        ],
        "key_auths": [
          [
            "XGT6LLegbAgLAy28EHrffBVuANFWcFgmqRMW13wBmTExqFE9SCkg4",
            1
          ]
        ]
      },
      "social": {
        "weight_threshold": 1,
        "account_auths": [

        ],
        "key_auths": [
          [
            "XGT6LLegbAgLAy28EHrffBVuANFWcFgmqRMW13wBmTExqFE9SCkg4",
            1
          ]
        ]
      },
      "memo_key": "XGT6LLegbAgLAy28EHrffBVuANFWcFgmqRMW13wBmTExqFE9SCkg4",
      "json_metadata": "",
      "social_json_metadata": "",
      "proxy": "",
      "last_recovery_update": "1970-01-01T00:00:00",
      "last_account_update": "1970-01-01T00:00:00",
      "created": "1970-01-01T00:00:00",
      "mined": true,
      "recovery_account": "",
      "last_account_recovery": "1970-01-01T00:00:00",
      "reset_account": "XGT0000000000002",
      "comment_count": 0,
      "lifetime_vote_count": 0,
      "post_count": 0,
      "can_vote": true,
      "voting_manabar": {
        "current_mana": 1529850,
        "last_update_time": 1588194636
      },
      "downvote_manabar": {
        "current_mana": 382462,
        "last_update_time": 1588194636
      },
      "balance": {
        "amount": "250000000000",
        "precision": 3,
        "nai": "@@000000021"
      },
      "savings_balance": {
        "amount": "0",
        "precision": 3,
        "nai": "@@000000021"
      },
      "sbd_balance": {
        "amount": "7000000000",
        "precision": 3,
        "nai": "@@000000013"
      },
      "sbd_seconds": "0",
      "sbd_seconds_last_update": "1970-01-01T00:00:00",
      "sbd_last_interest_payment": "1970-01-01T00:00:00",
      "savings_sbd_balance": {
        "amount": "0",
        "precision": 3,
        "nai": "@@000000013"
      },
      "savings_sbd_seconds": "0",
      "savings_sbd_seconds_last_update": "1970-01-01T00:00:00",
      "savings_sbd_last_interest_payment": "1970-01-01T00:00:00",
      "savings_withdraw_requests": 0,
      "reward_sbd_balance": {
        "amount": "0",
        "precision": 3,
        "nai": "@@000000013"
      },
      "reward_steem_balance": {
        "amount": "0",
        "precision": 3,
        "nai": "@@000000021"
      },
      "reward_vesting_balance": {
        "amount": "0",
        "precision": 6,
        "nai": "@@000000037"
      },
      "reward_vesting_steem": {
        "amount": "0",
        "precision": 3,
        "nai": "@@000000021"
      },
      "vesting_shares": {
        "amount": "1529850",
        "precision": 6,
        "nai": "@@000000037"
      },
      "delegated_vesting_shares": {
        "amount": "0",
        "precision": 6,
        "nai": "@@000000037"
      },
      "received_vesting_shares": {
        "amount": "0",
        "precision": 6,
        "nai": "@@000000037"
      },
      "vesting_withdraw_rate": {
        "amount": "1",
        "precision": 6,
        "nai": "@@000000037"
      },
      "next_vesting_withdrawal": "1969-12-31T23:59:59",
      "withdrawn": 0,
      "to_withdraw": 0,
      "withdraw_routes": 0,
      "curation_rewards": 0,
      "social_rewards": 0,
      "proxied_vsf_votes": [
        0,
        0,
        0,
        0
      ],
      "witnesses_voted_for": 0,
      "last_post": "1970-01-01T00:00:00",
      "last_root_post": "1970-01-01T00:00:00",
      "last_post_edit": "1970-01-01T00:00:00",
      "last_vote_time": "1970-01-01T00:00:00",
      "post_bandwidth": 0,
      "pending_claimed_accounts": 0,
      "is_smt": false
    }
  ]
}
```
---

### Procedure:  find_accounts
Returns list of wallets if inputted wallet addresses exist.
#### Variables

#### Arguments
* Array of Strings `accounts` - _Wallet addresses to search for._
#### Example JSON Payload Format
```javascript
{
  'accounts': [
    'XGT22NqCrWPExii6'
  ]
}
```
#### Example JSON Response
```javascript
{
  "accounts": [
    {
      "id": 5,
      "name": "XGT273AkZNcF6Eso",
      "recovery": {
        "weight_threshold": 1,
        "account_auths": [],
        "key_auths": [
          [
            "XGT7TVoUdXwWaMqSQ44TbL4LqpP97JvRjtAN1PNzDsRPe4DMxn38J", 1
          ]
        ]
      },
      "money": {
        "weight_threshold": 1,
        "account_auths": [],
        "key_auths": [
          [
            "XGT7GXB9CkXTgnErBQuGynn2vrDzG2dMknSZCHCxfT4g1D2fxifaT", 1
          ]
        ]
      },
      "social": {
        "weight_threshold": 1,
        "account_auths": [],
        "key_auths": [
          [
            "XGT52UzbG73WhBqAjUWebTtSxp5xLH4i8zXncptpnN14bPMs9cG8T", 1
          ]
        ]
      },
      "memo_key": "XGT5dVCSn4YnHcagT8vVnztfxpuHhRNBdda3t8kejbuWvjP9wBEfn",
      "json_metadata": "",
      "social_json_metadata": "",
      "proxy": "",
      "last_recovery_update": "1970-01-01T00:00:00",
      "last_account_update": "1970-01-01T00:00:00",
      "created": "2020-04-21T04:18:36",
      "mined": false,
      "recovery_account": "XGT0000000000000",
      "last_account_recovery": "1970-01-01T00:00:00",
      "reset_account": "XGT0000000000002",
      "comment_count": 0,
      "lifetime_vote_count": 0,
      "post_count": 0,
      "can_vote": true,
      "voting_manabar": {
        "current_mana": 0,
        "last_update_time": 1587442716
      },
      "downvote_manabar": {
        "current_mana": 0,
        "last_update_time": 1587442716
      },
      "balance": {
        "amount": "0",
        "precision": 3,
        "nai": "@@000000021"
      },
      "savings_balance": {
        "amount": "0",
        "precision": 3,
        "nai": "@@000000021"
      },
      "sbd_balance": {
        "amount": "0",
        "precision": 3,
        "nai": "@@000000013"
      },
      "sbd_seconds": "0",
      "sbd_seconds_last_update": "1970-01-01T00:00:00",
      "sbd_last_interest_payment": "1970-01-01T00:00:00",
      "savings_sbd_balance": {
        "amount": "0",
        "precision": 3,
        "nai": "@@000000013"
      },
      "savings_sbd_seconds": "0",
      "savings_sbd_seconds_last_update": "1970-01-01T00:00:00",
      "savings_sbd_last_interest_payment": "1970-01-01T00:00:00",
      "savings_withdraw_requests": 0,
      "reward_sbd_balance": {
        "amount": "0",
        "precision": 3,
        "nai": "@@000000013"
      },
      "reward_steem_balance": {
        "amount": "0",
        "precision": 3,
        "nai": "@@000000021"
      },
      "reward_vesting_balance": {
        "amount": "0",
        "precision": 6,
        "nai": "@@000000037"
      },
      "reward_vesting_steem": {
        "amount": "0",
        "precision": 3,
        "nai": "@@000000021"
      },
      "vesting_shares": {
        "amount": "0",
        "precision": 6,
        "nai": "@@000000037"
      },
      "delegated_vesting_shares": {
        "amount": "0",
        "precision": 6,
        "nai": "@@000000037"
      },
      "received_vesting_shares": {
        "amount": "0",
        "precision": 6,
        "nai": "@@000000037"
      },
      "vesting_withdraw_rate": {
        "amount": "0",
        "precision": 6,
        "nai": "@@000000037"
      },
      "next_vesting_withdrawal": "1969-12-31T23:59:59",
      "withdrawn": 0,
      "to_withdraw": 0,
      "withdraw_routes": 0,
      "curation_rewards": 0,
      "social_rewards": 0,
      "proxied_vsf_votes": [0, 0, 0, 0],
      "witnesses_voted_for": 0,
      "last_post": "1970-01-01T00:00:00",
      "last_root_post": "1970-01-01T00:00:00",
      "last_post_edit": "1970-01-01T00:00:00",
      "last_vote_time": "1970-01-01T00:00:00",
      "post_bandwidth": 0,
      "pending_claimed_accounts": 0,
      "is_smt": false
    }
  ]
}
```

---

### Procedure:  list_recovery_histories
List accounts ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  find_recovery_histories
List accounts ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  list_account_recovery_requests
List accounts ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  find_account_recovery_requests
List accounts ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  list_change_recovery_account_requests
List accounts ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  find_change_recovery_account_requests
List accounts ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  list_escrows
List accounts ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  list_escrows
List accounts ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  find_escrows
List accounts ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  list_withdraw_vesting_routes
List accounts ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  find_withdraw_vesting_routes
List accounts ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  list_savings_withdrawals
List accounts ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  find_savings_withdrawals
List accounts ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  list_vesting_delegations
List accounts ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  find_vesting_delegations
List accounts ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  list_vesting_delegation_expirations
List accounts ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  find_vesting_delegation_expirations
List accounts ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  list_sbd_conversion_requests
List accounts ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  find_sbd_conversion_requests
List accounts ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  list_decline_voting_rights_requests
List accounts ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  find_decline_voting_rights_requests
List accounts ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

-------------------------------------------------------------------------------

## Comments

### Procedure:  list_comments
List accounts ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  find_comments
List accounts ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  list_votes
List accounts ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  find_votes
List accounts ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

-------------------------------------------------------------------------------

## Market

### Procedure:  list_limit_orders
List accounts ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  find_limit_orders
List accounts ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  get_order_book
List accounts ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

-------------------------------------------------------------------------------

## SPS

### Procedure:  list_proposals
List accounts ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  find_proposals
List accounts ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  list_proposal_votes
List accounts ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

-------------------------------------------------------------------------------

## Authority

### Procedure:  get_transaction_hex
Get a hexdump of the serialized binary form of a transaction
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  get_required_signatures
This API will take a partially signed transaction and a set of public keys that
the recovery has the ability to sign for and return the minimal subset of
public keys that should add signatures to the transaction.
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  get_potential_signatures
This method will return the set of all public keys that could possibly sign for
a given transaction.  This call can be used by wallets to filter their set of
public keys to just the relevant subset prior to calling @ref
get_required_signatures to get the minimum subset.
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  verify_authority
@return true of the @ref trx has all of the required signatures, otherwise throws an exception
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  verify_account_authority
@return true if the signers have enough authority to authorize an account
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  verify_signatures
This is a general purpose API that checks signatures against accounts for an
arbitrary sha256 hash using the existing authority structures in Steem
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

-------------------------------------------------------------------------------

## SMTs

### Procedure:  get_nai_pool
@return array of Numeric Asset Identifier (NAI) available to be used for new
SMT to be created.
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  list_smt_contributions
description
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  find_smt_contributions
description#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  list_smt_tokens
description#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  find_smt_tokens
description
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  list_smt_token_emissions
description
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  find_smt_token_emissions
description
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

## Plugin: Transaction API

Namespace: `transaction_api`

Valid return status codes:

| Status	                  | Meaning                                                                                             |
|---------------------------|-----------------------------------------------------------------------------------------------------|
| unknown	                  | Expiration time in future, transaction not included in block or mempool                             |
| within_mempool	          | Transaction in mempool                                                                              | 
| within_reversible_block	  | Transaction has been included in block, block not irreversible (result will also contain block_num) |
| within_irreversible_block	| Transaction has been included in block, block is irreversible (result will also contain block_num)  |
| expired_reversible	      | Transaction has expired, transaction is not irreversible (transaction could be in a fork)           | 
| expired_irreversible	    | Transaction has expired, transaction is irreversible (transaction cannot be in a fork)              | 
| too_old	                  | Transaction is too old, and is not available from the tx status API                                 |

### Procedure: find_transaction
Get the current status of a transaction indicated by a transaction ID.
#### Arguments
* String `transaction_id` - _Some transaction ID._
* Timestamp `expiration` (optional) - _Transaction expiration formatted yyyy-mm-ddT00:00:00._
#### Returns
* String `status` - _A valid status._
* UInt32_t `block_num` - _Block number._
#### Example JSON Payload Format
```javascript
{
  "transaction_id": "868e8d918f5fb370d5d4b47aaf9ba438ba06457f"
}
```
#### Example JSON Response
```javascript
{
  "status": "within_irreversible_block",
  "block_num": 1085
}
```

[//]: # (TODO Procedure: get_transaction_hex
        args: vector< variant > get_transaction_hex_args
        return: annotated_signed_transaction
)

[//]: # (TODO Procedure: broadcast_transaction
        args: vector< variant > broadcast_transaction_args
        return: transaction_id_type id
)

[//]: # (TODO Procedure: broadcast_block
        args: signed_block block
        return: void_type broadcast_block_return
)
## Plugin: Account by Key API

Namespace: `accounts_by_key_api`

### Procedure: get_key_references
Returns all wallets that have the key associated with their owner or active authorities.
#### Arguments
* Array<String> `keys` - _Array of keys to look up._
#### Returns

[//]: # (TODO change account_name_type to wallet_name_type)

* Array<Array<account\_name\_type> > `wallets` - _Nested array of wallet addresses matching each key._
#### Example JSON Payload Format
```javascript
{
  "keys": [
    "XGT6ejjRv1fDDbe9bbNfx98U9847hvfDzWvFXTriHG2M5xLaWoCu5"
  ]
}
```
#### Example JSON Response
```javascript
{
  "accounts": [
    [
      "XGTz579hvZFWwUSn"
    ]
  ]
}
```

### Procedure: generate_wallet_name
Generates a unique wallet name remotely.
#### Arguments
* Array<public\_key\_type> `recovery_keys` - _Array of recovery keys for new wallet._
#### Returns

[//]: # (TODO change account_name_type to wallet_name_type)

* account_name_type `wallet_name` - _XGT wallet name._
#### Example JSON Payload Format

[//]: # (TODO change wallet name below to recovery keys)

```javascript
{
  "recovery_keys": [
    "XGT6ejjRv1fDDbe9bbNfx98U9847hvfDzWvFXTriHG2M5xLaWoCu5"
  ]
}
```
#### Example JSON Response

[//]: # (TODO update format of output below)

```javascript
{
  "accounts": [
    [
      "XGTz579hvZFWwUSn"
    ]
  ]
}
```
## Plugin: Wallet History API

Namespace: `wallet_history_api`

Describe blocks and transactions at either a specific point in the chain, or which are associated with a specific wallet.

### Common return types:

#### API Operations
##### Fields
* String `trx_id` - _ID of the transaction._
* UInt32 `block` - _ID of the block._
* UInt32 `trx_in_block` - _Number of transactions._
* UInt32 `op_in_trx` - _Number of operations in transactions._
* UInt32 `virtual_op` - _Is the operation virtual, 1 for yes, 0 for no._
* Timestamp `timestamp` - _The time of the block commit._
* Op `op` - _the serialized operation._

##### Example
```javascript
{ 
  'trx_id': 'f1b4...',
  'block': 333333,
  'trx_in_block': 24,
  'virtual_op': 0,
  'op_in_trx': 0,
  'timestamp': '2020-01-20T20:20:20',
  'op': ['some_operation', {}]
}
```
---

### Procedure: get_ops_in_block
Retrieve all operations in a block specified by a block ID.
#### Arguments
* UInt32 `block_num` - _Block number._
* Boolean `only_virtual` - _Set to true to return only virtual operations._
#### Returns
* Multiset `api_operation_object - `[API Operations](#api-operations)

#### Example JSON Payload Format
```javascript
{
  'block_num': '1756',
  'only_virtual': false
}

```
#### Example JSON Response
```javascript
{
  "ops": [
    {
      "trx_id": "8be030ad61f9926f5970df3a6e375d46a6f542d7",
      "block": 1756,
      "trx_in_block": 0,
      "op_in_trx": 0,
      "virtual_op": 0,
      "timestamp": "2020-04-21T16:46:30",
      "op": {
        "type": "account_create_operation",
        "value": {
          "fee": {
            "amount": "0",
            "precision": 3,
            "nai": "@@000000021"
          },
          "creator": "XGT0000000000000",
          "new_account_name": "",
          "recovery": {
            "weight_threshold": 1,
            "account_auths": [],
            "key_auths": [
              [
                "XGT6eLW3zhTK3oZfDMQ95U17ySabat4zvNUVC825Jc8kYPfLJ2taV", 1
              ]
            ]
          },
          "money": {
            "weight_threshold": 1,
            "account_auths": [],
            "key_auths": [
              [
                "XGT78ARhThmw5tPhYpmcYgG2L2ynZsQ136Rc3R9aL2XfeM3g8jGD2", 1
              ]
            ]
          },
          "social": {
            "weight_threshold": 1,
            "account_auths": [],
            "key_auths": [
              [
                "XGT5GSFown3qZ8bs3ainK7vxz6diFaiLMFJCXoEVUPUzpSCfHLam2", 1
              ]
            ]
          },
          "memo_key": "XGT6ZcN5pjPCSMm7J843bjch5uSNXXNwCMyW8eEHQusMVp2yhfq2f",
          "json_metadata": ""
        }
      }
    },
    {
      "trx_id": "0000000000000000000000000000000000000000",
      "block": 1756,
      "trx_in_block": 4294967295,
      "op_in_trx": 0,
      "virtual_op": 1,
      "timestamp": "2020-04-21T16:46:33",
      "op": {
        "type": "producer_reward_operation",
        "value": {
          "producer": "XGT0000000000000",
          "vesting_shares": {
            "amount": "49",
            "precision": 6,
            "nai": "@@000000037"
          }
        }
      }
    }
  ]
}
```

---

[//]: # (TODO Procedure: get_transaction
        args: transaction_id_type id
        return: annotated_signed_transaction
)

---

[//]: # (TODO Procedure: enum_virtual_ops
        args: uint32_t block_range_begin = 1, uint32_t block_range_end = 2
        return: vector<api_operation_object> ops, uint32_t next_block_range_begin = 0
      )

---

### Procedure: get_wallet_history
Retrieve a list of objects, containing an index and an [API operation object](#api-operation-objects)
#### Arguments
* String `wallet` - _Wallet address._
* UInt64 `start` - _Paging start, first position._
* UInt64 `limit` - _Number of records to return._
#### Example JSON Payload Format
```javascript
{
  'wallet': 'XGT29ZZP6RMk9KCT'
}
```
#### Example JSON Response
```javascript
{
  "history": [
    [
      1,
      {
        "trx_id": "c2a5cd89291ae96aa266fbf5b9e580540a17a499",
        "block": 2479,
        "trx_in_block": 0,
        "op_in_trx": 0,
        "virtual_op": 0,
        "timestamp": "2020-04-21T17:22:39",
        "op": {
          "type": "wallet_create_operation",
          "value": {
            "fee": {
              "amount": "0",
              "precision": 3,
              "nai": "@@000000021"
            },
            "creator": "XGT0000000000000",
            "new_wallet_name": "",
            "recovery": {
              "weight_threshold": 1,
              "wallet_auths": [

              ],
              "key_auths": [
                [
                  "XGT7ReW2VTtHkmvTsC8X2MYMHShec99usd8STaS9Zuy4jSekvsKQJ",
                  1
                ]
              ]
            },
            "money": {
              "weight_threshold": 1,
              "wallet_auths": [

              ],
              "key_auths": [
                [
                  "XGT7xicXr8xJL71SdpT7oNPXi8v5AEk4wMfz5hHAz8yhi9DKJTfBB",
                  1
                ]
              ]
            },
            "social": {
              "weight_threshold": 1,
              "wallet_auths": [

              ],
              "key_auths": [
                [
                  "XGT6sMS29Cir6Aa4wVixSL3oenA3qBDUqLpMGWvG98zzNr1ozh533",
                  1
                ]
              ]
            },
            "memo_key": "XGT7RpXJMyd7dkuTv7tQZQP2PBBuexbPbvHrnExDv6Fo6EMGNPMm3",
            "json_metadata": ""
          }
        }
      }
    ]
  ]
}
```


