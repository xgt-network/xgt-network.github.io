# XGT JSON RPC API documents

#### Table of contents
  * [Block API](#block_api)
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
#### Example JSON Payload Format
```javascript
{
  block_num: 569557
}
```
#### Example JSON Response
```javascript
{
  "header": {
    "previous": "0008b0d4a5c5591e25331f3c447352f68eccde4e",
    "timestamp": "2021-06-24T19:37:44",
    "witness": "XGT2iJ45vibYdMczNQLqXbvQMNb6vAtTcY9okRoaPF6",
    "transaction_merkle_root": "544046d6a138bae0c2898f469b55d15f5ed1385f",
    "extensions": [

    ]
  }
}
```
---

### Procedure: get\_block
Returns block information for specified block.
#### Arguments
* uint32\_t `block_num` - _Block number._
#### Returns
* api\_signed\_block\_object `block` - _Block information for specified block or null if block not found._
#### Example JSON Payload Format
```javascript
{
  block_num: 569557
}
```
#### Example JSON Response
```javascript
{
  "block": {
    "previous": "0008b0d4a5c5591e25331f3c447352f68eccde4e",                                                       "timestamp": "2021-06-24T19:37:44",                                                                           "witness": "XGT2iJ45vibYdMczNQLqXbvQMNb6vAtTcY9okRoaPF6",
      "transaction_merkle_root": "544046d6a138bae0c2898f469b55d15f5ed1385f",
      "extensions": [

      ],
      "witness_signature": "2093870dd8cb9c5418daf3d369e1fd80742bae5af2d0554f47828379c21b0014b7753ffb5de13bd4c3d2ec9b3a835d7be197df14f0a8d8fa9fb1dcb37d12285416",
      "transactions": [
      {
        "ref_block_num": 45267,
        "ref_block_prefix": 610474609,
        "expiration": "2021-06-24T20:37:37",
        "operations": [
        {
          "type": "pow_operation",
          "value": {
            "work": {
              "type": "sha2_pow",
              "value": {
                "input": {
                  "worker_account": "XGTGmzVNN1ucwYWhSQKUyG5wuaGXvhjzZ25sf41WV6B",
                  "prev_block": "0008b0d3711a6324c043ded65028ce7513e1774d",
                  "nonce": 1246464257
                },
                "proof": "0000001ed73109cc43d0239a39ac20ece7e416e5c77517c92d232de77456592d",
                "prev_block": "0008b0d3711a6324c043ded65028ce7513e1774d",
                "pow_summary": 3840766736
              }
            },
            "props": {
              "account_creation_fee": {
                "amount": "0",
                "precision": 8,
                "nai": "@@000000021"
              },
              "maximum_block_size": 131072
            }
          }
        }
        ],
        "extensions": [

        ],
        "signatures": [
          "204e60ca06af3c50dcc0d7c4d602c2828b794093617b5064a4b4ce2a6e2c74972550cb979bc8052dfe4e0c7192a12752e955286d6462739f61d2b36afb5984efbd"
        ]
      }
      ],
      "block_id": "0008b0d5e95cd667c50898a36d4b8bfb61a6e41c",
      "signing_key": "XGT56HuM2Esc4saSkvXSdQ7UTbTxeRvCnHikqeYiDNiKVesrVknX1",
      "transaction_ids": [
        "f6d5c0bf692467b5a1fb48814b9bb675874f5404"
      ]
  }
}
```
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
  "XTT_MAX_VOTABLE_ASSETS": 2,
  "XTT_UPVOTE_LOCKOUT": 43200,
  "XTT_EMIT_INDEFINITELY": 4294967295,
  "XTT_MAX_NOMINAL_VOTES_PER_DAY": 1000,
  "XTT_DEFAULT_VOTES_PER_REGEN_PERIOD": 50,
  "XTT_BALLAST_SUPPLY_PERCENT": 10,
  "XTT_MAX_ICO_TIERS": 10,
  "XGT_SYMBOL": {
    "nai": "@@000000021",
    "precision": 8
  },
  "XGT_SYMBOL_STR": "XGT",
  "XGT_INITIAL_VOTE_POWER_RATE": 40,
  "XGT_REDUCED_VOTE_POWER_RATE": 10,
  "XGT_100_PERCENT": 10000,
  "XGT_1_PERCENT": 100,
  "XGT_WALLET_RECOVERY_REQUEST_EXPIRATION_PERIOD": "86400000000",
  "XGT_ACTIVE_CHALLENGE_COOLDOWN": "86400000000",
  "XGT_ACTIVE_CHALLENGE_FEE": {
    "amount": "2000",
    "precision": 8,
    "nai": "@@000000021"
  },
  "XGT_ADDRESS_PREFIX": "XGT",
  "XGT_WALLET_NAME_LENGTH": 40,
  "XGT_APR_PERCENT_MULTIPLY_PER_BLOCK": "102035135585887",
  "XGT_APR_PERCENT_MULTIPLY_PER_HOUR": "119577151364285",
  "XGT_APR_PERCENT_MULTIPLY_PER_ROUND": "133921203762304",
  "XGT_APR_PERCENT_SHIFT_PER_BLOCK": 87,
  "XGT_APR_PERCENT_SHIFT_PER_HOUR": 77,
  "XGT_APR_PERCENT_SHIFT_PER_ROUND": 83,
  "XGT_BANDWIDTH_AVERAGE_WINDOW_SECONDS": 604800,
  "XGT_BANDWIDTH_PRECISION": 1000000,
  "XGT_BLOCK# XGT JSON RPC API documents

#### Table of contents
  * [Block API](#block_api)
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
#### Example JSON Payload Format
```javascript
{
  block_num: 569557
}
```
#### Example JSON Response
```javascript
{
  "header": {
    "previous": "0008b0d4a5c5591e25331f3c447352f68eccde4e",
    "timestamp": "2021-06-24T19:37:44",
    "witness": "XGT2iJ45vibYdMczNQLqXbvQMNb6vAtTcY9okRoaPF6",
    "transaction_merkle_root": "544046d6a138bae0c2898f469b55d15f5ed1385f",
    "extensions": [

    ]
  }
}
```
---

### Procedure: get\_block
Returns block information for specified block.
#### Arguments
* uint32\_t `block_num` - _Block number._
#### Returns
* api\_signed\_block\_object `block` - _Block information for specified block or null if block not found._
#### Example JSON Payload Format
```javascript
{
  block_num: 569557
}
```
#### Example JSON Response
```javascript
{
  "block": {
    "previous": "0008b0d4a5c5591e25331f3c447352f68eccde4e",                                                       "timestamp": "2021-06-24T19:37:44",                                                                           "witness": "XGT2iJ45vibYdMczNQLqXbvQMNb6vAtTcY9okRoaPF6",
      "transaction_merkle_root": "544046d6a138bae0c2898f469b55d15f5ed1385f",
      "extensions": [

      ],
      "witness_signature": "2093870dd8cb9c5418daf3d369e1fd80742bae5af2d0554f47828379c21b0014b7753ffb5de13bd4c3d2ec9b3a835d7be197df14f0a8d8fa9fb1dcb37d12285416",
      "transactions": [
      {
        "ref_block_num": 45267,
        "ref_block_prefix": 610474609,
        "expiration": "2021-06-24T20:37:37",
        "operations": [
        {
          "type": "pow_operation",
          "value": {
            "work": {
              "type": "sha2_pow",
              "value": {
                "input": {
                  "worker_account": "XGTGmzVNN1ucwYWhSQKUyG5wuaGXvhjzZ25sf41WV6B",
                  "prev_block": "0008b0d3711a6324c043ded65028ce7513e1774d",
                  "nonce": 1246464257
                },
                "proof": "0000001ed73109cc43d0239a39ac20ece7e416e5c77517c92d232de77456592d",
                "prev_block": "0008b0d3711a6324c043ded65028ce7513e1774d",
                "pow_summary": 3840766736
              }
            },
            "props": {
              "account_creation_fee": {
                "amount": "0",
                "precision": 8,
                "nai": "@@000000021"
              },
              "maximum_block_size": 131072
            }
          }
        }
        ],
        "extensions": [

        ],
        "signatures": [
          "204e60ca06af3c50dcc0d7c4d602c2828b794093617b5064a4b4ce2a6e2c74972550cb979bc8052dfe4e0c7192a12752e955286d6462739f61d2b36afb5984efbd"
        ]
      }
      ],
      "block_id": "0008b0d5e95cd667c50898a36d4b8bfb61a6e41c",
      "signing_key": "XGT56HuM2Esc4saSkvXSdQ7UTbTxeRvCnHikqeYiDNiKVesrVknX1",
      "transaction_ids": [
        "f6d5c0bf692467b5a1fb48814b9bb675874f5404"
      ]
  }
}
```
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
  "XTT_MAX_VOTABLE_ASSETS": 2,
  "XTT_UPVOTE_LOCKOUT": 43200,
  "XTT_EMIT_INDEFINITELY": 4294967295,
  "XTT_MAX_NOMINAL_VOTES_PER_DAY": 1000,
  "XTT_DEFAULT_VOTES_PER_REGEN_PERIOD": 50,
  "XTT_BALLAST_SUPPLY_PERCENT": 10,
  "XTT_MAX_ICO_TIERS": 10,
  "XGT_SYMBOL": {
    "nai": "@@000000021",
    "precision": 8
  },
  "XGT_SYMBOL_STR": "XGT",
  "XGT_INITIAL_VOTE_POWER_RATE": 40,
  "XGT_REDUCED_VOTE_POWER_RATE": 10,
  "XGT_100_PERCENT": 10000,
  "XGT_1_PERCENT": 100,
  "XGT_WALLET_RECOVERY_REQUEST_EXPIRATION_PERIOD": "86400000000",
  "XGT_ACTIVE_CHALLENGE_COOLDOWN": "86400000000",
  "XGT_ACTIVE_CHALLENGE_FEE": {
    "amount": "2000",
    "precision": 8,
    "nai": "@@000000021"
  },
  "XGT_ADDRESS_PREFIX": "XGT",
  "XGT_WALLET_NAME_LENGTH": 40,
  "XGT_APR_PERCENT_MULTIPLY_PER_BLOCK": "102035135585887",
  "XGT_APR_PERCENT_MULTIPLY_PER_HOUR": "119577151364285",
  "XGT_APR_PERCENT_MULTIPLY_PER_ROUND": "133921203762304",
  "XGT_APR_PERCENT_SHIFT_PER_BLOCK": 87,
  "XGT_APR_PERCENT_SHIFT_PER_HOUR": 77,
  "XGT_APR_PERCENT_SHIFT_PER_ROUND": 83,
  "XGT_BANDWIDTH_AVERAGE_WINDOW_SECONDS": 604800,
  "XGT_BANDWIDTH_PRECISION": 1000000,
  "XGT_BLOCKCHAIN_PRECISION": 100000000,
  "XGT_BLOCKCHAIN_PRECISION_DIGITS": 8,
  "XGT_BLOCKCHAIN_HARDFORK_VERSION": "0.0.0",
  "XGT_BLOCKCHAIN_VERSION": "0.0.0",
  "XGT_BLOCK_INTERVAL": 5,
  "XGT_BLOCKS_PER_DAY": 17280,
  "XGT_BLOCKS_PER_HOUR": 720,
  "XGT_BLOCKS_PER_YEAR": 6307200,
  "XGT_CHAIN_ID": "4e08b752aff5f66e1339cb8c0a8bca14c4ebb238655875db7dade86349091197",
  "XGT_COMMENT_TITLE_LIMIT": 256,
  "XGT_CONTENT_APR_PERCENT": 3875,
  "XGT_CONTENT_CONSTANT_HF0": "2000000000000",
  "XGT_CONTENT_CONSTANT_HF21": "2000000000000",
  "XGT_CREATE_WALLET_WITH_XGT_MODIFIER": 30,
  "XGT_CURATE_APR_PERCENT": 3875,
  "XGT_CUSTOM_OP_DATA_MAX_LENGTH": 8192,
  "XGT_CUSTOM_OP_ID_MAX_LENGTH": 32,
  "XGT_DOWNVOTE_POOL_PERCENT_HF21": 2500,
  "XGT_FEED_INTERVAL_BLOCKS": 720,
  "XGT_GENESIS_TIME": "2020-04-14T04:53:35",
  "XGT_HARDFORK_REQUIRED_WITNESSES": 17,
  "XGT_HF21_CONVERGENT_LINEAR_RECENT_CLAIMS": "503600561838938636",
  "XGT_INFLATION_NARROWING_PERIOD": 250000,
  "XGT_INFLATION_RATE_START_PERCENT": 978,
  "XGT_INFLATION_RATE_STOP_PERCENT": 95,
  "XGT_INIT_MINER_NAME": "XGT0000000000000000000000000000000000000000",
  "XGT_INIT_PUBLIC_KEY_STR": "XGT7dDoJbrmueAw431pPbjLDoRhqFCC5Xs5o6f1cZLepWEpkcy3Tc",
  "XGT_INIT_SUPPLY": "1872936875000000",
  "XGT_INIT_TIME": "1970-01-01T00:00:00",
  "XGT_IRREVERSIBLE_THRESHOLD": 7500,
  "XGT_MAX_WALLET_CREATION_FEE": 0,
  "XGT_MAX_WALLET_NAME_LENGTH": 16,
  "XGT_MAX_ASSET_WHITELIST_AUTHORITIES": 10,
  "XGT_MAX_AUTHORITY_MEMBERSHIP": 40,
  "XGT_MAX_BLOCK_SIZE": 655360000,
  "XGT_SOFT_MAX_BLOCK_SIZE": 2097152,
  "XGT_MAX_COMMENT_DEPTH": 65535,
  "XGT_MAX_COMMENT_DEPTH_PRE_HF17": 6,
  "XGT_MAX_FEED_AGE_SECONDS": 604800,
  "XGT_MAX_INSTANCE_ID": "281474976710655",
  "XGT_MAX_MEMO_SIZE": 2048,
  "XGT_MAX_WITNESSES": 10,
  "XGT_MAX_VOTED_WITNESSES": 0,
  "XGT_MAX_MINER_WITNESSES": 10,
  "XGT_MAX_PERMLINK_LENGTH": 256,
  "XGT_MAX_RATION_DECAY_RATE": 1000000,
  "XGT_MAX_RESERVE_RATIO": 20000,
  "XGT_MAX_SATOSHIS": "4611686018427387903",
  "XGT_MAX_SHARE_SUPPLY": "1000000000000000",
  "XGT_MAX_SIG_CHECK_DEPTH": 2,
  "XGT_MAX_SIG_CHECK_WALLETS": 125,
  "XGT_MAX_TIME_UNTIL_EXPIRATION": 3600,
  "XGT_MAX_TRANSACTION_SIZE": 65536,
  "XGT_MAX_UNDO_HISTORY": 151200,
  "XGT_MAX_URL_LENGTH": 127,
  "XGT_MAX_VOTE_CHANGES": 5,
  "XGT_MAX_WITNESS_URL_LENGTH": 2048,
  "XGT_MIN_WALLET_CREATION_FEE": 0,
  "XGT_MIN_WALLET_NAME_LENGTH": 3,
  "XGT_MIN_BLOCK_SIZE_LIMIT": 65536,
  "XGT_MIN_BLOCK_SIZE": 115,
  "XGT_MIN_PERMLINK_LENGTH": 0,
  "XGT_MIN_REPLY_INTERVAL": 20000000,
  "XGT_MIN_REPLY_INTERVAL_HF20": 3000000,
  "XGT_MIN_ROOT_COMMENT_INTERVAL": 300000000,
  "XGT_MIN_COMMENT_EDIT_INTERVAL": 3000000,
  "XGT_MIN_VOTE_INTERVAL_SEC": 3,
  "XGT_MINER_WALLET": "XGT0000000000000000000000000000000000000001",
  "XGT_MINER_PAY_PERCENT": 100,
  "XGT_MIN_FEEDS": 3,
  "XGT_MINING_BLOCKS_PER_SECOND": "0.25000000000000000",
  "XGT_MINING_BTC_BLOCKS_PER_SECOND": "0.00166666670702398",
  "XGT_MINING_RELATIVE_SPEED": "150.00000000000000000",
  "XGT_STARTING_OFFSET": 0,
  "XGT_MINING_REWARD": {
    "amount": "4166166",
    "precision": 8,
    "nai": "@@000000021"
  },
  "XGT_MIN_POW_REWARD": {
    "amount": "4166166",
    "precision": 8,
    "nai": "@@000000021"
  },
  "XGT_MINING_ADJUSTMENT_MAX_FACTOR": "4.00000000000000000",
  "XGT_MINING_REWARD_HALVING_INTERVAL": 30150000,
  "XGT_MINING_RECALC_EVERY_N_BLOCKS": 302400,
  "XGT_MINING_TARGET_START": "000000ffff000000000000000000000000000000000000000000000000000000",
  "XGT_MINING_TARGET_MAX": "00000ffff0000000000000000000000000000000000000000000000000000000",
  "XGT_MIN_TRANSACTION_EXPIRATION_LIMIT": 25,
  "XGT_MIN_TRANSACTION_SIZE_LIMIT": 1024,
  "XGT_MIN_UNDO_HISTORY": 10,
  "XGT_NULL_WALLET": "XGT0000000000000000000000000000000000000002",
  "XGT_RECOVERY_AUTH_HISTORY_TRACKING_START_BLOCK_NUM": 3186477,
  "XGT_RECOVERY_AUTH_RECOVERY_PERIOD": "2592000000000",
  "XGT_RECOVERY_CHALLENGE_COOLDOWN": "86400000000",
  "XGT_RECOVERY_CHALLENGE_FEE": {
    "amount": "30000",
    "precision": 8,
    "nai": "@@000000021"
  },
  "XGT_RECOVERY_UPDATE_LIMIT": 3600000000,
  "XGT_POST_AVERAGE_WINDOW": 86400,
  "XGT_POST_WEIGHT_CONSTANT": 1600000000,
  "XGT_POW_APR_PERCENT": 750,
  "XGT_PRODUCER_APR_PERCENT": 750,
  "XGT_SECONDS_PER_YEAR": 31536000,
  "XGT_REVERSE_AUCTION_WINDOW_SECONDS": 300,
  "XGT_ROOT_POST_PARENT": "",
  "XGT_SOFT_MAX_COMMENT_DEPTH": 255,
  "XGT_START_MINER_VOTING_BLOCK": 518400,
  "XGT_TEMP_WALLET": "XGT0000000000000000000000000000000000000003",
  "XGT_UPVOTE_LOCKOUT_SECONDS": 43200,
  "XGT_VOTE_DUST_THRESHOLD": 50000000,
  "XGT_VOTING_ENERGY_REGENERATION_SECONDS": 86400,
  "XGT_VIRTUAL_SCHEDULE_LAP_LENGTH": "18446744073709551615",
  "XGT_VIRTUAL_SCHEDULE_LAP_LENGTH2": "340282366920938463463374607431768211455",
  "XGT_VOTES_PER_PERIOD_XTT_HF": 50,
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
  "XGT_DECAY_BACKSTOP_PERCENT": 9000,
  "XGT_BLOCK_GENERATION_POSTPONED_TX_LIMIT": 5,
  "XGT_PENDING_TRANSACTION_EXECUTION_LIMIT": 200000,
  "XGT_TREASURY_WALLET": "XGT0000000000000000000000000000000000000004",
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
  "blockchain_version": "0.0.0",
  "xgt_revision": "0583f0cb28b05b547e7a57acc4b82959fb78da9b",
  "fc_revision": "0583f0cb28b05b547e7a57acc4b82959fb78da9b",
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
  "head_block_number": 1341626,
  "head_block_id": "001478ba34854673ffc07e04e5a715f8b21bfb51",
  "time": "2021-07-06T23:09:18",
  "current_witness": "XGT8JEbh79M3xbSJa9kTxhmpWKZEuKhzFz5PFnXNV9u",
  "mining_target": "0000000a31c4a7d274058c7e8a9c6d0ad025f08df1e5861e9c8ad4c410731e46",
  "total_pow": 1340687,
  "num_pow_witnesses": 1340688,
  "virtual_supply": {
    "amount": "1872936875000000",
    "precision": 8,
    "nai": "@@000000021"
  },
  "current_supply": {
    "amount": "1872936875000000",
    "precision": 8,
    "nai": "@@000000021"
  },
  "confidential_supply": {
    "amount": "0",
    "precision": 8,
    "nai": "@@000000021"
  },
  "maximum_block_size": 655360000,
  "required_actions_partition_percent": 0,
  "current_aslot": 0,
  "recent_slots_filled": "340282366920938463463374607431768211455",
  "participation_count": 128,
  "last_irreversible_block_num": 1341616,
  "target_votes_per_period": 40,
  "delegation_return_period": 86400,
  "reverse_auction_seconds": 300,
  "next_maintenance_time": "2020-04-14T04:53:35",
  "last_budget_time": "2020-04-14T04:53:35",
  "downvote_pool_percent": 0,
  "xtt_creation_fee": {
    "amount": "1000",
    "precision": 8,
    "nai": "@@000000021"
  }
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
    "2020-04-14T04:53:35"
  ],
  "last_hardfork": 0,
  "current_hardfork_version": "0.0.0",
  "next_hardfork": "0.0.0",
  "next_hardfork_time": "1970-01-01T00:00:00"
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
  start: 0,
  limit: 3,
  order: "by_name"
}
```
#### Example JSON Response
```javascript
{
  "witnesses": [
    {
      "id": 0,
      "owner": "XGT0000000000000000000000000000000000000000",
      "created": "1970-01-01T00:00:00",
      "url": "",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 93538,
      "signing_key": "XGT7dDoJbrmueAw431pPbjLDoRhqFCC5Xs5o6f1cZLepWEpkcy3Tc",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 165,
      "owner": "XGTBTR3cWLJVythoqRynqRNtgiDRe68v17KKJbbpLuv",
      "created": "2021-06-28T01:14:11",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 812235,
      "signing_key": "XGT5KeDHoGs3jfhLSRMDoMvWgRDXbMsgmVCBJHeye6pXpEawiokaL",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 155,
      "owner": "XGT7vdjEsVeDz5tifitKBPm3rcCTExLp1BtwvD3NvJr",
      "created": "2021-06-20T05:00:28",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT8NEAGHRe83iAurBdK687U1fD9wYqhBs6TWaqr3CPpMDczzf4T7",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 168,
      "owner": "XGTCmh8sAGbhMttykSSQAruvD76gvnMb1E6PT49YVin",
      "created": "2021-07-01T13:31:32",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT8GLzJJcng2mSqsdRyRoijfumUmAj3dskFmoDmWh67fm6yeaVw2",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 8,
      "owner": "XGTC4jWpZYwPM57daCDSR8bJdSzUCt7t1of5bj84omQ",
      "created": "2021-06-07T21:46:13",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT854uosvkV8AiH5uqx2mBcA9VucdyuCfgWPe31xZJkfygxunqpu",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 64,
      "owner": "XGTXSJrfvybryBgnWHVmQEtjKUbDoBSP2BVwQUXBueP",
      "created": "2021-06-09T16:08:18",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT5VJpvtRveztzvRSZ7UWV8VjBBL4iw3sZTCGUfXRbJD3mi2HJhv",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 174,
      "owner": "XGTrZmdKpaXFkV1iQqZ9hmy8NhxNWaEU2KQgzYpZBDc",
      "created": "2021-07-06T15:08:41",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT5NS9jjaDhWETfXsmYDg2JnQa8vM8SJF5x7NrqhMiZXy7LgZgFL",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 115,
      "owner": "XGTBuSqkKhb1PQioVzArLnUBXAnQCbqD2ew7KuzrVb1",
      "created": "2021-06-15T17:27:09",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT6PZpeFfxBFe6U2vjEYZuTkDvoj4KAHnaCuR5RvKLsEwqGnaQq9",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 169,
      "owner": "XGTAgcGtv2ntgw4hoXTWz93RMAomo4EK3EAyeiB6LEY",
      "created": "2021-07-02T03:14:40",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 962517,
      "signing_key": "XGT5dqhtZcTW3DGCo8SAc2sE572ypSsUGGrvW9jUki2o18pyPZnFq",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 104,
      "owner": "XGTBi9M4wHTwmFpuPHzDQHpbiL7huW113JRjnmqZJJR",
      "created": "2021-06-15T07:19:15",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT4v61HgWYsuuHurnwz4QpZFijbVA7hSg5vLbmkT8xFRkwt5NGrD",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 89,
      "owner": "XGT4uFLr6eJNavX97G4skac8uPQ65t3f3c15YA8v2iA",
      "created": "2021-06-14T09:17:30",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 379986,
      "signing_key": "XGT5JCw9cM8P7mQvqM1MTtEUgR3s4TMvp7FKBCBcwc5JFXF2X1B3T",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 163,
      "owner": "XGTEzp6fe8XsRNq8DfW5vcgQ5PJuiUeg3c94aonGLXe",
      "created": "2021-06-25T23:44:18",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT85tW5jLzYtF9Ug4sDkEymu3wY34edbdpP1c6fAne2ymvpuHMcs",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 9,
      "owner": "XGT8ZbbkW8xo58x4ZXBCZyK1AnNMicFv3x7prvofY8S",
      "created": "2021-06-07T21:56:32",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT6rhh5Yh6wVZN2nVCqXCY4vc3d8PxRSHdxcFvVMncow6Js82yrF",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 66,
      "owner": "XGT2bHiA5AF6vuJTSW9L5m91HDUzeLvU4ERmgLwTXDZ",
      "created": "2021-06-09T16:08:39",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT7NvsnX4HTgMzwhgXrM98EAsghjJN1NMtGVX7BnC1fnp2BmAM5U",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 156,
      "owner": "XGT9H9eggTTpKDRAsT9LmqZLg9AijC375DVqjDRNiGf",
      "created": "2021-06-21T06:13:53",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT5WuhSne3PrXqwwWDC9gLDSvaPtTceWU9zdppw6Ggz46WaDWUDr",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 83,
      "owner": "XGT3vuT1SegDyih6T5jmT3WJ9YTPYRnY5GE4DwfgD96",
      "created": "2021-06-13T15:16:50",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 493456,
      "signing_key": "XGT5agvZ3gg7HYQJJ6oP2tAeQkNwSSzSr6TsKBcGd7V4kSXakV8jC",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 149,
      "owner": "XGT6TnBGQxPT6Vg3AFn9fRgcFdyvv4nZ5ZqAKJhGGog",
      "created": "2021-06-18T02:51:50",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT8YFrw1LEheqYYjDgK5BUtoTdm4eVoinobXgZpfYf2vepinE9cu",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 12,
      "owner": "XGT3vt1JsCNdrfQh8kN8RZCwCsLsRwGG5fGzPdsuppn",
      "created": "2021-06-07T22:20:02",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT7m3pPNzN7rJRfAbwuBJoKuoHY1MeUWSnGvqkowkX3nJrPAq5xL",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 139,
      "owner": "XGT6rcrHLbiVN7UWwc6EE1U8QyqAp9iv5pnbNhBGbL6",
      "created": "2021-06-17T15:50:33",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT7sY8QTXjQeFNT9q5ttGMrWjek8A2ftzdKev8ajq7VrCrpnFFUn",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 75,
      "owner": "XGT2jhfspb3HV3uct9FCT9zDYW7oUyTf6AAdC5ECqnE",
      "created": "2021-06-11T16:11:23",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT5GdZYCtPuCruTtJYLqm6ewVCou2bFjcQdAGExXdZr5WM9gPAwc",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 56,
      "owner": "XGTGHqMjp6kqQcb6h6sXwUqU4ZeaRGby6Rrd4VwwLes",
      "created": "2021-06-08T08:19:59",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT8Hjbs4vr3aK9yB8ymLhRhciv7Q9Nc1PBaGHVhQpFtR4PeZhFfL",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 39,
      "owner": "XGTGM18acHjFPVKsTkYCmRPhmtBvdKH86bEBz1MbvJb",
      "created": "2021-06-08T06:34:29",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT7FomwHBebQSRb6LLiqDkyrF6mHgVANuzeMXqHAEe46YUwHj1Kq",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 29,
      "owner": "XGT5QKJzUtS4nGPJLD1jmJmxb7wLj6uE6putfUzoScY",
      "created": "2021-06-08T01:44:46",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 510434,
      "signing_key": "XGT71avwWsd1Uyqs4uQ31rVz7Pka6JMnjQVjRxPjmYe6zmwkDrrsq",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 150,
      "owner": "XGT6dSQDvF7uMmcF66Rc1nVFNg2qhDdU7VQDafQGvUu",
      "created": "2021-06-18T05:40:30",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 1340690,
      "signing_key": "XGT55mionaVumbtf849GbramAKXZ5tnJMpX1qewptjLSW58JUkHP8",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 154,
      "owner": "XGTBqPasoLtPe1SjDeCEnhx1RnZWiPae8W2JjaNKxgE",
      "created": "2021-06-18T23:12:37",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT83kBTpbtAPLQoRtuYxoq8t9puDA6Hzjt7rHCjRV6976FYiDDhP",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 98,
      "owner": "XGTAcg5xfmrNijzvrVWn3L2jTMrAZL3h8WUXG3kh53Z",
      "created": "2021-06-14T23:08:09",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT5zQPqt4TokKyPxvTccp8MmSMiKz2gGDxyjBDyMmXwE3spi8s8k",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 4,
      "owner": "XGTH5jncbEmBvVBtgDJJHFzvd4nGKtQ18ooiMgA9Ck8",
      "created": "2021-06-07T21:30:07",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT7b8UEa1R9GzLxdMTNsWR25fjoZv4nqjcuu6n4Xj1qqH1aYqY9W",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 2,
      "owner": "XGT5nbpvvwDUvhEY3FKKW3aV7g5kQRbp92GDBPsJvwC",
      "created": "2021-06-07T21:29:00",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT65bVJbm8M56JvaB9F87Y9FTqCgPvmQ9NVAxxUnLeyQc9s74puX",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 41,
      "owner": "XGTFazBN9rLM5rK6Doa9T3HHdVSFod7x9Kk6E3HhCgZ",
      "created": "2021-06-08T06:58:54",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT8EbiFbE4p9ZuR3EsN2GmXQJmgQNnAnhfST2PuTMZJpx1DjBUX2",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 81,
      "owner": "XGT7Bo9owdAv5drGa1Kp3562VsNz2g669U13XUhymev",
      "created": "2021-06-13T06:19:41",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT5VFihBQwdeyoM3obQ6hhfqtU6Ceove5M3R9Cu7qWRNxHfHEdfJ",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 153,
      "owner": "XGTC8HErX74o9AHLEf7BaGZoZDNwpGjx9VSCcPUfcTv",
      "created": "2021-06-18T17:44:16",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT5kKXa4Jif3GfRfAN3WrxZBQ6Uwy2eXvL7QUebdKr7doP9Qi3au",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 152,
      "owner": "XGT5R4KMp3Vxf4K46CR1Y5CsYLgULGXF9upoHCV7uJj",
      "created": "2021-06-18T17:28:51",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT5H3x1rLiq9XHSVgw3f7KwCtzpnWBk7ceEYKmmQjNyRAxRjeGLx",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 37,
      "owner": "XGTDcKm1qFrXHdS9WnYzJ8ZfvKSsrp42A7JezzsnJ7g",
      "created": "2021-06-08T05:58:46",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT751cWuQsHDsBSeiqVPD1EiR1R2b1QYAYnAUdSb8SLiYM2YuQxP",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 63,
      "owner": "XGTAK7uQpKA4u2B3dQuUH2DwEmPaHU7WBCBN6N4FutA",
      "created": "2021-06-09T04:47:16",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT7MTq73gHzQZgeaEZS6ZSkFtJ7HDWfTTeogjs7Sdcs39XqT8r5F",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 101,
      "owner": "XGTCoTeMrGvGSsrsNk9sTJfLHvHGTVDvBEGcg29k3vF",
      "created": "2021-06-15T06:12:44",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 382118,
      "signing_key": "XGT7M5hAa4tbks89Fp6Jhu5U18LnBEk2eG1poeR8vu2xqFjkmJ9p1",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 107,
      "owner": "XGT6zQJQTac3PfJdv24ez8DdG2RxX88pBRKMxRtRYy3",
      "created": "2021-06-15T11:03:30",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 548586,
      "signing_key": "XGT5pRCSJ14aHM7bYNtoyvJiJ787vPbVbF9CCQYYBABtnXXfPfqRn",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 148,
      "owner": "XGT3jFXKk4RNFwAd2PRaC2D9t16higNNC9RjVvxZCjw",
      "created": "2021-06-18T01:50:28",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT7yiVrg16hNFRWgU3RTEGXPno7WYJCtYvwFiA2uqGq1HHNx3Usr",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 61,
      "owner": "XGTEEHrvP5cXpg69bGYQGJSd9Wfz4PuhCF1xaZLsFos",
      "created": "2021-06-09T01:14:29",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT8d2GbNhqg4aNJbnGFB2gzafhsr7zq8UpgDumiCFYn9STp3h8z5",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 125,
      "owner": "XGTDCC8bpuq6L6GLQN4w3KgzusXufeoPCfhKES37ZAd",
      "created": "2021-06-16T16:44:51",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT4wxkBfFexU2HpiRFkJi4QfJP6s4nTyTZbMz9pFPVBUP6RbuBwy",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 116,
      "owner": "XGTEev2AAkuNhR4Hxcck9khkmADQWoibDSef9y4biMe",
      "created": "2021-06-15T20:23:38",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT6WGEgLPB94qMnK2mobZgPArW5wKas5HpL39QHV1tMCnGaVrJfu",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 167,
      "owner": "XGT5EmFknGeZzwyLPQpV5VVGBa5E64ZnDT7FY7qhQUn",
      "created": "2021-06-30T19:51:37",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT6mBFdmkeG1zXJWgoDSEnZ23p3GhMcHUJYWjoiowMLYyd3m2e22",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 55,
      "owner": "XGT9eyLQW8u8fetnqfN2GuSQRG1ZQRm3DawYDFGePrv",
      "created": "2021-06-08T07:49:32",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT8RPLkpZWdFocceXPoQj1RZsov1eevbPV85St8E76krZzVHAkaT",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 85,
      "owner": "XGTEk87STghgHXCNMmXvzcoU7nvPfU3zDuCntrewZis",
      "created": "2021-06-14T05:20:59",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 711698,
      "signing_key": "XGT7TCHNr28wH53X3SPV8C7WKpQDbjEWEkwc9EUPZAE3RBDqg9ah7",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 11,
      "owner": "XGTDkkLogBPdtB6i2ZUvBaz4NgXVgcRJF1Jgvsny55E",
      "created": "2021-06-07T22:18:53",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 504980,
      "signing_key": "XGT5tZWPRGkUyfiy68KK9kRym2ZxAqzNM8a1ZdxvESUWjE9nq8NuF",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 103,
      "owner": "XGTCQjDWREvCJyyijftf6ZqpsEAfWb96FoNacZhjczj",
      "created": "2021-06-15T06:32:04",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 459372,
      "signing_key": "XGT5SFfU1CA3kAqjKZviVSXdszRBgr7tdvjXmnPD8ELY3LauyaqjU",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 34,
      "owner": "XGTFJbSijB2WyZFw6vurNScPkUvQn7nqFsEqTn53uSd",
      "created": "2021-06-08T05:08:41",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT5VYpMfUVdzxpYuQPE17dTKiSpwX7QiNm6EqoZCcN7FtUE4i1LM",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 166,
      "owner": "XGT8JEbh79M3xbSJa9kTxhmpWKZEuKhzFz5PFnXNV9u",
      "created": "2021-06-30T13:57:15",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 1340718,
      "signing_key": "XGT5C96My82amdrtGvj58tAq76yDjmmWjNCA3xdqyDfdTRBxZyF6i",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 143,
      "owner": "XGTEz1rG1BE1r8Hn6iAMpmUoXE132UcHG4Agkqqg2zT",
      "created": "2021-06-17T21:09:32",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 469568,
      "signing_key": "XGT8UmqMRZ9cfZMMNTjNm3EJNkMLkfTgNZFYo2bRfmMQNCrdYjvMo",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 16,
      "owner": "XGT7Yw6iMUMfbGBeHtgzPTyFBN72x3gWGCjvc1nuXH5",
      "created": "2021-06-07T22:39:23",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT7KxC5na4LjVSA38idSVZqnR7Jyf3VKJKQBJGVhJLFPAhFPeFhM",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 48,
      "owner": "XGT8CXwcz4HubwW3RYoqh5qZffJF5tJ5GSM4a6QwJsV",
      "created": "2021-06-08T07:29:15",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT5v2ByuM6pykLM6PvzGtpnRFCXtvDdtpv9Ha5czguHoCk3R3ggb",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 5,
      "owner": "XGT8CW6Pk3wDAwwEGbMZhXo2RvfztV9gGzT2ByN78DG",
      "created": "2021-06-07T21:34:49",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT4wGcWdD8RZEQdu1qcGYm5p9UoR4GeLbzMSGXZudW7LPTvZSB3s",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 108,
      "owner": "XGTGveyhdWrN1yxbgum92cii1CHmYzi7Hx2dYae7fH9",
      "created": "2021-06-15T11:07:02",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT8RMokwbKV3555HoZX4tf5ZCkifAnWi52zpd2TJSnGVczD6VMoq",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 157,
      "owner": "XGTAWdNS2uazGjm2vAbHjTrBB29mk2YrJBCDwSnsQ4t",
      "created": "2021-06-22T22:15:56",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 1340646,
      "signing_key": "XGT5TFpAEBks9qrsVh9hFLJf6A3YFjTf1prUgaCfeApSXFZTB1CFa",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 24,
      "owner": "XGT8RnxMN5EX1z9vjmtu4heQToS2q7jKJuLJAMVqfCu",
      "created": "2021-06-07T23:17:34",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT8h3oBmSQFgxESC87foDmESbYFVwLKmAmgZxHtR4LALPCUtwfsx",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 62,
      "owner": "XGTDHeEmdowDKb2a82WanBmuQetzTPzbJvrtZuqNZs5",
      "created": "2021-06-09T01:45:57",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT62ctdUozdD4ziJCpYqP5FJwPWEmQzT1cLPcYvMs1EDSRNcFnSG",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 7,
      "owner": "XGTFaH4L4UWvLhnD2NqL1ZexBFbtwHnUKLPnhwReVU8",
      "created": "2021-06-07T21:40:27",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT7GEoGpgVjDtnpaRuBicg59HtAruHC8GFqyHfbNARshUd3m6ozK",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 44,
      "owner": "XGTA7KhMnJXsYzRqqpJRb9zS2akz6koTKyq38n7nkWz",
      "created": "2021-06-08T07:20:37",
      "url": "http://witness-category/my-witness",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT83T4B5vezp5b4y4pYfScdpL9MoeGsGXDrSZ7X4H98igXxm3Ai6",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 137,
      "owner": "XGTAGB8usZFppemNHZiEovYH6gbimmV3LijaunmmLCm",
      "created": "2021-06-17T11:57:46",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 819821,
      "signing_key": "XGT7eUERmbPvsUSEPyj5AcoKVHEBtejA8yhdENJ4TGnPRXh6uiPXY",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 82,
      "owner": "XGT4bahdxakZEvFP6WkRPAB1i7nvonNwMFqCAuGCEsL",
      "created": "2021-06-13T13:52:46",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 468319,
      "signing_key": "XGT5iLmwogUm52NL4SzCmBWRSqqWBD1SdvzJAQ93FtkZnq4cZnwEj",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 134,
      "owner": "XGTH6aobewk3vBSqhGMMroszhmKFkJ5qMKWgSXhbe4e",
      "created": "2021-06-17T07:44:32",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT8fDuRudA7RXpmcSVADUQqsaLBLtmp7nep1q4DwEjcLxkoRis4G",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 80,
      "owner": "XGTGsTFzDyPZ4RVdff6NG5Prf2Xx2NGoMRYWy7ScF2x",
      "created": "2021-06-13T05:47:05",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 683955,
      "signing_key": "XGT73MUAGRXDQbWJW6wCic2izm3u5B2dNZYYRQQDbnYZQGAe5gTs6",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 18,
      "owner": "XGTE6QyxE5fwfcCYNL6hdT7LwsKDZtjgMSZ6mYsksEx",
      "created": "2021-06-07T22:47:52",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT8BgCaM7DXhdZfxiW3TfGW1adyt8ZiGLQxqozwWYEKAzX5h1FjH",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 22,
      "owner": "XGTDyNCcpwZ1GcVwvdJ5CH4Mg1NDkvfzN4ZMQ4jZg1T",
      "created": "2021-06-07T23:06:30",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 7979,
      "signing_key": "XGT51KqT1syZd8PRwSgctzzFA36e4vEuzpkkCdM92jiAhUNDgvqV9",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 161,
      "owner": "XGTGM4ZSF4RhMvtLFLzDQvwihP9nwEz8NrqFyRqRebH",
      "created": "2021-06-25T19:56:10",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT8mAJsc78n21FCZA32z4KMSskc8Z7hddS8ag1YzWJD8kJxvTEMh",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 84,
      "owner": "XGT95X6s2PtSUjVSfLsrTEusrqmHQBXANy66mnc9EpZ",
      "created": "2021-06-14T04:02:15",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 555329,
      "signing_key": "XGT7yzyTr6gTBAs4fzDDC7TtPbAsYMG6iw82ACttt6GyTMRfFQfnw",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 97,
      "owner": "XGTDZatHRi3cCoebySHz6iV8p4DoWQhjQQMJSJ9kwTD",
      "created": "2021-06-14T20:45:27",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 1329609,
      "signing_key": "XGT7MT4mHCEjJGongH65zmTeM4Vsp9WnbJ9MQ3WraqD7XTnPZEw6H",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 1,
      "owner": "XGTFPni4anwm5sUCULerBG86f2JhYYZVQWBH5mNAahA",
      "created": "2021-06-07T21:26:43",
      "url": "http://witness-category/my-witness",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 239808,
      "signing_key": "XGT7kCfG7NctddZbQeoYxF6vimfmvGwi9zLzuDgS1J1NwCYQeMYa2",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 122,
      "owner": "XGT6Wmv5vGXbLkAHtrnu6LfairtZuXYkQb3cV6h65XY",
      "created": "2021-06-16T14:59:18",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 483002,
      "signing_key": "XGT68FQi1N5q3qeySuQSJZLoPwxxxzVnyNb7KSUWqoTcxAob7dWUy",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 57,
      "owner": "XGT8ZvVEhahVK4fFLXtk5oEQnS1FSNHHQgkwBcDerZv",
      "created": "2021-06-08T09:29:38",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT7ZUrm7HCJtcfw4Pn3bEznBo8z6SnVESYzop7u6keEzmKUZYYWB",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 114,
      "owner": "XGT36yrBZ5PbXV8BiZR3Cu25K6oT2TpSQyEeUN16C3d",
      "created": "2021-06-15T16:02:14",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT6259eHBiZzEj4wmyNfcFkikD89WRu2mSf5rMNjQJgPY7gXEPVP",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 160,
      "owner": "XGT64EytQ9MRzKti5EkdvwdX5a9vmButRGBbrsqA6he",
      "created": "2021-06-23T22:39:39",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT6rTEgrD54jrMmhbyJG8oA9pWBdc2GdEippPbKKwd5YULAxJ4XG",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 28,
      "owner": "XGTHcsayM9TRs2Xpcpd7BmXRfE3rpJiHRRFvqW3Cz6d",
      "created": "2021-06-08T01:12:34",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 587137,
      "signing_key": "XGT7C3yd4uZqbEqz6vsG9iF4ncHWZGjNPXQnordnprkdX11XRVeqS",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 100,
      "owner": "XGT7r8PnSkmow33DemPGx26JHHQuiwQpRZGNdgBNQi7",
      "created": "2021-06-15T06:03:09",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 479777,
      "signing_key": "XGT8jyAiWXvnxJfPdYkE176C1mzne7ZTqAa2Hsp6ZNJhi4yG9cq8Y",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 19,
      "owner": "XGTH8DDftgzsxf1ag7Pz4nqEGXecBAGbRycmgzKmSgJ",
      "created": "2021-06-07T22:50:56",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT8bQ3uaVenR1PRiaWDPEacxkxWnoRUVzjo57i956hfrBm7pn5HN",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 53,
      "owner": "XGT3DiQVdjMeNbMQk6EnnLXwKQXkZnFjS1asKq5zzL8",
      "created": "2021-06-08T07:31:17",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 1337125,
      "signing_key": "XGT5tnT1MbgAfgYKZBKJB2pzEdybqnGiqAvLSFvJjw6ubvQZSfiFZ",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 92,
      "owner": "XGTB5jjv7H2jSZZcvT9B8eWCAQfHpjd4S3PrS4YCzjy",
      "created": "2021-06-14T16:07:56",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT6yGpicoR7ePd2zW4mmSesB4dpRbyfBM68SLaNLY1j3FKwC3KxW",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 33,
      "owner": "XGT4vpiys9doDjNs7VkQo9R3tzeHtBPESJWfTS9wf7L",
      "created": "2021-06-08T04:46:38",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 1340691,
      "signing_key": "XGT8Sc7A6FRDVpATV3e8UczDdNbTfE7nDFhf3dFgTdpDiMXPxbu3M",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 135,
      "owner": "XGT7RcPWgPxns6cATdiyobhLcRn2G4RWSbxKjSxgy95",
      "created": "2021-06-17T08:29:54",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 1308870,
      "signing_key": "XGT8axjvBzbX9REKw5qHdEYGXXSJxGoxPnFsYtT7B2MntJoraYBaW",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 127,
      "owner": "XGTFfrJjYqnmsMJAvNW9fEwQBAeQ6FUfSkr4vPKXoZr",
      "created": "2021-06-16T17:02:44",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 513296,
      "signing_key": "XGT8icDmD63rPh52syH97PDbxbpJhhm8quDJLe3hnq8xbqJN2HzYR",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 35,
      "owner": "XGTEKuKqWGS2yLrrLZwNYkAHkbbC5GzQSrzeyfcxoLc",
      "created": "2021-06-08T05:14:25",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 495707,
      "signing_key": "XGT6UcVQwtSf9kWQWFZ5MV2oCdntgwF3dintvZ9JAMWSEk3sB1MPL",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 151,
      "owner": "XGT7sDmwy14meJpdoAK5iXnZsDz7F6XKSsNvuTxFE3z",
      "created": "2021-06-18T16:08:07",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 644768,
      "signing_key": "XGT7FtCXD86i3ULTE6qWAi14feXZZpgHagWM3EbL9z3Z9VKiaPH3L",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 120,
      "owner": "XGT2rt23Je3YCfxkAzVjVT8c8V7wrC8uTA28u5xFKub",
      "created": "2021-06-16T00:34:53",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 606212,
      "signing_key": "XGT8ddFc3FisKKnGxyJgcKtTyd4o17PF6T8RJMmuZRsnMCd6Ar3Sw",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 144,
      "owner": "XGT4h2wpXLY4UxuTkU2iZaknnfo387YeTuCk233ky3z",
      "created": "2021-06-17T21:48:38",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 485940,
      "signing_key": "XGT6AgHdm62qN7VZHB1gn6NMupeYG5SSuKgbuPLMr5jv3g62gAQG8",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 78,
      "owner": "XGTGLXqgd6UmY6WzJ1kWwi2ebgVQQbonTxL3HNXzKVd",
      "created": "2021-06-13T05:43:35",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT8UBFEHBXKVXjrhwFK6ScEfkXCZJK9iYrCHt6sZyvQro6sASfCq",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 74,
      "owner": "XGTDMmRMPHchj37Ch9s5EFwmLinTupnjUB2de5WxxDV",
      "created": "2021-06-11T15:53:57",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT7MtN8Rbyi1eajRTNQVZTYn4oWn4vnnTBwgAD6RPuwS6XWk7V2G",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 129,
      "owner": "XGTEuj5wZeZzcCdeCoXdNEetsb73wGX2Uq7uLtsXQKf",
      "created": "2021-06-16T23:13:36",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 1340639,
      "signing_key": "XGT82Gm6dzPSKM51Y8S2pXUmFqsKn5dVbZcREkUX1iM6sMTnZriZq",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 138,
      "owner": "XGT76iGsFSnQQ2uUPwey7Dz5r94aBZFnVRogkkF3f1S",
      "created": "2021-06-17T12:48:51",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 601973,
      "signing_key": "XGT58kX5Lm1GJmXR3eQnyJTyAe64gvt1keTRBbo3LYeNSQEp2Mmb1",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 109,
      "owner": "XGTGvpMqyd5GNA2cZpndWYKgvABwfAACVWN9roSvNWv",
      "created": "2021-06-15T12:27:54",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT7regEctNxfmRg6GjYYevHKPQFSzYfe2NxmeRVmjKCLYnb9vNLu",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 118,
      "owner": "XGT2zieEsiFWCxGM3n8QNXo5HrhrgAfDVyxCjfc78Uj",
      "created": "2021-06-15T21:27:22",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 607343,
      "signing_key": "XGT5ffVs13jG5aycuthKHVjYKQc9GWE28eQ6ZaGcrFnwvGKCiRqnb",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 38,
      "owner": "XGTEuY8PS61orxrxARwwDqntRDoCn1WxW1RNmxHDBsq",
      "created": "2021-06-08T06:04:18",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT72UZikvTLJxaLtsb7gpfhu4bSMLRTavYZRbvaPDe99QhSuo4Lf",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 111,
      "owner": "XGT2KWs9XGDRvv5GCDh1piv3JbPZuN1WWAPtKVqLAdt",
      "created": "2021-06-15T12:42:08",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT6gLfM4RSKz3vLdchrWpEQB7NXPRgXT14JEAhvJM6JuKAPQFoA6",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 90,
      "owner": "XGT7Dz34yUW7TsBUzDRrcpxJXSejPHZQWjF4sBxoPxa",
      "created": "2021-06-14T14:52:31",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT6gStUQ7LQcQFLZNtU18EXgV5MqZ2Tr4wnkRHkCUgKvPNoTbgPB",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 113,
      "owner": "XGTD87g6gUghdMMfNg3rtuEPxjTvPQAXX3fo31Zfau2",
      "created": "2021-06-15T13:26:32",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 701914,
      "signing_key": "XGT4z8WnYNurt2JpYkUKTumDPKpaepws6MAwkrVwbKo5by9s5Wn7r",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 119,
      "owner": "XGT52idQKLaWE9hdTDrjXdYNLLc3mBwGXP4eG9ekfGa",
      "created": "2021-06-15T23:47:24",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT8KCchMegPqMAs3WxumyKbQLZ2U9FwDmW5TiT8k7bT3EkZFsfhh",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 110,
      "owner": "XGT6QFaQGxwzQRxuZGvtX7qucwycXmJtXpa5EbWLfmA",
      "created": "2021-06-15T12:34:14",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT7YTfsmBCtY4jxQSURfTr11PxwfnrVcgf4fHkWY6TgCGL9iWUie",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 15,
      "owner": "XGTGYS6fFkS6gBG8VfT7gETtkRhEzbDXXzJDNQyrRFy",
      "created": "2021-06-07T22:36:40",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 887371,
      "signing_key": "XGT5JM1dHS93s58MsUmnwG32TAgduNoEMx36YbxnazXAMpuUCY24H",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 6,
      "owner": "XGTH9SiLMzsWFYR1bP9NkJLWb3TiMzptYCVpvLuWGPb",
      "created": "2021-06-07T21:37:08",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 19012,
      "signing_key": "XGT7omA6LKxAUF25PLHiEujGAP7mVACHXRPTNd8iof8xoNuys28sG",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 159,
      "owner": "XGT22C4t3EojFeEd5B9JXGp8RbuizAPdYM6ZMiyyZ6a",
      "created": "2021-06-23T19:50:31",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 579475,
      "signing_key": "XGT7A5822rbS5aAh1rvChdHYuciqy7MCnSL3DPchVfEUnCuKxpGKu",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 3,
      "owner": "XGTGmzVNN1ucwYWhSQKUyG5wuaGXvhjzZ25sf41WV6B",
      "created": "2021-06-07T21:29:00",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 1340699,
      "signing_key": "XGT6gRy5TJTibrsdLkQQLTkBTrKbeHvxbVBEvJA5wJiiGgZXN8T3h",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 10,
      "owner": "XGTDco6nNwVPohJ2a4nTyutoMJJ2T5LmZBmf4NYw1pj",
      "created": "2021-06-07T22:01:27",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT84vuo4pgd494jWqoVzdZ9ktav7CTxoyYFGQLMujatgny4xrvTG",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    }
  ]
}
```

---

### Procedure:  find_witnesses
Returns a list of witnesses corresponding to inputted wallet addresses.
#### Arguments
* Vector<String> `miners` - _List of wallet addresses to retreive associated witnesses._
#### Example JSON Payload Format
```javascript
{
  miners: [
    'XGT0000000000000000000000000000000000000000'
  ]
}
```
#### Example JSON Response
```javascript
{
  "miners": [
    {
      "id": 0,
      "owner": "XGT0000000000000000000000000000000000000000",
      "created": "1970-01-01T00:00:00",
      "url": "",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 93538,
      "signing_key": "XGT7dDoJbrmueAw431pPbjLDoRhqFCC5Xs5o6f1cZLepWEpkcy3Tc",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    }
  ]
}
```

-------------------------------------------------------------------------------

## Wallets

### Procedure:  list_wallets
List wallets ordered by specified key.
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
{
  "wallets": [
    {
      "id": 1,
      "name": "XGT0000000000000000000000000000000000000000",
      "recovery": {
        "weight_threshold": 1,
        "wallet_auths": [

        ],
        "key_auths": [
          [
            "XGT7dDoJbrmueAw431pPbjLDoRhqFCC5Xs5o6f1cZLepWEpkcy3Tc",
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
            "XGT7dDoJbrmueAw431pPbjLDoRhqFCC5Xs5o6f1cZLepWEpkcy3Tc",
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
            "XGT7dDoJbrmueAw431pPbjLDoRhqFCC5Xs5o6f1cZLepWEpkcy3Tc",
            1
          ]
        ]
      },
      "memo_key": "XGT7dDoJbrmueAw431pPbjLDoRhqFCC5Xs5o6f1cZLepWEpkcy3Tc",
      "json_metadata": "",
      "social_json_metadata": "",
      "last_recovery_update": "1970-01-01T00:00:00",
      "last_account_update": "1970-01-01T00:00:00",
      "created": "1970-01-01T00:00:00",
      "mined": true,
      "recovery_account": "",
      "last_account_recovery": "1970-01-01T00:00:00",
      "reset_account": "XGT0000000000000000000000000000000000000002",
      "comment_count": 0,
      "lifetime_vote_count": 0,
      "post_count": 0,
      "can_vote": true,
      "energybar": {
        "current_energy": 0,
        "last_update_time": 0
      },
      "balance": {
        "amount": "1873016361281114",
        "precision": 8,
        "nai": "@@000000021"
      },
      "witnesses_voted_for": 0,
      "last_post": "1970-01-01T00:00:00",
      "last_root_post": "1970-01-01T00:00:00",
      "last_post_edit": "1970-01-01T00:00:00",
      "last_vote_time": "1970-01-01T00:00:00",
      "post_bandwidth": 0,
      "is_xtt": false
    },
    {
      "id": 0,
      "name": "XGT0000000000000000000000000000000000000001",
      "recovery": {
        "weight_threshold": 1,
        "wallet_auths": [

        ],
        "key_auths": [

        ]
      },
      "money": {
        "weight_threshold": 1,
        "wallet_auths": [

        ],
        "key_auths": [

        ]
      },
      "social": {
        "weight_threshold": 0,
        "wallet_auths": [

        ],
        "key_auths": [

        ]
      },
      "memo_key": "XGT1111111111111111111111111111111114T1Anm",
      "json_metadata": "",
      "social_json_metadata": "",
      "last_recovery_update": "1970-01-01T00:00:00",
      "last_account_update": "1970-01-01T00:00:00",
      "created": "1970-01-01T00:00:00",
      "mined": true,
      "recovery_account": "",
      "last_account_recovery": "1970-01-01T00:00:00",
      "reset_account": "XGT0000000000000000000000000000000000000002",
      "comment_count": 0,
      "lifetime_vote_count": 0,
      "post_count": 0,
      "can_vote": true,
      "energybar": {
        "current_energy": 0,
        "last_update_time": 0
      },
      "balance": {
        "amount": "0",
        "precision": 8,
        "nai": "@@000000021"
      },
      "witnesses_voted_for": 0,
      "last_post": "1970-01-01T00:00:00",
      "last_root_post": "1970-01-01T00:00:00",
      "last_post_edit": "1970-01-01T00:00:00",
      "last_vote_time": "1970-01-01T00:00:00",
      "post_bandwidth": 0,
      "is_xtt": false
    },
    {
      "id": 2,
      "name": "XGT0000000000000000000000000000000000000002",
      "recovery": {
        "weight_threshold": 1,
        "wallet_auths": [

        ],
        "key_auths": [

        ]
      },
      "money": {
        "weight_threshold": 1,
        "wallet_auths": [

        ],
        "key_auths": [

        ]
      },
      "social": {
        "weight_threshold": 0,
        "wallet_auths": [

        ],
        "key_auths": [

        ]
      },
      "memo_key": "XGT1111111111111111111111111111111114T1Anm",
      "json_metadata": "",
      "social_json_metadata": "",
      "last_recovery_update": "1970-01-01T00:00:00",
      "last_account_update": "1970-01-01T00:00:00",
      "created": "1970-01-01T00:00:00",
      "mined": true,
      "recovery_account": "",
      "last_account_recovery": "1970-01-01T00:00:00",
      "reset_account": "XGT0000000000000000000000000000000000000002",
      "comment_count": 0,
      "lifetime_vote_count": 0,
      "post_count": 0,
      "can_vote": true,
      "energybar": {
        "current_energy": 0,
        "last_update_time": 0
      },
      "balance": {
        "amount": "0",
        "precision": 8,
        "nai": "@@000000021"
      },
      "witnesses_voted_for": 0,
      "last_post": "1970-01-01T00:00:00",
      "last_root_post": "1970-01-01T00:00:00",
      "last_post_edit": "1970-01-01T00:00:00",
      "last_vote_time": "1970-01-01T00:00:00",
      "post_bandwidth": 0,
      "is_xtt": false
    },
    {
      "id": 4,
      "name": "XGT0000000000000000000000000000000000000003",
      "recovery": {
        "weight_threshold": 0,
        "wallet_auths": [

        ],
        "key_auths": [

        ]
      },
      "money": {
        "weight_threshold": 0,
        "wallet_auths": [

        ],
        "key_auths": [

        ]
      },
      "social": {
        "weight_threshold": 0,
        "wallet_auths": [

        ],
        "key_auths": [

        ]
      },
      "memo_key": "XGT1111111111111111111111111111111114T1Anm",
      "json_metadata": "",
      "social_json_metadata": "",
      "last_recovery_update": "1970-01-01T00:00:00",
      "last_account_update": "1970-01-01T00:00:00",
      "created": "1970-01-01T00:00:00",
      "mined": true,
      "recovery_account": "",
      "last_account_recovery": "1970-01-01T00:00:00",
      "reset_account": "XGT0000000000000000000000000000000000000002",
      "comment_count": 0,
      "lifetime_vote_count": 0,
      "post_count": 0,
      "can_vote": true,
      "energybar": {
        "current_energy": 0,
        "last_update_time": 0
      },
      "balance": {
        "amount": "0",
        "precision": 8,
        "nai": "@@000000021"
      },
      "witnesses_voted_for": 0,
      "last_post": "1970-01-01T00:00:00",
      "last_root_post": "1970-01-01T00:00:00",
      "last_post_edit": "1970-01-01T00:00:00",
      "last_vote_time": "1970-01-01T00:00:00",
      "post_bandwidth": 0,
      "is_xtt": false
    }
  ]
}
```
---

### Procedure:  find_wallets
Returns list of wallets if inputted wallet addresses exist.
#### Variables

#### Arguments
* Array of Strings `wallets` - _Wallet addresses to search for._
#### Example JSON Payload Format
```javascript
{
  wallets: [
    'XGT0000000000000000000000000000000000000000'
  ]
}
```
#### Example JSON Response
```javascript
{
  "wallets": [
    {
      "id": 1,
      "name": "XGT0000000000000000000000000000000000000000",
      "recovery": {
        "weight_threshold": 1,
        "wallet_auths": [

        ],
        "key_auths": [
          [
            "XGT7dDoJbrmueAw431pPbjLDoRhqFCC5Xs5o6f1cZLepWEpkcy3Tc",
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
            "XGT7dDoJbrmueAw431pPbjLDoRhqFCC5Xs5o6f1cZLepWEpkcy3Tc",
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
            "XGT7dDoJbrmueAw431pPbjLDoRhqFCC5Xs5o6f1cZLepWEpkcy3Tc",
            1
          ]
        ]
      },
      "memo_key": "XGT7dDoJbrmueAw431pPbjLDoRhqFCC5Xs5o6f1cZLepWEpkcy3Tc",
      "json_metadata": "",
      "social_json_metadata": "",
      "last_recovery_update": "1970-01-01T00:00:00",
      "last_account_update": "1970-01-01T00:00:00",
      "created": "1970-01-01T00:00:00",
      "mined": true,
      "recovery_account": "",
      "last_account_recovery": "1970-01-01T00:00:00",
      "reset_account": "XGT0000000000000000000000000000000000000002",
      "comment_count": 0,
      "lifetime_vote_count": 0,
      "post_count": 0,
      "can_vote": true,
      "energybar": {
        "current_energy": 0,
        "last_update_time": 0
      },
      "balance": {
        "amount": "1873016361281114",
        "precision": 8,
        "nai": "@@000000021"
      },
      "witnesses_voted_for": 0,
      "last_post": "1970-01-01T00:00:00",
      "last_root_post": "1970-01-01T00:00:00",
      "last_post_edit": "1970-01-01T00:00:00",
      "last_vote_time": "1970-01-01T00:00:00",
      "post_bandwidth": 0,
      "is_xtt": false
    }
  ]
}
```

---

### Procedure:  list_escrows
List wallets ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns

#### Example JSON Payload Format
```javascript
payload = {
  from: 'XGT0000000000000000000000000000000000000000'
}
```
#### Example JSON Response
```javascript
{
  "escrows": [

  ]
}
```

---

### Procedure:  find_escrows
List wallets ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  list_withdraw_vesting_routes
List wallets ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  find_withdraw_vesting_routes
List wallets ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  list_savings_withdrawals
List wallets ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  find_savings_withdrawals
List wallets ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  list_vesting_delegations
List wallets ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  find_vesting_delegations
List wallets ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  list_vesting_delegation_expirations
List wallets ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  find_vesting_delegation_expirations
List wallets ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  list_sbd_conversion_requests
List wallets ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  find_sbd_conversion_requests
List wallets ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  list_decline_voting_rights_requests
List wallets ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  find_decline_voting_rights_requests
List wallets ordered by specified key
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
List wallets ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  find_comments
List wallets ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  list_votes
List wallets ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  find_votes
List wallets ordered by specified key
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
List wallets ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  find_limit_orders
List wallets ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  get_order_book
List wallets ordered by specified key
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
List wallets ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  find_proposals
List wallets ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  list_proposal_votes
List wallets ordered by specified key
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
This is a general purpose API that checks signatures against wallets for an
arbitrary sha256 hash using the existing authority structures in Steem
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

-------------------------------------------------------------------------------

## XTTs

### Procedure:  get_nai_pool
@return array of Numeric Asset Identifier (NAI) available to be used for new
XTTs to be created.
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  list_xtt_contributions
description
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  find_xtt_contributions
description#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  list_xtt_tokens
description#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  find_xtt_tokens
description
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  list_xtt_token_emissions
description
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  find_xtt_token_emissions
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

_PRECISION": 100000000,
  "XGT_BLOCKCHAIN_PRECISION_DIGITS": 8,
  "XGT_BLOCKCHAIN_HARDFORK_VERSION": "0.0.0",
  "XGT_BLOCKCHAIN_VERSION": "0.0.0",
  "XGT_BLOCK_INTERVAL": 5,
  "XGT_BLOCKS_PER_DAY": 17280,
  "XGT_BLOCKS_PER_HOUR": 720,
  "XGT_BLOCKS_PER_YEAR": 6307200,
  "XGT_CHAIN_ID": "4e08b752aff5f66e1339cb8c0a8bca14c4ebb238655875db7dade86349091197",
  "XGT_COMMENT_TITLE_LIMIT": 256,
  "XGT_CONTENT_APR_PERCENT": 3875,
  "XGT_CONTENT_CONSTANT_HF0": "2000000000000",
  "XGT_CONTENT_CONSTANT_HF21": "2000000000000",
  "XGT_CREATE_WALLET_WITH_XGT_MODIFIER": 30,
  "XGT_CURATE_APR_PERCENT": 3875,
  "XGT_CUSTOM_OP_DATA_MAX_LENGTH": 8192,
  "XGT_CUSTOM_OP_ID_MAX_LENGTH": 32,
  "XGT_DOWNVOTE_POOL_PERCENT_HF21": 2500,
  "XGT_FEED_INTERVAL_BLOCKS": 720,
  "XGT_GENESIS_TIME": "2020-04-14T04:53:35",
  "XGT_HARDFORK_REQUIRED_WITNESSES": 17,
  "XGT_HF21_CONVERGENT_LINEAR_RECENT_CLAIMS": "503600561838938636",
  "XGT_INFLATION_NARROWING_PERIOD": 250000,
  "XGT_INFLATION_RATE_START_PERCENT": 978,
  "XGT_INFLATION_RATE_STOP_PERCENT": 95,
  "XGT_INIT_MINER_NAME": "XGT0000000000000000000000000000000000000000",
  "XGT_INIT_PUBLIC_KEY_STR": "XGT7dDoJbrmueAw431pPbjLDoRhqFCC5Xs5o6f1cZLepWEpkcy3Tc",
  "XGT_INIT_SUPPLY": "1872936875000000",
  "XGT_INIT_TIME": "1970-01-01T00:00:00",
  "XGT_IRREVERSIBLE_THRESHOLD": 7500,
  "XGT_MAX_WALLET_CREATION_FEE": 0,
  "XGT_MAX_WALLET_NAME_LENGTH": 16,
  "XGT_MAX_ASSET_WHITELIST_AUTHORITIES": 10,
  "XGT_MAX_AUTHORITY_MEMBERSHIP": 40,
  "XGT_MAX_BLOCK_SIZE": 655360000,
  "XGT_SOFT_MAX_BLOCK_SIZE": 2097152,
  "XGT_MAX_COMMENT_DEPTH": 65535,
  "XGT_MAX_COMMENT_DEPTH_PRE_HF17": 6,
  "XGT_MAX_FEED_AGE_SECONDS": 604800,
  "XGT_MAX_INSTANCE_ID": "281474976710655",
  "XGT_MAX_MEMO_SIZE": 2048,
  "XGT_MAX_WITNESSES": 10,
  "XGT_MAX_VOTED_WITNESSES": 0,
  "XGT_MAX_MINER_WITNESSES": 10,
  "XGT_MAX_PERMLINK_LENGTH": 256,
  "XGT_MAX_RATION_DECAY_RATE": 1000000,
  "XGT_MAX_RESERVE_RATIO": 20000,
  "XGT_MAX_SATOSHIS": "4611686018427387903",
  "XGT_MAX_SHARE_SUPPLY": "1000000000000000",
  "XGT_MAX_SIG_CHECK_DEPTH": 2,
  "XGT_MAX_SIG_CHECK_WALLETS": 125,
  "XGT_MAX_TIME_UNTIL_EXPIRATION": 3600,
  "XGT_MAX_TRANSACTION_SIZE": 65536,
  "XGT_MAX_UNDO_HISTORY": 151200,
  "XGT_MAX_URL_LENGTH": 127,
  "XGT_MAX_VOTE_CHANGES": 5,
  "XGT_MAX_WITNESS_URL_LENGTH": 2048,
  "XGT_MIN_WALLET_CREATION_FEE": 0,
  "XGT_MIN_WALLET_NAME_LENGTH": 3,
  "XGT_MIN_BLOCK_SIZE_LIMIT": 65536,
  "XGT_MIN_BLOCK_SIZE": 115,
  "XGT_MIN_PERMLINK_LENGTH": 0,
  "XGT_MIN_REPLY_INTERVAL": 20000000,
  "XGT_MIN_REPLY_INTERVAL_HF20": 3000000,
  "XGT_MIN_ROOT_COMMENT_INTERVAL": 300000000,
  "XGT_MIN_COMMENT_EDIT_INTERVAL": 3000000,
  "XGT_MIN_VOTE_INTERVAL_SEC": 3,
  "XGT_MINER_WALLET": "XGT0000000000000000000000000000000000000001",
  "XGT_MINER_PAY_PERCENT": 100,
  "XGT_MIN_FEEDS": 3,
  "XGT_MINING_BLOCKS_PER_SECOND": "0.25000000000000000",
  "XGT_MINING_BTC_BLOCKS_PER_SECOND": "0.00166666670702398",
  "XGT_MINING_RELATIVE_SPEED": "150.00000000000000000",
  "XGT_STARTING_OFFSET": 0,
  "XGT_MINING_REWARD": {
    "amount": "4166166",
    "precision": 8,
    "nai": "@@000000021"
  },
  "XGT_MIN_POW_REWARD": {
    "amount": "4166166",
    "precision": 8,
    "nai": "@@000000021"
  },
  "XGT_MINING_ADJUSTMENT_MAX_FACTOR": "4.00000000000000000",
  "XGT_MINING_REWARD_HALVING_INTERVAL": 30150000,
  "XGT_MINING_RECALC_EVERY_N_BLOCKS": 302400,
  "XGT_MINING_TARGET_START": "000000ffff000000000000000000000000000000000000000000000000000000",
  "XGT_MINING_TARGET_MAX": "00000ffff0000000000000000000000000000000000000000000000000000000",
  "XGT_MIN_TRANSACTION_EXPIRATION_LIMIT": 25,
  "XGT_MIN_TRANSACTION_SIZE_LIMIT": 1024,
  "XGT_MIN_UNDO_HISTORY": 10,
  "XGT_NULL_WALLET": "XGT0000000000000000000000000000000000000002",
  "XGT_RECOVERY_AUTH_HISTORY_TRACKING_START_BLOCK_NUM": 3186477,
  "XGT_RECOVERY_AUTH_RECOVERY_PERIOD": "2592000000000",
  "XGT_RECOVERY_CHALLENGE_COOLDOWN": "86400000000",
  "XGT_RECOVERY_CHALLENGE_FEE": {
    "amount": "30000",
    "precision": 8,
    "nai": "@@000000021"
  },
  "XGT_RECOVERY_UPDATE_LIMIT": 3600000000,
  "XGT_POST_AVERAGE_WINDOW": 86400,
  "XGT_POST_WEIGHT_CONSTANT": 1600000000,
  "XGT_POW_APR_PERCENT": 750,
  "XGT_PRODUCER_APR_PERCENT": 750,
  "XGT_SECONDS_PER_YEAR": 31536000,
  "XGT_REVERSE_AUCTION_WINDOW_SECONDS": 300,
  "XGT_ROOT_POST_PARENT": "",
  "XGT_SOFT_MAX_COMMENT_DEPTH": 255,
  "XGT_START_MINER_VOTING_BLOCK": 518400,
  "XGT_TEMP_WALLET": "XGT0000000000000000000000000000000000000003",
  "XGT_UPVOTE_LOCKOUT_SECONDS": 43200,
  "XGT_VOTE_DUST_THRESHOLD": 50000000,
  "XGT_VOTING_ENERGY_REGENERATION_SECONDS": 86400,
  "XGT_VIRTUAL_SCHEDULE_LAP_LENGTH": "18446744073709551615",
  "XGT_VIRTUAL_SCHEDULE_LAP_LENGTH2": "340282366920938463463374607431768211455",
  "XGT_VOTES_PER_PERIOD_XTT_HF": 50,
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
  "XGT_DECAY_BACKSTOP_PERCENT": 9000,
  "XGT_BLOCK_GENERATION_POSTPONED_TX_LIMIT": 5,
  "XGT_PENDING_TRANSACTION_EXECUTION_LIMIT": 200000,
  "XGT_TREASURY_WALLET": "XGT0000000000000000000000000000000000000004",
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
  "blockchain_version": "0.0.0",
  "xgt_revision": "0583f0cb28b05b547e7a57acc4b82959fb78da9b",
  "fc_revision": "0583f0cb28b05b547e7a57acc4b82959fb78da9b",
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
  "head_block_number": 1341626,
  "head_block_id": "001478ba34854673ffc07e04e5a715f8b21bfb51",
  "time": "2021-07-06T23:09:18",
  "current_witness": "XGT8JEbh79M3xbSJa9kTxhmpWKZEuKhzFz5PFnXNV9u",
  "mining_target": "0000000a31c4a7d274058c7e8a9c6d0ad025f08df1e5861e9c8ad4c410731e46",
  "total_pow": 1340687,
  "num_pow_witnesses": 1340688,
  "virtual_supply": {
    "amount": "1872936875000000",
    "precision": 8,
    "nai": "@@000000021"
  },
  "current_supply": {
    "amount": "1872936875000000",
    "precision": 8,
    "nai": "@@000000021"
  },
  "confidential_supply": {
    "amount": "0",
    "precision": 8,
    "nai": "@@000000021"
  },
  "maximum_block_size": 655360000,
  "required_actions_partition_percent": 0,
  "current_aslot": 0,
  "recent_slots_filled": "340282366920938463463374607431768211455",
  "participation_count": 128,
  "last_irreversible_block_num": 1341616,
  "target_votes_per_period": 40,
  "delegation_return_period": 86400,
  "reverse_auction_seconds": 300,
  "next_maintenance_time": "2020-04-14T04:53:35",
  "last_budget_time": "2020-04-14T04:53:35",
  "downvote_pool_percent": 0,
  "xtt_creation_fee": {
    "amount": "1000",
    "precision": 8,
    "nai": "@@000000021"
  }
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
    "2020-04-14T04:53:35"
  ],
  "last_hardfork": 0,
  "current_hardfork_version": "0.0.0",
  "next_hardfork": "0.0.0",
  "next_hardfork_time": "1970-01-01T00:00:00"
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
  start: 0,
  limit: 3,
  order: "by_name"
}
```
#### Example JSON Response
```javascript
{
  "witnesses": [
    {
      "id": 0,
      "owner": "XGT0000000000000000000000000000000000000000",
      "created": "1970-01-01T00:00:00",
      "url": "",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 93538,
      "signing_key": "XGT7dDoJbrmueAw431pPbjLDoRhqFCC5Xs5o6f1cZLepWEpkcy3Tc",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 165,
      "owner": "XGTBTR3cWLJVythoqRynqRNtgiDRe68v17KKJbbpLuv",
      "created": "2021-06-28T01:14:11",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 812235,
      "signing_key": "XGT5KeDHoGs3jfhLSRMDoMvWgRDXbMsgmVCBJHeye6pXpEawiokaL",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 155,
      "owner": "XGT7vdjEsVeDz5tifitKBPm3rcCTExLp1BtwvD3NvJr",
      "created": "2021-06-20T05:00:28",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT8NEAGHRe83iAurBdK687U1fD9wYqhBs6TWaqr3CPpMDczzf4T7",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 168,
      "owner": "XGTCmh8sAGbhMttykSSQAruvD76gvnMb1E6PT49YVin",
      "created": "2021-07-01T13:31:32",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT8GLzJJcng2mSqsdRyRoijfumUmAj3dskFmoDmWh67fm6yeaVw2",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 8,
      "owner": "XGTC4jWpZYwPM57daCDSR8bJdSzUCt7t1of5bj84omQ",
      "created": "2021-06-07T21:46:13",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT854uosvkV8AiH5uqx2mBcA9VucdyuCfgWPe31xZJkfygxunqpu",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 64,
      "owner": "XGTXSJrfvybryBgnWHVmQEtjKUbDoBSP2BVwQUXBueP",
      "created": "2021-06-09T16:08:18",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT5VJpvtRveztzvRSZ7UWV8VjBBL4iw3sZTCGUfXRbJD3mi2HJhv",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 174,
      "owner": "XGTrZmdKpaXFkV1iQqZ9hmy8NhxNWaEU2KQgzYpZBDc",
      "created": "2021-07-06T15:08:41",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT5NS9jjaDhWETfXsmYDg2JnQa8vM8SJF5x7NrqhMiZXy7LgZgFL",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 115,
      "owner": "XGTBuSqkKhb1PQioVzArLnUBXAnQCbqD2ew7KuzrVb1",
      "created": "2021-06-15T17:27:09",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT6PZpeFfxBFe6U2vjEYZuTkDvoj4KAHnaCuR5RvKLsEwqGnaQq9",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 169,
      "owner": "XGTAgcGtv2ntgw4hoXTWz93RMAomo4EK3EAyeiB6LEY",
      "created": "2021-07-02T03:14:40",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 962517,
      "signing_key": "XGT5dqhtZcTW3DGCo8SAc2sE572ypSsUGGrvW9jUki2o18pyPZnFq",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 104,
      "owner": "XGTBi9M4wHTwmFpuPHzDQHpbiL7huW113JRjnmqZJJR",
      "created": "2021-06-15T07:19:15",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT4v61HgWYsuuHurnwz4QpZFijbVA7hSg5vLbmkT8xFRkwt5NGrD",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 89,
      "owner": "XGT4uFLr6eJNavX97G4skac8uPQ65t3f3c15YA8v2iA",
      "created": "2021-06-14T09:17:30",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 379986,
      "signing_key": "XGT5JCw9cM8P7mQvqM1MTtEUgR3s4TMvp7FKBCBcwc5JFXF2X1B3T",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 163,
      "owner": "XGTEzp6fe8XsRNq8DfW5vcgQ5PJuiUeg3c94aonGLXe",
      "created": "2021-06-25T23:44:18",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT85tW5jLzYtF9Ug4sDkEymu3wY34edbdpP1c6fAne2ymvpuHMcs",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 9,
      "owner": "XGT8ZbbkW8xo58x4ZXBCZyK1AnNMicFv3x7prvofY8S",
      "created": "2021-06-07T21:56:32",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT6rhh5Yh6wVZN2nVCqXCY4vc3d8PxRSHdxcFvVMncow6Js82yrF",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 66,
      "owner": "XGT2bHiA5AF6vuJTSW9L5m91HDUzeLvU4ERmgLwTXDZ",
      "created": "2021-06-09T16:08:39",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT7NvsnX4HTgMzwhgXrM98EAsghjJN1NMtGVX7BnC1fnp2BmAM5U",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 156,
      "owner": "XGT9H9eggTTpKDRAsT9LmqZLg9AijC375DVqjDRNiGf",
      "created": "2021-06-21T06:13:53",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT5WuhSne3PrXqwwWDC9gLDSvaPtTceWU9zdppw6Ggz46WaDWUDr",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 83,
      "owner": "XGT3vuT1SegDyih6T5jmT3WJ9YTPYRnY5GE4DwfgD96",
      "created": "2021-06-13T15:16:50",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 493456,
      "signing_key": "XGT5agvZ3gg7HYQJJ6oP2tAeQkNwSSzSr6TsKBcGd7V4kSXakV8jC",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 149,
      "owner": "XGT6TnBGQxPT6Vg3AFn9fRgcFdyvv4nZ5ZqAKJhGGog",
      "created": "2021-06-18T02:51:50",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT8YFrw1LEheqYYjDgK5BUtoTdm4eVoinobXgZpfYf2vepinE9cu",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 12,
      "owner": "XGT3vt1JsCNdrfQh8kN8RZCwCsLsRwGG5fGzPdsuppn",
      "created": "2021-06-07T22:20:02",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT7m3pPNzN7rJRfAbwuBJoKuoHY1MeUWSnGvqkowkX3nJrPAq5xL",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 139,
      "owner": "XGT6rcrHLbiVN7UWwc6EE1U8QyqAp9iv5pnbNhBGbL6",
      "created": "2021-06-17T15:50:33",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT7sY8QTXjQeFNT9q5ttGMrWjek8A2ftzdKev8ajq7VrCrpnFFUn",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 75,
      "owner": "XGT2jhfspb3HV3uct9FCT9zDYW7oUyTf6AAdC5ECqnE",
      "created": "2021-06-11T16:11:23",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT5GdZYCtPuCruTtJYLqm6ewVCou2bFjcQdAGExXdZr5WM9gPAwc",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 56,
      "owner": "XGTGHqMjp6kqQcb6h6sXwUqU4ZeaRGby6Rrd4VwwLes",
      "created": "2021-06-08T08:19:59",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT8Hjbs4vr3aK9yB8ymLhRhciv7Q9Nc1PBaGHVhQpFtR4PeZhFfL",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 39,
      "owner": "XGTGM18acHjFPVKsTkYCmRPhmtBvdKH86bEBz1MbvJb",
      "created": "2021-06-08T06:34:29",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT7FomwHBebQSRb6LLiqDkyrF6mHgVANuzeMXqHAEe46YUwHj1Kq",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 29,
      "owner": "XGT5QKJzUtS4nGPJLD1jmJmxb7wLj6uE6putfUzoScY",
      "created": "2021-06-08T01:44:46",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 510434,
      "signing_key": "XGT71avwWsd1Uyqs4uQ31rVz7Pka6JMnjQVjRxPjmYe6zmwkDrrsq",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 150,
      "owner": "XGT6dSQDvF7uMmcF66Rc1nVFNg2qhDdU7VQDafQGvUu",
      "created": "2021-06-18T05:40:30",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 1340690,
      "signing_key": "XGT55mionaVumbtf849GbramAKXZ5tnJMpX1qewptjLSW58JUkHP8",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 154,
      "owner": "XGTBqPasoLtPe1SjDeCEnhx1RnZWiPae8W2JjaNKxgE",
      "created": "2021-06-18T23:12:37",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT83kBTpbtAPLQoRtuYxoq8t9puDA6Hzjt7rHCjRV6976FYiDDhP",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 98,
      "owner": "XGTAcg5xfmrNijzvrVWn3L2jTMrAZL3h8WUXG3kh53Z",
      "created": "2021-06-14T23:08:09",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT5zQPqt4TokKyPxvTccp8MmSMiKz2gGDxyjBDyMmXwE3spi8s8k",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 4,
      "owner": "XGTH5jncbEmBvVBtgDJJHFzvd4nGKtQ18ooiMgA9Ck8",
      "created": "2021-06-07T21:30:07",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT7b8UEa1R9GzLxdMTNsWR25fjoZv4nqjcuu6n4Xj1qqH1aYqY9W",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 2,
      "owner": "XGT5nbpvvwDUvhEY3FKKW3aV7g5kQRbp92GDBPsJvwC",
      "created": "2021-06-07T21:29:00",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT65bVJbm8M56JvaB9F87Y9FTqCgPvmQ9NVAxxUnLeyQc9s74puX",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 41,
      "owner": "XGTFazBN9rLM5rK6Doa9T3HHdVSFod7x9Kk6E3HhCgZ",
      "created": "2021-06-08T06:58:54",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT8EbiFbE4p9ZuR3EsN2GmXQJmgQNnAnhfST2PuTMZJpx1DjBUX2",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 81,
      "owner": "XGT7Bo9owdAv5drGa1Kp3562VsNz2g669U13XUhymev",
      "created": "2021-06-13T06:19:41",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT5VFihBQwdeyoM3obQ6hhfqtU6Ceove5M3R9Cu7qWRNxHfHEdfJ",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 153,
      "owner": "XGTC8HErX74o9AHLEf7BaGZoZDNwpGjx9VSCcPUfcTv",
      "created": "2021-06-18T17:44:16",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT5kKXa4Jif3GfRfAN3WrxZBQ6Uwy2eXvL7QUebdKr7doP9Qi3au",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 152,
      "owner": "XGT5R4KMp3Vxf4K46CR1Y5CsYLgULGXF9upoHCV7uJj",
      "created": "2021-06-18T17:28:51",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT5H3x1rLiq9XHSVgw3f7KwCtzpnWBk7ceEYKmmQjNyRAxRjeGLx",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 37,
      "owner": "XGTDcKm1qFrXHdS9WnYzJ8ZfvKSsrp42A7JezzsnJ7g",
      "created": "2021-06-08T05:58:46",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT751cWuQsHDsBSeiqVPD1EiR1R2b1QYAYnAUdSb8SLiYM2YuQxP",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 63,
      "owner": "XGTAK7uQpKA4u2B3dQuUH2DwEmPaHU7WBCBN6N4FutA",
      "created": "2021-06-09T04:47:16",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT7MTq73gHzQZgeaEZS6ZSkFtJ7HDWfTTeogjs7Sdcs39XqT8r5F",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 101,
      "owner": "XGTCoTeMrGvGSsrsNk9sTJfLHvHGTVDvBEGcg29k3vF",
      "created": "2021-06-15T06:12:44",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 382118,
      "signing_key": "XGT7M5hAa4tbks89Fp6Jhu5U18LnBEk2eG1poeR8vu2xqFjkmJ9p1",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 107,
      "owner": "XGT6zQJQTac3PfJdv24ez8DdG2RxX88pBRKMxRtRYy3",
      "created": "2021-06-15T11:03:30",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 548586,
      "signing_key": "XGT5pRCSJ14aHM7bYNtoyvJiJ787vPbVbF9CCQYYBABtnXXfPfqRn",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 148,
      "owner": "XGT3jFXKk4RNFwAd2PRaC2D9t16higNNC9RjVvxZCjw",
      "created": "2021-06-18T01:50:28",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT7yiVrg16hNFRWgU3RTEGXPno7WYJCtYvwFiA2uqGq1HHNx3Usr",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 61,
      "owner": "XGTEEHrvP5cXpg69bGYQGJSd9Wfz4PuhCF1xaZLsFos",
      "created": "2021-06-09T01:14:29",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT8d2GbNhqg4aNJbnGFB2gzafhsr7zq8UpgDumiCFYn9STp3h8z5",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 125,
      "owner": "XGTDCC8bpuq6L6GLQN4w3KgzusXufeoPCfhKES37ZAd",
      "created": "2021-06-16T16:44:51",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT4wxkBfFexU2HpiRFkJi4QfJP6s4nTyTZbMz9pFPVBUP6RbuBwy",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 116,
      "owner": "XGTEev2AAkuNhR4Hxcck9khkmADQWoibDSef9y4biMe",
      "created": "2021-06-15T20:23:38",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT6WGEgLPB94qMnK2mobZgPArW5wKas5HpL39QHV1tMCnGaVrJfu",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 167,
      "owner": "XGT5EmFknGeZzwyLPQpV5VVGBa5E64ZnDT7FY7qhQUn",
      "created": "2021-06-30T19:51:37",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT6mBFdmkeG1zXJWgoDSEnZ23p3GhMcHUJYWjoiowMLYyd3m2e22",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 55,
      "owner": "XGT9eyLQW8u8fetnqfN2GuSQRG1ZQRm3DawYDFGePrv",
      "created": "2021-06-08T07:49:32",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT8RPLkpZWdFocceXPoQj1RZsov1eevbPV85St8E76krZzVHAkaT",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 85,
      "owner": "XGTEk87STghgHXCNMmXvzcoU7nvPfU3zDuCntrewZis",
      "created": "2021-06-14T05:20:59",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 711698,
      "signing_key": "XGT7TCHNr28wH53X3SPV8C7WKpQDbjEWEkwc9EUPZAE3RBDqg9ah7",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 11,
      "owner": "XGTDkkLogBPdtB6i2ZUvBaz4NgXVgcRJF1Jgvsny55E",
      "created": "2021-06-07T22:18:53",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 504980,
      "signing_key": "XGT5tZWPRGkUyfiy68KK9kRym2ZxAqzNM8a1ZdxvESUWjE9nq8NuF",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 103,
      "owner": "XGTCQjDWREvCJyyijftf6ZqpsEAfWb96FoNacZhjczj",
      "created": "2021-06-15T06:32:04",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 459372,
      "signing_key": "XGT5SFfU1CA3kAqjKZviVSXdszRBgr7tdvjXmnPD8ELY3LauyaqjU",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 34,
      "owner": "XGTFJbSijB2WyZFw6vurNScPkUvQn7nqFsEqTn53uSd",
      "created": "2021-06-08T05:08:41",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT5VYpMfUVdzxpYuQPE17dTKiSpwX7QiNm6EqoZCcN7FtUE4i1LM",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 166,
      "owner": "XGT8JEbh79M3xbSJa9kTxhmpWKZEuKhzFz5PFnXNV9u",
      "created": "2021-06-30T13:57:15",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 1340718,
      "signing_key": "XGT5C96My82amdrtGvj58tAq76yDjmmWjNCA3xdqyDfdTRBxZyF6i",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 143,
      "owner": "XGTEz1rG1BE1r8Hn6iAMpmUoXE132UcHG4Agkqqg2zT",
      "created": "2021-06-17T21:09:32",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 469568,
      "signing_key": "XGT8UmqMRZ9cfZMMNTjNm3EJNkMLkfTgNZFYo2bRfmMQNCrdYjvMo",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 16,
      "owner": "XGT7Yw6iMUMfbGBeHtgzPTyFBN72x3gWGCjvc1nuXH5",
      "created": "2021-06-07T22:39:23",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT7KxC5na4LjVSA38idSVZqnR7Jyf3VKJKQBJGVhJLFPAhFPeFhM",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 48,
      "owner": "XGT8CXwcz4HubwW3RYoqh5qZffJF5tJ5GSM4a6QwJsV",
      "created": "2021-06-08T07:29:15",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT5v2ByuM6pykLM6PvzGtpnRFCXtvDdtpv9Ha5czguHoCk3R3ggb",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 5,
      "owner": "XGT8CW6Pk3wDAwwEGbMZhXo2RvfztV9gGzT2ByN78DG",
      "created": "2021-06-07T21:34:49",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT4wGcWdD8RZEQdu1qcGYm5p9UoR4GeLbzMSGXZudW7LPTvZSB3s",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 108,
      "owner": "XGTGveyhdWrN1yxbgum92cii1CHmYzi7Hx2dYae7fH9",
      "created": "2021-06-15T11:07:02",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT8RMokwbKV3555HoZX4tf5ZCkifAnWi52zpd2TJSnGVczD6VMoq",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 157,
      "owner": "XGTAWdNS2uazGjm2vAbHjTrBB29mk2YrJBCDwSnsQ4t",
      "created": "2021-06-22T22:15:56",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 1340646,
      "signing_key": "XGT5TFpAEBks9qrsVh9hFLJf6A3YFjTf1prUgaCfeApSXFZTB1CFa",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 24,
      "owner": "XGT8RnxMN5EX1z9vjmtu4heQToS2q7jKJuLJAMVqfCu",
      "created": "2021-06-07T23:17:34",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT8h3oBmSQFgxESC87foDmESbYFVwLKmAmgZxHtR4LALPCUtwfsx",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 62,
      "owner": "XGTDHeEmdowDKb2a82WanBmuQetzTPzbJvrtZuqNZs5",
      "created": "2021-06-09T01:45:57",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT62ctdUozdD4ziJCpYqP5FJwPWEmQzT1cLPcYvMs1EDSRNcFnSG",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 7,
      "owner": "XGTFaH4L4UWvLhnD2NqL1ZexBFbtwHnUKLPnhwReVU8",
      "created": "2021-06-07T21:40:27",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT7GEoGpgVjDtnpaRuBicg59HtAruHC8GFqyHfbNARshUd3m6ozK",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 44,
      "owner": "XGTA7KhMnJXsYzRqqpJRb9zS2akz6koTKyq38n7nkWz",
      "created": "2021-06-08T07:20:37",
      "url": "http://witness-category/my-witness",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT83T4B5vezp5b4y4pYfScdpL9MoeGsGXDrSZ7X4H98igXxm3Ai6",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 137,
      "owner": "XGTAGB8usZFppemNHZiEovYH6gbimmV3LijaunmmLCm",
      "created": "2021-06-17T11:57:46",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 819821,
      "signing_key": "XGT7eUERmbPvsUSEPyj5AcoKVHEBtejA8yhdENJ4TGnPRXh6uiPXY",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 82,
      "owner": "XGT4bahdxakZEvFP6WkRPAB1i7nvonNwMFqCAuGCEsL",
      "created": "2021-06-13T13:52:46",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 468319,
      "signing_key": "XGT5iLmwogUm52NL4SzCmBWRSqqWBD1SdvzJAQ93FtkZnq4cZnwEj",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 134,
      "owner": "XGTH6aobewk3vBSqhGMMroszhmKFkJ5qMKWgSXhbe4e",
      "created": "2021-06-17T07:44:32",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT8fDuRudA7RXpmcSVADUQqsaLBLtmp7nep1q4DwEjcLxkoRis4G",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 80,
      "owner": "XGTGsTFzDyPZ4RVdff6NG5Prf2Xx2NGoMRYWy7ScF2x",
      "created": "2021-06-13T05:47:05",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 683955,
      "signing_key": "XGT73MUAGRXDQbWJW6wCic2izm3u5B2dNZYYRQQDbnYZQGAe5gTs6",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 18,
      "owner": "XGTE6QyxE5fwfcCYNL6hdT7LwsKDZtjgMSZ6mYsksEx",
      "created": "2021-06-07T22:47:52",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT8BgCaM7DXhdZfxiW3TfGW1adyt8ZiGLQxqozwWYEKAzX5h1FjH",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 22,
      "owner": "XGTDyNCcpwZ1GcVwvdJ5CH4Mg1NDkvfzN4ZMQ4jZg1T",
      "created": "2021-06-07T23:06:30",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 7979,
      "signing_key": "XGT51KqT1syZd8PRwSgctzzFA36e4vEuzpkkCdM92jiAhUNDgvqV9",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 161,
      "owner": "XGTGM4ZSF4RhMvtLFLzDQvwihP9nwEz8NrqFyRqRebH",
      "created": "2021-06-25T19:56:10",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT8mAJsc78n21FCZA32z4KMSskc8Z7hddS8ag1YzWJD8kJxvTEMh",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 84,
      "owner": "XGT95X6s2PtSUjVSfLsrTEusrqmHQBXANy66mnc9EpZ",
      "created": "2021-06-14T04:02:15",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 555329,
      "signing_key": "XGT7yzyTr6gTBAs4fzDDC7TtPbAsYMG6iw82ACttt6GyTMRfFQfnw",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 97,
      "owner": "XGTDZatHRi3cCoebySHz6iV8p4DoWQhjQQMJSJ9kwTD",
      "created": "2021-06-14T20:45:27",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 1329609,
      "signing_key": "XGT7MT4mHCEjJGongH65zmTeM4Vsp9WnbJ9MQ3WraqD7XTnPZEw6H",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 1,
      "owner": "XGTFPni4anwm5sUCULerBG86f2JhYYZVQWBH5mNAahA",
      "created": "2021-06-07T21:26:43",
      "url": "http://witness-category/my-witness",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 239808,
      "signing_key": "XGT7kCfG7NctddZbQeoYxF6vimfmvGwi9zLzuDgS1J1NwCYQeMYa2",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 122,
      "owner": "XGT6Wmv5vGXbLkAHtrnu6LfairtZuXYkQb3cV6h65XY",
      "created": "2021-06-16T14:59:18",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 483002,
      "signing_key": "XGT68FQi1N5q3qeySuQSJZLoPwxxxzVnyNb7KSUWqoTcxAob7dWUy",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 57,
      "owner": "XGT8ZvVEhahVK4fFLXtk5oEQnS1FSNHHQgkwBcDerZv",
      "created": "2021-06-08T09:29:38",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT7ZUrm7HCJtcfw4Pn3bEznBo8z6SnVESYzop7u6keEzmKUZYYWB",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 114,
      "owner": "XGT36yrBZ5PbXV8BiZR3Cu25K6oT2TpSQyEeUN16C3d",
      "created": "2021-06-15T16:02:14",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT6259eHBiZzEj4wmyNfcFkikD89WRu2mSf5rMNjQJgPY7gXEPVP",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 160,
      "owner": "XGT64EytQ9MRzKti5EkdvwdX5a9vmButRGBbrsqA6he",
      "created": "2021-06-23T22:39:39",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT6rTEgrD54jrMmhbyJG8oA9pWBdc2GdEippPbKKwd5YULAxJ4XG",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 28,
      "owner": "XGTHcsayM9TRs2Xpcpd7BmXRfE3rpJiHRRFvqW3Cz6d",
      "created": "2021-06-08T01:12:34",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 587137,
      "signing_key": "XGT7C3yd4uZqbEqz6vsG9iF4ncHWZGjNPXQnordnprkdX11XRVeqS",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 100,
      "owner": "XGT7r8PnSkmow33DemPGx26JHHQuiwQpRZGNdgBNQi7",
      "created": "2021-06-15T06:03:09",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 479777,
      "signing_key": "XGT8jyAiWXvnxJfPdYkE176C1mzne7ZTqAa2Hsp6ZNJhi4yG9cq8Y",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 19,
      "owner": "XGTH8DDftgzsxf1ag7Pz4nqEGXecBAGbRycmgzKmSgJ",
      "created": "2021-06-07T22:50:56",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT8bQ3uaVenR1PRiaWDPEacxkxWnoRUVzjo57i956hfrBm7pn5HN",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 53,
      "owner": "XGT3DiQVdjMeNbMQk6EnnLXwKQXkZnFjS1asKq5zzL8",
      "created": "2021-06-08T07:31:17",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 1337125,
      "signing_key": "XGT5tnT1MbgAfgYKZBKJB2pzEdybqnGiqAvLSFvJjw6ubvQZSfiFZ",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 92,
      "owner": "XGTB5jjv7H2jSZZcvT9B8eWCAQfHpjd4S3PrS4YCzjy",
      "created": "2021-06-14T16:07:56",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT6yGpicoR7ePd2zW4mmSesB4dpRbyfBM68SLaNLY1j3FKwC3KxW",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 33,
      "owner": "XGT4vpiys9doDjNs7VkQo9R3tzeHtBPESJWfTS9wf7L",
      "created": "2021-06-08T04:46:38",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 1340691,
      "signing_key": "XGT8Sc7A6FRDVpATV3e8UczDdNbTfE7nDFhf3dFgTdpDiMXPxbu3M",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 135,
      "owner": "XGT7RcPWgPxns6cATdiyobhLcRn2G4RWSbxKjSxgy95",
      "created": "2021-06-17T08:29:54",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 1308870,
      "signing_key": "XGT8axjvBzbX9REKw5qHdEYGXXSJxGoxPnFsYtT7B2MntJoraYBaW",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 127,
      "owner": "XGTFfrJjYqnmsMJAvNW9fEwQBAeQ6FUfSkr4vPKXoZr",
      "created": "2021-06-16T17:02:44",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 513296,
      "signing_key": "XGT8icDmD63rPh52syH97PDbxbpJhhm8quDJLe3hnq8xbqJN2HzYR",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 35,
      "owner": "XGTEKuKqWGS2yLrrLZwNYkAHkbbC5GzQSrzeyfcxoLc",
      "created": "2021-06-08T05:14:25",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 495707,
      "signing_key": "XGT6UcVQwtSf9kWQWFZ5MV2oCdntgwF3dintvZ9JAMWSEk3sB1MPL",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 151,
      "owner": "XGT7sDmwy14meJpdoAK5iXnZsDz7F6XKSsNvuTxFE3z",
      "created": "2021-06-18T16:08:07",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 644768,
      "signing_key": "XGT7FtCXD86i3ULTE6qWAi14feXZZpgHagWM3EbL9z3Z9VKiaPH3L",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 120,
      "owner": "XGT2rt23Je3YCfxkAzVjVT8c8V7wrC8uTA28u5xFKub",
      "created": "2021-06-16T00:34:53",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 606212,
      "signing_key": "XGT8ddFc3FisKKnGxyJgcKtTyd4o17PF6T8RJMmuZRsnMCd6Ar3Sw",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 144,
      "owner": "XGT4h2wpXLY4UxuTkU2iZaknnfo387YeTuCk233ky3z",
      "created": "2021-06-17T21:48:38",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 485940,
      "signing_key": "XGT6AgHdm62qN7VZHB1gn6NMupeYG5SSuKgbuPLMr5jv3g62gAQG8",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 78,
      "owner": "XGTGLXqgd6UmY6WzJ1kWwi2ebgVQQbonTxL3HNXzKVd",
      "created": "2021-06-13T05:43:35",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT8UBFEHBXKVXjrhwFK6ScEfkXCZJK9iYrCHt6sZyvQro6sASfCq",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 74,
      "owner": "XGTDMmRMPHchj37Ch9s5EFwmLinTupnjUB2de5WxxDV",
      "created": "2021-06-11T15:53:57",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT7MtN8Rbyi1eajRTNQVZTYn4oWn4vnnTBwgAD6RPuwS6XWk7V2G",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 129,
      "owner": "XGTEuj5wZeZzcCdeCoXdNEetsb73wGX2Uq7uLtsXQKf",
      "created": "2021-06-16T23:13:36",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 1340639,
      "signing_key": "XGT82Gm6dzPSKM51Y8S2pXUmFqsKn5dVbZcREkUX1iM6sMTnZriZq",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 138,
      "owner": "XGT76iGsFSnQQ2uUPwey7Dz5r94aBZFnVRogkkF3f1S",
      "created": "2021-06-17T12:48:51",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 601973,
      "signing_key": "XGT58kX5Lm1GJmXR3eQnyJTyAe64gvt1keTRBbo3LYeNSQEp2Mmb1",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 109,
      "owner": "XGTGvpMqyd5GNA2cZpndWYKgvABwfAACVWN9roSvNWv",
      "created": "2021-06-15T12:27:54",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT7regEctNxfmRg6GjYYevHKPQFSzYfe2NxmeRVmjKCLYnb9vNLu",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 118,
      "owner": "XGT2zieEsiFWCxGM3n8QNXo5HrhrgAfDVyxCjfc78Uj",
      "created": "2021-06-15T21:27:22",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 607343,
      "signing_key": "XGT5ffVs13jG5aycuthKHVjYKQc9GWE28eQ6ZaGcrFnwvGKCiRqnb",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 38,
      "owner": "XGTEuY8PS61orxrxARwwDqntRDoCn1WxW1RNmxHDBsq",
      "created": "2021-06-08T06:04:18",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT72UZikvTLJxaLtsb7gpfhu4bSMLRTavYZRbvaPDe99QhSuo4Lf",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 111,
      "owner": "XGT2KWs9XGDRvv5GCDh1piv3JbPZuN1WWAPtKVqLAdt",
      "created": "2021-06-15T12:42:08",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT6gLfM4RSKz3vLdchrWpEQB7NXPRgXT14JEAhvJM6JuKAPQFoA6",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 90,
      "owner": "XGT7Dz34yUW7TsBUzDRrcpxJXSejPHZQWjF4sBxoPxa",
      "created": "2021-06-14T14:52:31",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT6gStUQ7LQcQFLZNtU18EXgV5MqZ2Tr4wnkRHkCUgKvPNoTbgPB",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 113,
      "owner": "XGTD87g6gUghdMMfNg3rtuEPxjTvPQAXX3fo31Zfau2",
      "created": "2021-06-15T13:26:32",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 701914,
      "signing_key": "XGT4z8WnYNurt2JpYkUKTumDPKpaepws6MAwkrVwbKo5by9s5Wn7r",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 119,
      "owner": "XGT52idQKLaWE9hdTDrjXdYNLLc3mBwGXP4eG9ekfGa",
      "created": "2021-06-15T23:47:24",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT8KCchMegPqMAs3WxumyKbQLZ2U9FwDmW5TiT8k7bT3EkZFsfhh",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 110,
      "owner": "XGT6QFaQGxwzQRxuZGvtX7qucwycXmJtXpa5EbWLfmA",
      "created": "2021-06-15T12:34:14",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT7YTfsmBCtY4jxQSURfTr11PxwfnrVcgf4fHkWY6TgCGL9iWUie",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 15,
      "owner": "XGTGYS6fFkS6gBG8VfT7gETtkRhEzbDXXzJDNQyrRFy",
      "created": "2021-06-07T22:36:40",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 887371,
      "signing_key": "XGT5JM1dHS93s58MsUmnwG32TAgduNoEMx36YbxnazXAMpuUCY24H",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 6,
      "owner": "XGTH9SiLMzsWFYR1bP9NkJLWb3TiMzptYCVpvLuWGPb",
      "created": "2021-06-07T21:37:08",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 19012,
      "signing_key": "XGT7omA6LKxAUF25PLHiEujGAP7mVACHXRPTNd8iof8xoNuys28sG",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 159,
      "owner": "XGT22C4t3EojFeEd5B9JXGp8RbuizAPdYM6ZMiyyZ6a",
      "created": "2021-06-23T19:50:31",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 579475,
      "signing_key": "XGT7A5822rbS5aAh1rvChdHYuciqy7MCnSL3DPchVfEUnCuKxpGKu",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 3,
      "owner": "XGTGmzVNN1ucwYWhSQKUyG5wuaGXvhjzZ25sf41WV6B",
      "created": "2021-06-07T21:29:00",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 1340699,
      "signing_key": "XGT6gRy5TJTibrsdLkQQLTkBTrKbeHvxbVBEvJA5wJiiGgZXN8T3h",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    },
    {
      "id": 10,
      "owner": "XGTDco6nNwVPohJ2a4nTyutoMJJ2T5LmZBmf4NYw1pj",
      "created": "2021-06-07T22:01:27",
      "url": "http://test.host",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 0,
      "signing_key": "XGT84vuo4pgd494jWqoVzdZ9ktav7CTxoyYFGQLMujatgny4xrvTG",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    }
  ]
}
```

---

### Procedure:  find_witnesses
Returns a list of witnesses corresponding to inputted wallet addresses.
#### Arguments
* Vector<String> `miners` - _List of wallet addresses to retreive associated witnesses._
#### Example JSON Payload Format
```javascript
{
  miners: [
    'XGT0000000000000000000000000000000000000000'
  ]
}
```
#### Example JSON Response
```javascript
{
  "miners": [
    {
      "id": 0,
      "owner": "XGT0000000000000000000000000000000000000000",
      "created": "1970-01-01T00:00:00",
      "url": "",
      "votes": 0,
      "virtual_last_update": "0",
      "virtual_position": "0",
      "virtual_scheduled_time": "340282366920938463463374607431768211455",
      "total_missed": 0,
      "last_aslot": 0,
      "last_confirmed_block_num": 0,
      "pow_worker": 93538,
      "signing_key": "XGT7dDoJbrmueAw431pPbjLDoRhqFCC5Xs5o6f1cZLepWEpkcy3Tc",
      "props": {
        "account_creation_fee": {
          "amount": "0",
          "precision": 8,
          "nai": "@@000000021"
        },
        "maximum_block_size": 131072
      },
      "last_work": "0000000000000000000000000000000000000000000000000000000000000000",
      "running_version": "0.0.0",
      "hardfork_version_vote": "0.0.0",
      "hardfork_time_vote": "2020-04-14T04:53:35"
    }
  ]
}
```

-------------------------------------------------------------------------------

## Wallets

### Procedure:  list_wallets
List wallets ordered by specified key.
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
{
  "wallets": [
    {
      "id": 1,
      "name": "XGT0000000000000000000000000000000000000000",
      "recovery": {
        "weight_threshold": 1,
        "wallet_auths": [

        ],
        "key_auths": [
          [
            "XGT7dDoJbrmueAw431pPbjLDoRhqFCC5Xs5o6f1cZLepWEpkcy3Tc",
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
            "XGT7dDoJbrmueAw431pPbjLDoRhqFCC5Xs5o6f1cZLepWEpkcy3Tc",
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
            "XGT7dDoJbrmueAw431pPbjLDoRhqFCC5Xs5o6f1cZLepWEpkcy3Tc",
            1
          ]
        ]
      },
      "memo_key": "XGT7dDoJbrmueAw431pPbjLDoRhqFCC5Xs5o6f1cZLepWEpkcy3Tc",
      "json_metadata": "",
      "social_json_metadata": "",
      "last_recovery_update": "1970-01-01T00:00:00",
      "last_account_update": "1970-01-01T00:00:00",
      "created": "1970-01-01T00:00:00",
      "mined": true,
      "recovery_account": "",
      "last_account_recovery": "1970-01-01T00:00:00",
      "reset_account": "XGT0000000000000000000000000000000000000002",
      "comment_count": 0,
      "lifetime_vote_count": 0,
      "post_count": 0,
      "can_vote": true,
      "energybar": {
        "current_energy": 0,
        "last_update_time": 0
      },
      "balance": {
        "amount": "1873016361281114",
        "precision": 8,
        "nai": "@@000000021"
      },
      "witnesses_voted_for": 0,
      "last_post": "1970-01-01T00:00:00",
      "last_root_post": "1970-01-01T00:00:00",
      "last_post_edit": "1970-01-01T00:00:00",
      "last_vote_time": "1970-01-01T00:00:00",
      "post_bandwidth": 0,
      "is_xtt": false
    },
    {
      "id": 0,
      "name": "XGT0000000000000000000000000000000000000001",
      "recovery": {
        "weight_threshold": 1,
        "wallet_auths": [

        ],
        "key_auths": [

        ]
      },
      "money": {
        "weight_threshold": 1,
        "wallet_auths": [

        ],
        "key_auths": [

        ]
      },
      "social": {
        "weight_threshold": 0,
        "wallet_auths": [

        ],
        "key_auths": [

        ]
      },
      "memo_key": "XGT1111111111111111111111111111111114T1Anm",
      "json_metadata": "",
      "social_json_metadata": "",
      "last_recovery_update": "1970-01-01T00:00:00",
      "last_account_update": "1970-01-01T00:00:00",
      "created": "1970-01-01T00:00:00",
      "mined": true,
      "recovery_account": "",
      "last_account_recovery": "1970-01-01T00:00:00",
      "reset_account": "XGT0000000000000000000000000000000000000002",
      "comment_count": 0,
      "lifetime_vote_count": 0,
      "post_count": 0,
      "can_vote": true,
      "energybar": {
        "current_energy": 0,
        "last_update_time": 0
      },
      "balance": {
        "amount": "0",
        "precision": 8,
        "nai": "@@000000021"
      },
      "witnesses_voted_for": 0,
      "last_post": "1970-01-01T00:00:00",
      "last_root_post": "1970-01-01T00:00:00",
      "last_post_edit": "1970-01-01T00:00:00",
      "last_vote_time": "1970-01-01T00:00:00",
      "post_bandwidth": 0,
      "is_xtt": false
    },
    {
      "id": 2,
      "name": "XGT0000000000000000000000000000000000000002",
      "recovery": {
        "weight_threshold": 1,
        "wallet_auths": [

        ],
        "key_auths": [

        ]
      },
      "money": {
        "weight_threshold": 1,
        "wallet_auths": [

        ],
        "key_auths": [

        ]
      },
      "social": {
        "weight_threshold": 0,
        "wallet_auths": [

        ],
        "key_auths": [

        ]
      },
      "memo_key": "XGT1111111111111111111111111111111114T1Anm",
      "json_metadata": "",
      "social_json_metadata": "",
      "last_recovery_update": "1970-01-01T00:00:00",
      "last_account_update": "1970-01-01T00:00:00",
      "created": "1970-01-01T00:00:00",
      "mined": true,
      "recovery_account": "",
      "last_account_recovery": "1970-01-01T00:00:00",
      "reset_account": "XGT0000000000000000000000000000000000000002",
      "comment_count": 0,
      "lifetime_vote_count": 0,
      "post_count": 0,
      "can_vote": true,
      "energybar": {
        "current_energy": 0,
        "last_update_time": 0
      },
      "balance": {
        "amount": "0",
        "precision": 8,
        "nai": "@@000000021"
      },
      "witnesses_voted_for": 0,
      "last_post": "1970-01-01T00:00:00",
      "last_root_post": "1970-01-01T00:00:00",
      "last_post_edit": "1970-01-01T00:00:00",
      "last_vote_time": "1970-01-01T00:00:00",
      "post_bandwidth": 0,
      "is_xtt": false
    },
    {
      "id": 4,
      "name": "XGT0000000000000000000000000000000000000003",
      "recovery": {
        "weight_threshold": 0,
        "wallet_auths": [

        ],
        "key_auths": [

        ]
      },
      "money": {
        "weight_threshold": 0,
        "wallet_auths": [

        ],
        "key_auths": [

        ]
      },
      "social": {
        "weight_threshold": 0,
        "wallet_auths": [

        ],
        "key_auths": [

        ]
      },
      "memo_key": "XGT1111111111111111111111111111111114T1Anm",
      "json_metadata": "",
      "social_json_metadata": "",
      "last_recovery_update": "1970-01-01T00:00:00",
      "last_account_update": "1970-01-01T00:00:00",
      "created": "1970-01-01T00:00:00",
      "mined": true,
      "recovery_account": "",
      "last_account_recovery": "1970-01-01T00:00:00",
      "reset_account": "XGT0000000000000000000000000000000000000002",
      "comment_count": 0,
      "lifetime_vote_count": 0,
      "post_count": 0,
      "can_vote": true,
      "energybar": {
        "current_energy": 0,
        "last_update_time": 0
      },
      "balance": {
        "amount": "0",
        "precision": 8,
        "nai": "@@000000021"
      },
      "witnesses_voted_for": 0,
      "last_post": "1970-01-01T00:00:00",
      "last_root_post": "1970-01-01T00:00:00",
      "last_post_edit": "1970-01-01T00:00:00",
      "last_vote_time": "1970-01-01T00:00:00",
      "post_bandwidth": 0,
      "is_xtt": false
    }
  ]
}
```
---

