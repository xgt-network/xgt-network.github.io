# XGT Schema outline

```json
{
    "schema_map": {
        "bip::flat_map<xgt::protocol::fixed_string<32>,uint16_t>": {
            "deps": [
                "xgt::protocol::fixed_string<32>",
                "uint16_t"
            ],
            "schema": {
                "name": "bip::flat_map<xgt::protocol::fixed_string<32>,uint16_t>",
                "type": "map",
                "ktype": "xgt::protocol::fixed_string<32>",
                "vtype": "uint16_t"
            }
        },
        "bool": {
            "deps": [],
            "schema": {
                "name": "bool",
                "type": "prim"
            }
        },
        "char": {
            "deps": [],
            "schema": {
                "name": "char",
                "type": "prim"
            }
        },
        "fc::array<char,33>": {
            "deps": [],
            "schema": {
                "name": "fc::array<char,33>",
                "type": "prim"
            }
        },
        "fc::array<uint8_t,65>": {
            "deps": [],
            "schema": {
                "name": "fc::array<uint8_t,65>",
                "type": "prim"
            }
        },
        "fc::sha256": {
            "deps": [],
            "schema": {
                "name": "fc::sha256",
                "type": "prim"
            }
        },
        "fc::static_variant<xgt::protocol::xtt_capped_generation_policy>": {
            "deps": [
                "xgt::protocol::xtt_capped_generation_policy"
            ],
            "schema": {
                "name": "fc::static_variant<xgt::protocol::xtt_capped_generation_policy>",
                "type": "static_variant",
                "etypes": [
                    "xgt::protocol::xtt_capped_generation_policy"
                ]
            }
        },
        "fc::time_point_sec": {
            "deps": [],
            "schema": {
                "name": "fc::time_point_sec",
                "type": "prim"
            }
        },
        "flat_set<xgt::protocol::block_header_extensions>": {
            "deps": [
                "xgt::protocol::block_header_extensions"
            ],
            "schema": {
                "name": "flat_set<xgt::protocol::block_header_extensions>",
                "type": "set",
                "etype": "xgt::protocol::block_header_extensions"
            }
        },
        "flat_set<xgt::protocol::future_extensions>": {
            "deps": [
                "xgt::protocol::future_extensions"
            ],
            "schema": {
                "name": "flat_set<xgt::protocol::future_extensions>",
                "type": "set",
                "etype": "xgt::protocol::future_extensions"
            }
        },
        "flat_set<xgt::protocol::wallet_name_type>": {
            "deps": [
                "xgt::protocol::wallet_name_type"
            ],
            "schema": {
                "name": "flat_set<xgt::protocol::wallet_name_type>",
                "type": "set",
                "etype": "xgt::protocol::wallet_name_type"
            }
        },
        "flat_set<xgt::protocol::xtt_runtime_parameter>": {
            "deps": [
                "xgt::protocol::xtt_runtime_parameter"
            ],
            "schema": {
                "name": "flat_set<xgt::protocol::xtt_runtime_parameter>",
                "type": "set",
                "etype": "xgt::protocol::xtt_runtime_parameter"
            }
        },
        "flat_set<xgt::protocol::xtt_setup_parameter>": {
            "deps": [
                "xgt::protocol::xtt_setup_parameter"
            ],
            "schema": {
                "name": "flat_set<xgt::protocol::xtt_setup_parameter>",
                "type": "set",
                "etype": "xgt::protocol::xtt_setup_parameter"
            }
        },
        "int64_t": {
            "deps": [],
            "schema": {
                "name": "int64_t",
                "type": "prim"
            }
        },
        "optional<xgt::protocol::authority>": {
            "deps": [
                "xgt::protocol::authority"
            ],
            "schema": {
                "name": "optional<xgt::protocol::authority>",
                "type": "optional",
                "etype": "xgt::protocol::authority"
            }
        },
        "optional<xgt::protocol::public_key_type>": {
            "deps": [
                "xgt::protocol::public_key_type"
            ],
            "schema": {
                "name": "optional<xgt::protocol::public_key_type>",
                "type": "optional",
                "etype": "xgt::protocol::public_key_type"
            }
        },
        "std::vector<char>": {
            "deps": [
                "char"
            ],
            "schema": {
                "name": "std::vector<char>",
                "type": "list",
                "etype": "char"
            }
        },
        "std::vector<fc::array<uint8_t,65>>": {
            "deps": [
                "fc::array<uint8_t,65>"
            ],
            "schema": {
                "name": "std::vector<fc::array<uint8_t,65>>",
                "type": "list",
                "etype": "fc::array<uint8_t,65>"
            }
        },
        "std::vector<std::vector<char>>": {
            "deps": [
                "std::vector<char>"
            ],
            "schema": {
                "name": "std::vector<std::vector<char>>",
                "type": "list",
                "etype": "std::vector<char>"
            }
        },
        "std::vector<xgt::protocol::asset>": {
            "deps": [
                "xgt::protocol::asset"
            ],
            "schema": {
                "name": "std::vector<xgt::protocol::asset>",
                "type": "list",
                "etype": "xgt::protocol::asset"
            }
        },
        "std::vector<xgt::protocol::operation>": {
            "deps": [
                "xgt::protocol::operation"
            ],
            "schema": {
                "name": "std::vector<xgt::protocol::operation>",
                "type": "list",
                "etype": "xgt::protocol::operation"
            }
        },
        "std::vector<xgt::protocol::optional_automated_action>": {
            "deps": [
                "xgt::protocol::optional_automated_action"
            ],
            "schema": {
                "name": "std::vector<xgt::protocol::optional_automated_action>",
                "type": "list",
                "etype": "xgt::protocol::optional_automated_action"
            }
        },
        "std::vector<xgt::protocol::required_automated_action>": {
            "deps": [
                "xgt::protocol::required_automated_action"
            ],
            "schema": {
                "name": "std::vector<xgt::protocol::required_automated_action>",
                "type": "list",
                "etype": "xgt::protocol::required_automated_action"
            }
        },
        "std::vector<xgt::protocol::signed_transaction>": {
            "deps": [
                "xgt::protocol::signed_transaction"
            ],
            "schema": {
                "name": "std::vector<xgt::protocol::signed_transaction>",
                "type": "list",
                "etype": "xgt::protocol::signed_transaction"
            }
        },
        "string": {
            "deps": [],
            "schema": {
                "name": "string",
                "type": "prim"
            }
        },
        "uint160_t": {
            "deps": [],
            "schema": {
                "name": "uint160_t",
                "type": "prim"
            }
        },
        "uint16_t": {
            "deps": [],
            "schema": {
                "name": "uint16_t",
                "type": "prim"
            }
        },
        "uint32_t": {
            "deps": [],
            "schema": {
                "name": "uint32_t",
                "type": "prim"
            }
        },
        "uint64_t": {
            "deps": [],
            "schema": {
                "name": "uint64_t",
                "type": "prim"
            }
        },
        "uint8_t": {
            "deps": [],
            "schema": {
                "name": "uint8_t",
                "type": "prim"
            }
        },
        "xgt::protocol::asset": {
            "deps": [
                "xgt::protocol::share_type",
                "xgt::protocol::asset_symbol_type"
            ],
            "schema": {
                "name": "xgt::protocol::asset",
                "type": "class",
                "members": [
                    [
                        "xgt::protocol::share_type",
                        "amount"
                    ],
                    [
                        "xgt::protocol::asset_symbol_type",
                        "symbol"
                    ]
                ]
            }
        },
        "xgt::protocol::asset_symbol_type": {
            "deps": [],
            "schema": {
                "name": "xgt::protocol::asset_symbol_type",
                "type": "asset_symbol_type"
            }
        },
        "xgt::protocol::authority": {
            "deps": [
                "uint32_t",
                "xgt::protocol::authority::wallet_authority_map",
                "xgt::protocol::authority::key_authority_map"
            ],
            "schema": {
                "name": "xgt::protocol::authority",
                "type": "class",
                "members": [
                    [
                        "uint32_t",
                        "weight_threshold"
                    ],
                    [
                        "xgt::protocol::authority::wallet_authority_map",
                        "wallet_auths"
                    ],
                    [
                        "xgt::protocol::authority::key_authority_map",
                        "key_auths"
                    ]
                ]
            }
        },
        "xgt::protocol::authority::key_authority_map": {
            "deps": [
                "xgt::protocol::public_key_type",
                "uint16_t"
            ],
            "schema": {
                "name": "xgt::protocol::authority::key_authority_map",
                "type": "map",
                "ktype": "xgt::protocol::public_key_type",
                "vtype": "uint16_t"
            }
        },
        "xgt::protocol::authority::wallet_authority_map": {
            "deps": [
                "xgt::protocol::wallet_name_type",
                "uint16_t"
            ],
            "schema": {
                "name": "xgt::protocol::authority::wallet_authority_map",
                "type": "map",
                "ktype": "xgt::protocol::wallet_name_type",
                "vtype": "uint16_t"
            }
        },
        "xgt::protocol::block_header_extensions": {
            "deps": [
                "xgt::void_t",
                "xgt::protocol::version",
                "xgt::protocol::hardfork_version_vote",
                "std::vector<xgt::protocol::required_automated_action>",
                "std::vector<xgt::protocol::optional_automated_action>"
            ],
            "schema": {
                "name": "xgt::protocol::block_header_extensions",
                "type": "static_variant",
                "etypes": [
                    "xgt::void_t",
                    "xgt::protocol::version",
                    "xgt::protocol::hardfork_version_vote",
                    "std::vector<xgt::protocol::required_automated_action>",
                    "std::vector<xgt::protocol::optional_automated_action>"
                ]
            }
        },
        "xgt::protocol::change_recovery_wallet_operation": {
            "deps": [
                "xgt::protocol::wallet_name_type",
                "xgt::protocol::wallet_name_type",
                "flat_set<xgt::protocol::future_extensions>"
            ],
            "schema": {
                "name": "xgt::protocol::change_recovery_wallet_operation",
                "type": "class",
                "members": [
                    [
                        "xgt::protocol::wallet_name_type",
                        "account_to_recover"
                    ],
                    [
                        "xgt::protocol::wallet_name_type",
                        "new_recovery_account"
                    ],
                    [
                        "flat_set<xgt::protocol::future_extensions>",
                        "extensions"
                    ]
                ]
            }
        },
        "xgt::protocol::clear_null_wallet_balance_operation": {
            "deps": [
                "std::vector<xgt::protocol::asset>"
            ],
            "schema": {
                "name": "xgt::protocol::clear_null_wallet_balance_operation",
                "type": "class",
                "members": [
                    [
                        "std::vector<xgt::protocol::asset>",
                        "total_cleared"
                    ]
                ]
            }
        },
        "xgt::protocol::comment_operation": {
            "deps": [
                "xgt::protocol::wallet_name_type",
                "string",
                "xgt::protocol::wallet_name_type",
                "string",
                "string",
                "string",
                "string"
            ],
            "schema": {
                "name": "xgt::protocol::comment_operation",
                "type": "class",
                "members": [
                    [
                        "xgt::protocol::wallet_name_type",
                        "parent_author"
                    ],
                    [
                        "string",
                        "parent_permlink"
                    ],
                    [
                        "xgt::protocol::wallet_name_type",
                        "author"
                    ],
                    [
                        "string",
                        "permlink"
                    ],
                    [
                        "string",
                        "title"
                    ],
                    [
                        "string",
                        "body"
                    ],
                    [
                        "string",
                        "json_metadata"
                    ]
                ]
            }
        },
        "xgt::protocol::comment_options_operation": {
            "deps": [
                "xgt::protocol::wallet_name_type",
                "string",
                "bool"
            ],
            "schema": {
                "name": "xgt::protocol::comment_options_operation",
                "type": "class",
                "members": [
                    [
                        "xgt::protocol::wallet_name_type",
                        "author"
                    ],
                    [
                        "string",
                        "permlink"
                    ],
                    [
                        "bool",
                        "allow_votes"
                    ]
                ]
            }
        },
        "xgt::protocol::contract_create_operation": {
            "deps": [
                "xgt::protocol::wallet_name_type",
                "std::vector<char>"
            ],
            "schema": {
                "name": "xgt::protocol::contract_create_operation",
                "type": "class",
                "members": [
                    [
                        "xgt::protocol::wallet_name_type",
                        "owner"
                    ],
                    [
                        "std::vector<char>",
                        "code"
                    ]
                ]
            }
        },
        "xgt::protocol::contract_invoke_operation": {
            "deps": [
                "xgt::protocol::wallet_name_type",
                "uint160_t",
                "std::vector<std::vector<char>>"
            ],
            "schema": {
                "name": "xgt::protocol::contract_invoke_operation",
                "type": "class",
                "members": [
                    [
                        "xgt::protocol::wallet_name_type",
                        "caller"
                    ],
                    [
                        "uint160_t",
                        "contract_hash"
                    ],
                    [
                        "std::vector<std::vector<char>>",
                        "args"
                    ]
                ]
            }
        },
        "xgt::protocol::custom_json_operation": {
            "deps": [
                "flat_set<xgt::protocol::wallet_name_type>",
                "flat_set<xgt::protocol::wallet_name_type>",
                "xgt::protocol::fixed_string<32>",
                "string"
            ],
            "schema": {
                "name": "xgt::protocol::custom_json_operation",
                "type": "class",
                "members": [
                    [
                        "flat_set<xgt::protocol::wallet_name_type>",
                        "required_auths"
                    ],
                    [
                        "flat_set<xgt::protocol::wallet_name_type>",
                        "required_social_auths"
                    ],
                    [
                        "xgt::protocol::fixed_string<32>",
                        "id"
                    ],
                    [
                        "string",
                        "json"
                    ]
                ]
            }
        },
        "xgt::protocol::custom_operation": {
            "deps": [
                "flat_set<xgt::protocol::wallet_name_type>",
                "uint16_t",
                "std::vector<char>"
            ],
            "schema": {
                "name": "xgt::protocol::custom_operation",
                "type": "class",
                "members": [
                    [
                        "flat_set<xgt::protocol::wallet_name_type>",
                        "required_auths"
                    ],
                    [
                        "uint16_t",
                        "id"
                    ],
                    [
                        "std::vector<char>",
                        "data"
                    ]
                ]
            }
        },
        "xgt::protocol::delete_comment_operation": {
            "deps": [
                "xgt::protocol::wallet_name_type",
                "string"
            ],
            "schema": {
                "name": "xgt::protocol::delete_comment_operation",
                "type": "class",
                "members": [
                    [
                        "xgt::protocol::wallet_name_type",
                        "author"
                    ],
                    [
                        "string",
                        "permlink"
                    ]
                ]
            }
        },
        "xgt::protocol::escrow_approve_operation": {
            "deps": [
                "xgt::protocol::wallet_name_type",
                "xgt::protocol::wallet_name_type",
                "xgt::protocol::wallet_name_type",
                "xgt::protocol::wallet_name_type",
                "uint32_t",
                "bool"
            ],
            "schema": {
                "name": "xgt::protocol::escrow_approve_operation",
                "type": "class",
                "members": [
                    [
                        "xgt::protocol::wallet_name_type",
                        "from"
                    ],
                    [
                        "xgt::protocol::wallet_name_type",
                        "to"
                    ],
                    [
                        "xgt::protocol::wallet_name_type",
                        "agent"
                    ],
                    [
                        "xgt::protocol::wallet_name_type",
                        "who"
                    ],
                    [
                        "uint32_t",
                        "escrow_id"
                    ],
                    [
                        "bool",
                        "approve"
                    ]
                ]
            }
        },
        "xgt::protocol::escrow_dispute_operation": {
            "deps": [
                "xgt::protocol::wallet_name_type",
                "xgt::protocol::wallet_name_type",
                "xgt::protocol::wallet_name_type",
                "xgt::protocol::wallet_name_type",
                "uint32_t"
            ],
            "schema": {
                "name": "xgt::protocol::escrow_dispute_operation",
                "type": "class",
                "members": [
                    [
                        "xgt::protocol::wallet_name_type",
                        "from"
                    ],
                    [
                        "xgt::protocol::wallet_name_type",
                        "to"
                    ],
                    [
                        "xgt::protocol::wallet_name_type",
                        "agent"
                    ],
                    [
                        "xgt::protocol::wallet_name_type",
                        "who"
                    ],
                    [
                        "uint32_t",
                        "escrow_id"
                    ]
                ]
            }
        },
        "xgt::protocol::escrow_release_operation": {
            "deps": [
                "xgt::protocol::wallet_name_type",
                "xgt::protocol::wallet_name_type",
                "xgt::protocol::wallet_name_type",
                "xgt::protocol::wallet_name_type",
                "xgt::protocol::wallet_name_type",
                "uint32_t",
                "xgt::protocol::asset"
            ],
            "schema": {
                "name": "xgt::protocol::escrow_release_operation",
                "type": "class",
                "members": [
                    [
                        "xgt::protocol::wallet_name_type",
                        "from"
                    ],
                    [
                        "xgt::protocol::wallet_name_type",
                        "to"
                    ],
                    [
                        "xgt::protocol::wallet_name_type",
                        "agent"
                    ],
                    [
                        "xgt::protocol::wallet_name_type",
                        "who"
                    ],
                    [
                        "xgt::protocol::wallet_name_type",
                        "receiver"
                    ],
                    [
                        "uint32_t",
                        "escrow_id"
                    ],
                    [
                        "xgt::protocol::asset",
                        "xgt_amount"
                    ]
                ]
            }
        },
        "xgt::protocol::escrow_transfer_operation": {
            "deps": [
                "xgt::protocol::wallet_name_type",
                "xgt::protocol::wallet_name_type",
                "xgt::protocol::asset",
                "uint32_t",
                "xgt::protocol::wallet_name_type",
                "xgt::protocol::asset",
                "string",
                "fc::time_point_sec",
                "fc::time_point_sec"
            ],
            "schema": {
                "name": "xgt::protocol::escrow_transfer_operation",
                "type": "class",
                "members": [
                    [
                        "xgt::protocol::wallet_name_type",
                        "from"
                    ],
                    [
                        "xgt::protocol::wallet_name_type",
                        "to"
                    ],
                    [
                        "xgt::protocol::asset",
                        "xgt_amount"
                    ],
                    [
                        "uint32_t",
                        "escrow_id"
                    ],
                    [
                        "xgt::protocol::wallet_name_type",
                        "agent"
                    ],
                    [
                        "xgt::protocol::asset",
                        "fee"
                    ],
                    [
                        "string",
                        "json_meta"
                    ],
                    [
                        "fc::time_point_sec",
                        "ratification_deadline"
                    ],
                    [
                        "fc::time_point_sec",
                        "escrow_expiration"
                    ]
                ]
            }
        },
        "xgt::protocol::example_optional_action": {
            "deps": [
                "xgt::protocol::wallet_name_type"
            ],
            "schema": {
                "name": "xgt::protocol::example_optional_action",
                "type": "class",
                "members": [
                    [
                        "xgt::protocol::wallet_name_type",
                        "wallet"
                    ]
                ]
            }
        },
        "xgt::protocol::example_required_action": {
            "deps": [
                "xgt::protocol::wallet_name_type"
            ],
            "schema": {
                "name": "xgt::protocol::example_required_action",
                "type": "class",
                "members": [
                    [
                        "xgt::protocol::wallet_name_type",
                        "account"
                    ]
                ]
            }
        },
        "xgt::protocol::fixed_string<32>": {
            "deps": [],
            "schema": {
                "name": "xgt::protocol::fixed_string<32>",
                "type": "prim"
            }
        },
        "xgt::protocol::fixed_string<8>": {
            "deps": [],
            "schema": {
                "name": "xgt::protocol::fixed_string<8>",
                "type": "prim"
            }
        },
        "xgt::protocol::future_extensions": {
            "deps": [
                "xgt::void_t"
            ],
            "schema": {
                "name": "xgt::protocol::future_extensions",
                "type": "static_variant",
                "etypes": [
                    "xgt::void_t"
                ]
            }
        },
        "xgt::protocol::hardfork_operation": {
            "deps": [
                "uint32_t"
            ],
            "schema": {
                "name": "xgt::protocol::hardfork_operation",
                "type": "class",
                "members": [
                    [
                        "uint32_t",
                        "hardfork_id"
                    ]
                ]
            }
        },
        "xgt::protocol::hardfork_version": {
            "deps": [
                "uint32_t"
            ],
            "schema": {
                "name": "xgt::protocol::hardfork_version",
                "type": "class",
                "members": [
                    [
                        "uint32_t",
                        "v_num"
                    ]
                ]
            }
        },
        "xgt::protocol::hardfork_version_vote": {
            "deps": [
                "xgt::protocol::hardfork_version",
                "fc::time_point_sec"
            ],
            "schema": {
                "name": "xgt::protocol::hardfork_version_vote",
                "type": "class",
                "members": [
                    [
                        "xgt::protocol::hardfork_version",
                        "hf_version"
                    ],
                    [
                        "fc::time_point_sec",
                        "hf_time"
                    ]
                ]
            }
        },
        "xgt::protocol::legacy_chain_properties": {
            "deps": [
                "xgt::protocol::legacy_xgt_asset",
                "uint32_t"
            ],
            "schema": {
                "name": "xgt::protocol::legacy_chain_properties",
                "type": "class",
                "members": [
                    [
                        "xgt::protocol::legacy_xgt_asset",
                        "account_creation_fee"
                    ],
                    [
                        "uint32_t",
                        "maximum_block_size"
                    ]
                ]
            }
        },
        "xgt::protocol::legacy_xgt_asset": {
            "deps": [
                "xgt::protocol::share_type",
                "xgt::protocol::legacy_xgt_asset_symbol_type"
            ],
            "schema": {
                "name": "xgt::protocol::legacy_xgt_asset",
                "type": "class",
                "members": [
                    [
                        "xgt::protocol::share_type",
                        "amount"
                    ],
                    [
                        "xgt::protocol::legacy_xgt_asset_symbol_type",
                        "symbol"
                    ]
                ]
            }
        },
        "xgt::protocol::legacy_xgt_asset_symbol_type": {
            "deps": [],
            "schema": {
                "name": "xgt::protocol::legacy_xgt_asset_symbol_type",
                "type": "prim"
            }
        },
        "xgt::protocol::operation": {
            "deps": [
                "xgt::protocol::comment_operation",
                "xgt::protocol::transfer_operation",
                "xgt::protocol::wallet_create_operation",
                "xgt::protocol::wallet_update_operation",
                "xgt::protocol::witness_update_operation",
                "xgt::protocol::custom_operation",
                "xgt::protocol::report_over_production_operation",
                "xgt::protocol::delete_comment_operation",
                "xgt::protocol::custom_json_operation",
                "xgt::protocol::comment_options_operation",
                "xgt::protocol::request_wallet_recovery_operation",
                "xgt::protocol::recover_wallet_operation",
                "xgt::protocol::change_recovery_wallet_operation",
                "xgt::protocol::escrow_transfer_operation",
                "xgt::protocol::escrow_dispute_operation",
                "xgt::protocol::escrow_release_operation",
                "xgt::protocol::pow_operation",
                "xgt::protocol::escrow_approve_operation",
                "xgt::protocol::vote_operation",
                "xgt::protocol::xtt_setup_operation",
                "xgt::protocol::xtt_setup_ico_tier_operation",
                "xgt::protocol::xtt_set_setup_parameters_operation",
                "xgt::protocol::xtt_set_runtime_parameters_operation",
                "xgt::protocol::xtt_create_operation",
                "xgt::protocol::xtt_contribute_operation",
                "xgt::protocol::shutdown_witness_operation",
                "xgt::protocol::hardfork_operation",
                "xgt::protocol::clear_null_wallet_balance_operation",
                "xgt::protocol::contract_create_operation",
                "xgt::protocol::contract_invoke_operation"
            ],
            "schema": {
                "name": "xgt::protocol::operation",
                "type": "static_variant",
                "etypes": [
                    "xgt::protocol::comment_operation",
                    "xgt::protocol::transfer_operation",
                    "xgt::protocol::wallet_create_operation",
                    "xgt::protocol::wallet_update_operation",
                    "xgt::protocol::witness_update_operation",
                    "xgt::protocol::custom_operation",
                    "xgt::protocol::report_over_production_operation",
                    "xgt::protocol::delete_comment_operation",
                    "xgt::protocol::custom_json_operation",
                    "xgt::protocol::comment_options_operation",
                    "xgt::protocol::request_wallet_recovery_operation",
                    "xgt::protocol::recover_wallet_operation",
                    "xgt::protocol::change_recovery_wallet_operation",
                    "xgt::protocol::escrow_transfer_operation",
                    "xgt::protocol::escrow_dispute_operation",
                    "xgt::protocol::escrow_release_operation",
                    "xgt::protocol::pow_operation",
                    "xgt::protocol::escrow_approve_operation",
                    "xgt::protocol::vote_operation",
                    "xgt::protocol::xtt_setup_operation",
                    "xgt::protocol::xtt_setup_ico_tier_operation",
                    "xgt::protocol::xtt_set_setup_parameters_operation",
                    "xgt::protocol::xtt_set_runtime_parameters_operation",
                    "xgt::protocol::xtt_create_operation",
                    "xgt::protocol::xtt_contribute_operation",
                    "xgt::protocol::shutdown_witness_operation",
                    "xgt::protocol::hardfork_operation",
                    "xgt::protocol::clear_null_wallet_balance_operation",
                    "xgt::protocol::contract_create_operation",
                    "xgt::protocol::contract_invoke_operation"
                ]
            }
        },
        "xgt::protocol::optional_automated_action": {
            "deps": [
                "xgt::protocol::example_optional_action"
            ],
            "schema": {
                "name": "xgt::protocol::optional_automated_action",
                "type": "static_variant",
                "etypes": [
                    "xgt::protocol::example_optional_action"
                ]
            }
        },
        "xgt::protocol::pow": {
            "deps": [
                "xgt::protocol::pow_input",
                "uint32_t"
            ],
            "schema": {
                "name": "xgt::protocol::pow",
                "type": "class",
                "members": [
                    [
                        "xgt::protocol::pow_input",
                        "input"
                    ],
                    [
                        "uint32_t",
                        "pow_summary"
                    ]
                ]
            }
        },
        "xgt::protocol::pow_input": {
            "deps": [
                "xgt::protocol::wallet_name_type",
                "uint160_t",
                "uint64_t"
            ],
            "schema": {
                "name": "xgt::protocol::pow_input",
                "type": "class",
                "members": [
                    [
                        "xgt::protocol::wallet_name_type",
                        "worker_account"
                    ],
                    [
                        "uint160_t",
                        "prev_block"
                    ],
                    [
                        "uint64_t",
                        "nonce"
                    ]
                ]
            }
        },
        "xgt::protocol::pow_operation": {
            "deps": [
                "xgt::protocol::pow_work",
                "optional<xgt::protocol::public_key_type>",
                "xgt::protocol::legacy_chain_properties"
            ],
            "schema": {
                "name": "xgt::protocol::pow_operation",
                "type": "class",
                "members": [
                    [
                        "xgt::protocol::pow_work",
                        "work"
                    ],
                    [
                        "optional<xgt::protocol::public_key_type>",
                        "new_recovery_key"
                    ],
                    [
                        "xgt::protocol::legacy_chain_properties",
                        "props"
                    ]
                ]
            }
        },
        "xgt::protocol::pow_work": {
            "deps": [
                "xgt::protocol::pow",
                "xgt::protocol::sha2_pow"
            ],
            "schema": {
                "name": "xgt::protocol::pow_work",
                "type": "static_variant",
                "etypes": [
                    "xgt::protocol::pow",
                    "xgt::protocol::sha2_pow"
                ]
            }
        },
        "xgt::protocol::public_key_type": {
            "deps": [
                "fc::array<char,33>"
            ],
            "schema": {
                "name": "xgt::protocol::public_key_type",
                "type": "class",
                "members": [
                    [
                        "fc::array<char,33>",
                        "key_data"
                    ]
                ]
            }
        },
        "xgt::protocol::recover_wallet_operation": {
            "deps": [
                "xgt::protocol::wallet_name_type",
                "xgt::protocol::authority",
                "xgt::protocol::authority",
                "flat_set<xgt::protocol::future_extensions>"
            ],
            "schema": {
                "name": "xgt::protocol::recover_wallet_operation",
                "type": "class",
                "members": [
                    [
                        "xgt::protocol::wallet_name_type",
                        "account_to_recover"
                    ],
                    [
                        "xgt::protocol::authority",
                        "new_recovery_authority"
                    ],
                    [
                        "xgt::protocol::authority",
                        "recent_recovery_authority"
                    ],
                    [
                        "flat_set<xgt::protocol::future_extensions>",
                        "extensions"
                    ]
                ]
            }
        },
        "xgt::protocol::report_over_production_operation": {
            "deps": [
                "xgt::protocol::wallet_name_type",
                "xgt::protocol::signed_block_header",
                "xgt::protocol::signed_block_header"
            ],
            "schema": {
                "name": "xgt::protocol::report_over_production_operation",
                "type": "class",
                "members": [
                    [
                        "xgt::protocol::wallet_name_type",
                        "reporter"
                    ],
                    [
                        "xgt::protocol::signed_block_header",
                        "first_block"
                    ],
                    [
                        "xgt::protocol::signed_block_header",
                        "second_block"
                    ]
                ]
            }
        },
        "xgt::protocol::request_wallet_recovery_operation": {
            "deps": [
                "xgt::protocol::wallet_name_type",
                "xgt::protocol::wallet_name_type",
                "xgt::protocol::authority",
                "flat_set<xgt::protocol::future_extensions>"
            ],
            "schema": {
                "name": "xgt::protocol::request_wallet_recovery_operation",
                "type": "class",
                "members": [
                    [
                        "xgt::protocol::wallet_name_type",
                        "recovery_account"
                    ],
                    [
                        "xgt::protocol::wallet_name_type",
                        "account_to_recover"
                    ],
                    [
                        "xgt::protocol::authority",
                        "new_recovery_authority"
                    ],
                    [
                        "flat_set<xgt::protocol::future_extensions>",
                        "extensions"
                    ]
                ]
            }
        },
        "xgt::protocol::required_automated_action": {
            "deps": [
                "xgt::protocol::xtt_ico_launch_action",
                "xgt::protocol::xtt_ico_evaluation_action",
                "xgt::protocol::xtt_token_launch_action",
                "xgt::protocol::xtt_refund_action",
                "xgt::protocol::example_required_action"
            ],
            "schema": {
                "name": "xgt::protocol::required_automated_action",
                "type": "static_variant",
                "etypes": [
                    "xgt::protocol::xtt_ico_launch_action",
                    "xgt::protocol::xtt_ico_evaluation_action",
                    "xgt::protocol::xtt_token_launch_action",
                    "xgt::protocol::xtt_refund_action",
                    "xgt::protocol::example_required_action"
                ]
            }
        },
        "xgt::protocol::sha2_pow": {
            "deps": [
                "xgt::protocol::pow_input",
                "fc::sha256",
                "uint160_t",
                "uint32_t"
            ],
            "schema": {
                "name": "xgt::protocol::sha2_pow",
                "type": "class",
                "members": [
                    [
                        "xgt::protocol::pow_input",
                        "input"
                    ],
                    [
                        "fc::sha256",
                        "proof"
                    ],
                    [
                        "uint160_t",
                        "prev_block"
                    ],
                    [
                        "uint32_t",
                        "pow_summary"
                    ]
                ]
            }
        },
        "xgt::protocol::share_type": {
            "deps": [
                "int64_t"
            ],
            "schema": {
                "name": "xgt::protocol::share_type",
                "type": "class",
                "members": [
                    [
                        "int64_t",
                        "value"
                    ]
                ]
            }
        },
        "xgt::protocol::shutdown_witness_operation": {
            "deps": [
                "xgt::protocol::wallet_name_type"
            ],
            "schema": {
                "name": "xgt::protocol::shutdown_witness_operation",
                "type": "class",
                "members": [
                    [
                        "xgt::protocol::wallet_name_type",
                        "recovery"
                    ]
                ]
            }
        },
        "xgt::protocol::signed_block": {
            "deps": [
                "uint160_t",
                "fc::time_point_sec",
                "string",
                "uint160_t",
                "flat_set<xgt::protocol::block_header_extensions>",
                "fc::array<uint8_t,65>",
                "std::vector<xgt::protocol::signed_transaction>"
            ],
            "schema": {
                "name": "xgt::protocol::signed_block",
                "type": "class",
                "members": [
                    [
                        "uint160_t",
                        "previous"
                    ],
                    [
                        "fc::time_point_sec",
                        "timestamp"
                    ],
                    [
                        "string",
                        "witness"
                    ],
                    [
                        "uint160_t",
                        "transaction_merkle_root"
                    ],
                    [
                        "flat_set<xgt::protocol::block_header_extensions>",
                        "extensions"
                    ],
                    [
                        "fc::array<uint8_t,65>",
                        "witness_signature"
                    ],
                    [
                        "std::vector<xgt::protocol::signed_transaction>",
                        "transactions"
                    ]
                ]
            }
        },
        "xgt::protocol::signed_block_header": {
            "deps": [
                "uint160_t",
                "fc::time_point_sec",
                "string",
                "uint160_t",
                "flat_set<xgt::protocol::block_header_extensions>",
                "fc::array<uint8_t,65>"
            ],
            "schema": {
                "name": "xgt::protocol::signed_block_header",
                "type": "class",
                "members": [
                    [
                        "uint160_t",
                        "previous"
                    ],
                    [
                        "fc::time_point_sec",
                        "timestamp"
                    ],
                    [
                        "string",
                        "witness"
                    ],
                    [
                        "uint160_t",
                        "transaction_merkle_root"
                    ],
                    [
                        "flat_set<xgt::protocol::block_header_extensions>",
                        "extensions"
                    ],
                    [
                        "fc::array<uint8_t,65>",
                        "witness_signature"
                    ]
                ]
            }
        },
        "xgt::protocol::signed_transaction": {
            "deps": [
                "uint16_t",
                "uint32_t",
                "fc::time_point_sec",
                "std::vector<xgt::protocol::operation>",
                "flat_set<xgt::protocol::future_extensions>",
                "std::vector<fc::array<uint8_t,65>>"
            ],
            "schema": {
                "name": "xgt::protocol::signed_transaction",
                "type": "class",
                "members": [
                    [
                        "uint16_t",
                        "ref_block_num"
                    ],
                    [
                        "uint32_t",
                        "ref_block_prefix"
                    ],
                    [
                        "fc::time_point_sec",
                        "expiration"
                    ],
                    [
                        "std::vector<xgt::protocol::operation>",
                        "operations"
                    ],
                    [
                        "flat_set<xgt::protocol::future_extensions>",
                        "extensions"
                    ],
                    [
                        "std::vector<fc::array<uint8_t,65>>",
                        "signatures"
                    ]
                ]
            }
        },
        "xgt::protocol::transfer_operation": {
            "deps": [
                "xgt::protocol::wallet_name_type",
                "xgt::protocol::wallet_name_type",
                "xgt::protocol::asset",
                "string"
            ],
            "schema": {
                "name": "xgt::protocol::transfer_operation",
                "type": "class",
                "members": [
                    [
                        "xgt::protocol::wallet_name_type",
                        "from"
                    ],
                    [
                        "xgt::protocol::wallet_name_type",
                        "to"
                    ],
                    [
                        "xgt::protocol::asset",
                        "amount"
                    ],
                    [
                        "string",
                        "memo"
                    ]
                ]
            }
        },
        "xgt::protocol::version": {
            "deps": [
                "uint32_t"
            ],
            "schema": {
                "name": "xgt::protocol::version",
                "type": "class",
                "members": [
                    [
                        "uint32_t",
                        "v_num"
                    ]
                ]
            }
        },
        "xgt::protocol::vote_operation": {
            "deps": [
                "xgt::protocol::wallet_name_type",
                "xgt::protocol::wallet_name_type",
                "string",
                "flat_set<xgt::protocol::future_extensions>"
            ],
            "schema": {
                "name": "xgt::protocol::vote_operation",
                "type": "class",
                "members": [
                    [
                        "xgt::protocol::wallet_name_type",
                        "voter"
                    ],
                    [
                        "xgt::protocol::wallet_name_type",
                        "author"
                    ],
                    [
                        "string",
                        "permlink"
                    ],
                    [
                        "flat_set<xgt::protocol::future_extensions>",
                        "extensions"
                    ]
                ]
            }
        },
        "xgt::protocol::wallet_create_operation": {
            "deps": [
                "xgt::protocol::asset",
                "xgt::protocol::wallet_name_type",
                "xgt::protocol::wallet_name_type",
                "xgt::protocol::authority",
                "xgt::protocol::authority",
                "xgt::protocol::authority",
                "xgt::protocol::public_key_type",
                "string"
            ],
            "schema": {
                "name": "xgt::protocol::wallet_create_operation",
                "type": "class",
                "members": [
                    [
                        "xgt::protocol::asset",
                        "fee"
                    ],
                    [
                        "xgt::protocol::wallet_name_type",
                        "creator"
                    ],
                    [
                        "xgt::protocol::wallet_name_type",
                        "new_wallet_name"
                    ],
                    [
                        "xgt::protocol::authority",
                        "recovery"
                    ],
                    [
                        "xgt::protocol::authority",
                        "money"
                    ],
                    [
                        "xgt::protocol::authority",
                        "social"
                    ],
                    [
                        "xgt::protocol::public_key_type",
                        "memo_key"
                    ],
                    [
                        "string",
                        "json_metadata"
                    ]
                ]
            }
        },
        "xgt::protocol::wallet_name_type": {
            "deps": [],
            "schema": {
                "name": "xgt::protocol::wallet_name_type",
                "type": "wallet_name_type"
            }
        },
        "xgt::protocol::wallet_update_operation": {
            "deps": [
                "xgt::protocol::wallet_name_type",
                "optional<xgt::protocol::authority>",
                "optional<xgt::protocol::authority>",
                "optional<xgt::protocol::authority>",
                "optional<xgt::protocol::public_key_type>",
                "string",
                "string",
                "flat_set<xgt::protocol::future_extensions>"
            ],
            "schema": {
                "name": "xgt::protocol::wallet_update_operation",
                "type": "class",
                "members": [
                    [
                        "xgt::protocol::wallet_name_type",
                        "wallet"
                    ],
                    [
                        "optional<xgt::protocol::authority>",
                        "recovery"
                    ],
                    [
                        "optional<xgt::protocol::authority>",
                        "money"
                    ],
                    [
                        "optional<xgt::protocol::authority>",
                        "social"
                    ],
                    [
                        "optional<xgt::protocol::public_key_type>",
                        "memo_key"
                    ],
                    [
                        "string",
                        "json_metadata"
                    ],
                    [
                        "string",
                        "social_json_metadata"
                    ],
                    [
                        "flat_set<xgt::protocol::future_extensions>",
                        "extensions"
                    ]
                ]
            }
        },
        "xgt::protocol::witness_update_operation": {
            "deps": [
                "xgt::protocol::wallet_name_type",
                "string",
                "xgt::protocol::public_key_type",
                "xgt::protocol::legacy_chain_properties",
                "xgt::protocol::asset"
            ],
            "schema": {
                "name": "xgt::protocol::witness_update_operation",
                "type": "class",
                "members": [
                    [
                        "xgt::protocol::wallet_name_type",
                        "owner"
                    ],
                    [
                        "string",
                        "url"
                    ],
                    [
                        "xgt::protocol::public_key_type",
                        "block_signing_key"
                    ],
                    [
                        "xgt::protocol::legacy_chain_properties",
                        "props"
                    ],
                    [
                        "xgt::protocol::asset",
                        "fee"
                    ]
                ]
            }
        },
        "xgt::protocol::xtt_capped_generation_policy": {
            "deps": [
                "xgt::protocol::xtt_generation_unit",
                "flat_set<xgt::protocol::future_extensions>"
            ],
            "schema": {
                "name": "xgt::protocol::xtt_capped_generation_policy",
                "type": "class",
                "members": [
                    [
                        "xgt::protocol::xtt_generation_unit",
                        "generation_unit"
                    ],
                    [
                        "flat_set<xgt::protocol::future_extensions>",
                        "extensions"
                    ]
                ]
            }
        },
        "xgt::protocol::xtt_contribute_operation": {
            "deps": [
                "xgt::protocol::wallet_name_type",
                "xgt::protocol::asset_symbol_type",
                "uint32_t",
                "xgt::protocol::asset",
                "flat_set<xgt::protocol::future_extensions>"
            ],
            "schema": {
                "name": "xgt::protocol::xtt_contribute_operation",
                "type": "class",
                "members": [
                    [
                        "xgt::protocol::wallet_name_type",
                        "contributor"
                    ],
                    [
                        "xgt::protocol::asset_symbol_type",
                        "symbol"
                    ],
                    [
                        "uint32_t",
                        "contribution_id"
                    ],
                    [
                        "xgt::protocol::asset",
                        "contribution"
                    ],
                    [
                        "flat_set<xgt::protocol::future_extensions>",
                        "extensions"
                    ]
                ]
            }
        },
        "xgt::protocol::xtt_create_operation": {
            "deps": [
                "xgt::protocol::wallet_name_type",
                "xgt::protocol::asset_symbol_type",
                "xgt::protocol::fixed_string<8>",
                "xgt::protocol::asset",
                "uint8_t",
                "flat_set<xgt::protocol::future_extensions>"
            ],
            "schema": {
                "name": "xgt::protocol::xtt_create_operation",
                "type": "class",
                "members": [
                    [
                        "xgt::protocol::wallet_name_type",
                        "control_account"
                    ],
                    [
                        "xgt::protocol::asset_symbol_type",
                        "symbol"
                    ],
                    [
                        "xgt::protocol::fixed_string<8>",
                        "desired_ticker"
                    ],
                    [
                        "xgt::protocol::asset",
                        "xtt_creation_fee"
                    ],
                    [
                        "uint8_t",
                        "precision"
                    ],
                    [
                        "flat_set<xgt::protocol::future_extensions>",
                        "extensions"
                    ]
                ]
            }
        },
        "xgt::protocol::xtt_generation_unit": {
            "deps": [
                "bip::flat_map<xgt::protocol::fixed_string<32>,uint16_t>",
                "bip::flat_map<xgt::protocol::fixed_string<32>,uint16_t>"
            ],
            "schema": {
                "name": "xgt::protocol::xtt_generation_unit",
                "type": "class",
                "members": [
                    [
                        "bip::flat_map<xgt::protocol::fixed_string<32>,uint16_t>",
                        "xgt_unit"
                    ],
                    [
                        "bip::flat_map<xgt::protocol::fixed_string<32>,uint16_t>",
                        "token_unit"
                    ]
                ]
            }
        },
        "xgt::protocol::xtt_ico_evaluation_action": {
            "deps": [
                "xgt::protocol::wallet_name_type",
                "xgt::protocol::asset_symbol_type"
            ],
            "schema": {
                "name": "xgt::protocol::xtt_ico_evaluation_action",
                "type": "class",
                "members": [
                    [
                        "xgt::protocol::wallet_name_type",
                        "control_account"
                    ],
                    [
                        "xgt::protocol::asset_symbol_type",
                        "symbol"
                    ]
                ]
            }
        },
        "xgt::protocol::xtt_ico_launch_action": {
            "deps": [
                "xgt::protocol::wallet_name_type",
                "xgt::protocol::asset_symbol_type"
            ],
            "schema": {
                "name": "xgt::protocol::xtt_ico_launch_action",
                "type": "class",
                "members": [
                    [
                        "xgt::protocol::wallet_name_type",
                        "control_account"
                    ],
                    [
                        "xgt::protocol::asset_symbol_type",
                        "symbol"
                    ]
                ]
            }
        },
        "xgt::protocol::xtt_param_allow_downvotes": {
            "deps": [
                "bool"
            ],
            "schema": {
                "name": "xgt::protocol::xtt_param_allow_downvotes",
                "type": "class",
                "members": [
                    [
                        "bool",
                        "value"
                    ]
                ]
            }
        },
        "xgt::protocol::xtt_param_allow_voting": {
            "deps": [
                "bool"
            ],
            "schema": {
                "name": "xgt::protocol::xtt_param_allow_voting",
                "type": "class",
                "members": [
                    [
                        "bool",
                        "value"
                    ]
                ]
            }
        },
        "xgt::protocol::xtt_param_vote_regeneration_period_seconds_v1": {
            "deps": [
                "uint32_t",
                "uint32_t"
            ],
            "schema": {
                "name": "xgt::protocol::xtt_param_vote_regeneration_period_seconds_v1",
                "type": "class",
                "members": [
                    [
                        "uint32_t",
                        "vote_regeneration_period_seconds"
                    ],
                    [
                        "uint32_t",
                        "votes_per_regeneration_period"
                    ]
                ]
            }
        },
        "xgt::protocol::xtt_param_windows_v1": {
            "deps": [
                "uint32_t"
            ],
            "schema": {
                "name": "xgt::protocol::xtt_param_windows_v1",
                "type": "class",
                "members": [
                    [
                        "uint32_t",
                        "reverse_auction_window_seconds"
                    ]
                ]
            }
        },
        "xgt::protocol::xtt_refund_action": {
            "deps": [
                "xgt::protocol::wallet_name_type",
                "xgt::protocol::asset_symbol_type",
                "uint32_t",
                "xgt::protocol::asset"
            ],
            "schema": {
                "name": "xgt::protocol::xtt_refund_action",
                "type": "class",
                "members": [
                    [
                        "xgt::protocol::wallet_name_type",
                        "contributor"
                    ],
                    [
                        "xgt::protocol::asset_symbol_type",
                        "symbol"
                    ],
                    [
                        "uint32_t",
                        "contribution_id"
                    ],
                    [
                        "xgt::protocol::asset",
                        "refund"
                    ]
                ]
            }
        },
        "xgt::protocol::xtt_runtime_parameter": {
            "deps": [
                "xgt::protocol::xtt_param_windows_v1",
                "xgt::protocol::xtt_param_vote_regeneration_period_seconds_v1",
                "xgt::protocol::xtt_param_allow_downvotes"
            ],
            "schema": {
                "name": "xgt::protocol::xtt_runtime_parameter",
                "type": "static_variant",
                "etypes": [
                    "xgt::protocol::xtt_param_windows_v1",
                    "xgt::protocol::xtt_param_vote_regeneration_period_seconds_v1",
                    "xgt::protocol::xtt_param_allow_downvotes"
                ]
            }
        },
        "xgt::protocol::xtt_set_runtime_parameters_operation": {
            "deps": [
                "xgt::protocol::wallet_name_type",
                "xgt::protocol::asset_symbol_type",
                "flat_set<xgt::protocol::xtt_runtime_parameter>",
                "flat_set<xgt::protocol::future_extensions>"
            ],
            "schema": {
                "name": "xgt::protocol::xtt_set_runtime_parameters_operation",
                "type": "class",
                "members": [
                    [
                        "xgt::protocol::wallet_name_type",
                        "control_account"
                    ],
                    [
                        "xgt::protocol::asset_symbol_type",
                        "symbol"
                    ],
                    [
                        "flat_set<xgt::protocol::xtt_runtime_parameter>",
                        "runtime_parameters"
                    ],
                    [
                        "flat_set<xgt::protocol::future_extensions>",
                        "extensions"
                    ]
                ]
            }
        },
        "xgt::protocol::xtt_set_setup_parameters_operation": {
            "deps": [
                "xgt::protocol::wallet_name_type",
                "xgt::protocol::asset_symbol_type",
                "flat_set<xgt::protocol::xtt_setup_parameter>",
                "flat_set<xgt::protocol::future_extensions>"
            ],
            "schema": {
                "name": "xgt::protocol::xtt_set_setup_parameters_operation",
                "type": "class",
                "members": [
                    [
                        "xgt::protocol::wallet_name_type",
                        "control_account"
                    ],
                    [
                        "xgt::protocol::asset_symbol_type",
                        "symbol"
                    ],
                    [
                        "flat_set<xgt::protocol::xtt_setup_parameter>",
                        "setup_parameters"
                    ],
                    [
                        "flat_set<xgt::protocol::future_extensions>",
                        "extensions"
                    ]
                ]
            }
        },
        "xgt::protocol::xtt_setup_ico_tier_operation": {
            "deps": [
                "xgt::protocol::wallet_name_type",
                "xgt::protocol::asset_symbol_type",
                "xgt::protocol::share_type",
                "fc::static_variant<xgt::protocol::xtt_capped_generation_policy>",
                "bool",
                "flat_set<xgt::protocol::future_extensions>"
            ],
            "schema": {
                "name": "xgt::protocol::xtt_setup_ico_tier_operation",
                "type": "class",
                "members": [
                    [
                        "xgt::protocol::wallet_name_type",
                        "control_account"
                    ],
                    [
                        "xgt::protocol::asset_symbol_type",
                        "symbol"
                    ],
                    [
                        "xgt::protocol::share_type",
                        "xgt_units_cap"
                    ],
                    [
                        "fc::static_variant<xgt::protocol::xtt_capped_generation_policy>",
                        "generation_policy"
                    ],
                    [
                        "bool",
                        "remove"
                    ],
                    [
                        "flat_set<xgt::protocol::future_extensions>",
                        "extensions"
                    ]
                ]
            }
        },
        "xgt::protocol::xtt_setup_operation": {
            "deps": [
                "xgt::protocol::wallet_name_type",
                "xgt::protocol::asset_symbol_type",
                "int64_t",
                "fc::time_point_sec",
                "fc::time_point_sec",
                "fc::time_point_sec",
                "xgt::protocol::share_type",
                "uint32_t",
                "uint32_t",
                "flat_set<xgt::protocol::future_extensions>"
            ],
            "schema": {
                "name": "xgt::protocol::xtt_setup_operation",
                "type": "class",
                "members": [
                    [
                        "xgt::protocol::wallet_name_type",
                        "control_account"
                    ],
                    [
                        "xgt::protocol::asset_symbol_type",
                        "symbol"
                    ],
                    [
                        "int64_t",
                        "max_supply"
                    ],
                    [
                        "fc::time_point_sec",
                        "contribution_begin_time"
                    ],
                    [
                        "fc::time_point_sec",
                        "contribution_end_time"
                    ],
                    [
                        "fc::time_point_sec",
                        "launch_time"
                    ],
                    [
                        "xgt::protocol::share_type",
                        "xgt_units_min"
                    ],
                    [
                        "uint32_t",
                        "min_unit_ratio"
                    ],
                    [
                        "uint32_t",
                        "max_unit_ratio"
                    ],
                    [
                        "flat_set<xgt::protocol::future_extensions>",
                        "extensions"
                    ]
                ]
            }
        },
        "xgt::protocol::xtt_setup_parameter": {
            "deps": [
                "xgt::protocol::xtt_param_allow_voting"
            ],
            "schema": {
                "name": "xgt::protocol::xtt_setup_parameter",
                "type": "static_variant",
                "etypes": [
                    "xgt::protocol::xtt_param_allow_voting"
                ]
            }
        },
        "xgt::protocol::xtt_token_launch_action": {
            "deps": [
                "xgt::protocol::wallet_name_type",
                "xgt::protocol::asset_symbol_type"
            ],
            "schema": {
                "name": "xgt::protocol::xtt_token_launch_action",
                "type": "class",
                "members": [
                    [
                        "xgt::protocol::wallet_name_type",
                        "control_account"
                    ],
                    [
                        "xgt::protocol::asset_symbol_type",
                        "symbol"
                    ]
                ]
            }
        },
        "xgt::void_t": {
            "deps": [],
            "schema": {
                "name": "xgt::void_t",
                "type": "class",
                "members": []
            }
        }
    },
    "chain_object_types": []
}

```