### Procedure:  find_wallets
Returns list of wallets if inputted wallet addresses exist.
#### Variables

#### Arguments
* Array of Strings `wallets` - _Wallet addresses to search for._
#### Example JSON Payload Format
```javascript
{
  wallets: [
    'XGT0000000000000000000000000000000000000000'
  ]
}
```
#### Example JSON Response
```javascript
{
  "wallets": [
    {
      "id": 1,
      "name": "XGT0000000000000000000000000000000000000000",
      "recovery": {
        "weight_threshold": 1,
        "wallet_auths": [

        ],
        "key_auths": [
          [
            "XGT7dDoJbrmueAw431pPbjLDoRhqFCC5Xs5o6f1cZLepWEpkcy3Tc",
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
            "XGT7dDoJbrmueAw431pPbjLDoRhqFCC5Xs5o6f1cZLepWEpkcy3Tc",
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
            "XGT7dDoJbrmueAw431pPbjLDoRhqFCC5Xs5o6f1cZLepWEpkcy3Tc",
            1
          ]
        ]
      },
      "memo_key": "XGT7dDoJbrmueAw431pPbjLDoRhqFCC5Xs5o6f1cZLepWEpkcy3Tc",
      "json_metadata": "",
      "social_json_metadata": "",
      "last_recovery_update": "1970-01-01T00:00:00",
      "last_account_update": "1970-01-01T00:00:00",
      "created": "1970-01-01T00:00:00",
      "mined": true,
      "recovery_account": "",
      "last_account_recovery": "1970-01-01T00:00:00",
      "reset_account": "XGT0000000000000000000000000000000000000002",
      "comment_count": 0,
      "lifetime_vote_count": 0,
      "post_count": 0,
      "can_vote": true,
      "energybar": {
        "current_energy": 0,
        "last_update_time": 0
      },
      "balance": {
        "amount": "1873016361281114",
        "precision": 8,
        "nai": "@@000000021"
      },
      "witnesses_voted_for": 0,
      "last_post": "1970-01-01T00:00:00",
      "last_root_post": "1970-01-01T00:00:00",
      "last_post_edit": "1970-01-01T00:00:00",
      "last_vote_time": "1970-01-01T00:00:00",
      "post_bandwidth": 0,
      "is_xtt": false
    }
  ]
}
```

---

### Procedure:  list_escrows
List wallets ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns

#### Example JSON Payload Format
```javascript
payload = {
  from: 'XGT0000000000000000000000000000000000000000'
}
```
#### Example JSON Response
```javascript
{
  "escrows": [

  ]
}
```

---

### Procedure:  find_escrows
List wallets ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  list_withdraw_vesting_routes
List wallets ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  find_withdraw_vesting_routes
List wallets ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  list_savings_withdrawals
List wallets ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  find_savings_withdrawals
List wallets ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  list_vesting_delegations
List wallets ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  find_vesting_delegations
List wallets ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  list_vesting_delegation_expirations
List wallets ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  find_vesting_delegation_expirations
List wallets ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  list_sbd_conversion_requests
List wallets ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  find_sbd_conversion_requests
List wallets ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  list_decline_voting_rights_requests
List wallets ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  find_decline_voting_rights_requests
List wallets ordered by specified key
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
List wallets ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  find_comments
List wallets ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  list_votes
List wallets ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  find_votes
List wallets ordered by specified key
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
List wallets ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  find_limit_orders
List wallets ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  get_order_book
List wallets ordered by specified key
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
List wallets ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  find_proposals
List wallets ordered by specified key
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  list_proposal_votes
List wallets ordered by specified key
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
This is a general purpose API that checks signatures against wallets for an
arbitrary sha256 hash using the existing authority structures in Steem
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

-------------------------------------------------------------------------------

## XTTs

### Procedure:  get_nai_pool
@return array of Numeric Asset Identifier (NAI) available to be used for new
XTTs to be created.
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  list_xtt_contributions
description
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  find_xtt_contributions
description#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  list_xtt_tokens
description#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  find_xtt_tokens
description
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  list_xtt_token_emissions
description
#### Arguments
* String `arg1` - _Description_
* UInt8 `arg2` - _Description_
#### Returns
```javascript
// some example code
```

---

### Procedure:  find_xtt_token_emissions
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

