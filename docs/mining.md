---
layout: default
title: Mining
permalink: /mining/
---

# Mining
XGT is currently being distributed via Docker to make it easy to get started. A mining - 
enabled wallet is required to mine XGT at this time.

# Overview
This getting started guide will cover:
* Getting the Command Line Interface (CLI) wallet software
* Creating an XGT wallet address and keys
* Getting the mining software
* Creating the miner run command using the keys
* Mining process

## Getting the XGT CLI Wallet 
The XGT CLI wallet is currently distributed as a Docker Image. This 
manages the wallet dependencies, and provides installation without 
cumbersome tooling configuration.

1. [Install Docker](https://www.docker.com/get-started)

2. Pull the wallet code docker image:
```bash
docker pull obskein/xgt-wallet:1.0.7
```

3. Run the docker wallet image, in this case connecting to a seed node at 98.33.76.100
```bash
docker run --env XGT_HOST=http://seed-node-1.xgt.co.in:8751/ -it obskein/xgt-wallet:1.0.7
```

## Creating an XGT wallet address and keys
Wallets which are used for mining XGT must be registered on the XGT network using 
a signing tap, such as [xgt-firestarter](https://github.com/xgt-network/xgt-firestarter).

Once the XGT CLI wallet is running, the command
```ruby
create_mining_wallet
```

*SAVE WHAT GETS EMITTED BY THIS COMMAND*, it will look like this:
```
{"extensions"=>[], "operations"=>[{"type"=>"witness_update_operation", "value"=>{"owner"=>"XGT3oKtXHRCJhc62YFfBmjpoKP9picBmRfkn77yUPmT", "url"=>"http://test.host", "block_signing_key"=>"XGT6AuTQeopoMyrwcbFhYJdv3G3MimjdVpATh9iVwWcN2TSmd1yYx", "props"=>{"account_creation_fee"=>{:amount=>"0", :precision=>8, :nai=>"@@000000021"}}, "fee"=>{:amount=>"0", :precision=>8, :nai=>"@@000000021"}}}]}
"4aa587ca9816fd0d25853439e5920129770b91e8"
"sudo docker run --publish 8751:8751 --publish 2001:2001 --env XGT_WALLET=XGT3oKtXHRCJhc62YFfBmjpoKP9picBmRfkn77yUPmT --env XGT_RECOVERY_PRIVATE_KEY=5JsLyFWarvkXQyvXZ2XD3Y9P1WRfmJLyarMfA4PGv3UFAb9eh86 --env XGT_WITNESS_PRIVATE_KEY=5JsLyFWarvkXQyvXZ2XD3Y9P1WRfmJLyarMfA4PGv3UFAb9eh86 --env XGT_SEED_HOST=98.33.76.100:2001 rjungemann/xgt:1.4.8"
keys
    master 5KKCemKjiTrxh8NS2vtfWZvzzhhMNHARZYgfvoFkDwZpJh4g91H
    recovery_private 5JsLyFWarvkXQyvXZ2XD3Y9P1WRfmJLyarMfA4PGv3UFAb9eh86
    recovery_public XGT6AuTQeopoMyrwcbFhYJdv3G3MimjdVpATh9iVwWcN2TSmd1yYx
    money_private 5KM95toHur4ehkBMnQTGMcGeHqW2w9DdSU2dCMyWqMwgDobnLam
    money_public XGT5t9LwMxPEGQw8kDs6cfUtzHHkLTJHfNWMQKtNkm32gDAShV4Eg
    social_private 5KDyq1jfvVMXDWLW4UXAKVSpyYjjtzDb4sU6V8F2tkCXvTtsrDz
    social_public XGT7Jc414q6vg8hF2vBiUWUJFykYzbt1vXU5wpwWzcVxfzX6daHaF
    memo_private 5JUF9fzkzmgEL6LVME37wRpYRfHiM5jmx8sqpSy3SZPLCjFQK1k
    memo_public XGT5gBkQjx3zhT7PR6seJLMgzcEUWYCU33hM4zytQG9upMmVee76v
    wallet_name XGT3oKtXHRCJhc62YFfBmjpoKP9picBmRfkn77yUPmT
body {"keys":{"wallet_name":"XGT3oKtXHRCJhc62YFfBmjpoKP9picBmRfkn77yUPmT","recovery_public":"XGT6AuTQeopoMyrwcbFhYJdv3G3MimjdVpATh9iVwWcN2TSmd1yYx","money_public":"XGT5t9LwMxPEGQw8kDs6cfUtzHHkLTJHfNWMQKtNkm32gDAShV4Eg","social_public":"XGT7Jc414q6vg8hF2vBiUWUJFykYzbt1vXU5wpwWzcVxfzX6daHaF","memo_public":"XGT5gBkQjx3zhT7PR6seJLMgzcEUWYCU33hM4zytQG9upMmVee76v"},"create_tx_res":{"id":"84878d4f9a50f869da4492d7c96ac8a2e2057def"}}
#=> true
```

This output contains several useful things:

### Miner registration operation:
The operation that will go to the network, to register your miner:
```json
{"extensions"=>[], "operations"=>[{"type"=>"witness_update_operation", "value"=>{"owner"=>"XGT3oKtXHRCJhc62YFfBmjpoKP9picBmRfkn77yUPmT", "url"=>"http://test.host", "block_signing_key"=>"XGT6AuTQeopoMyrwcbFhYJdv3G3MimjdVpATh9iVwWcN2TSmd1yYx", "props"=>{"account_creation_fee"=>{:amount=>"0", :precision=>8, :nai=>"@@000000021"}}, "fee"=>{:amount=>"0", :precision=>8, :nai=>"@@000000021"}}}]}
```
The TXID for that registration:
```json
"4aa587ca9816fd0d25853439e5920129770b91e8"
```

A Docker run command, for running the miner:
```bash
sudo docker run --publish 8751:8751 --publish 2001:2001 --env XGT_WALLET=XGT3oKtXHRCJhc62YFfBmjpoKP9picBmRfkn77yUPmT --env XGT_RECOVERY_PRIVATE_KEY=5JsLyFWarvkXQyvXZ2XD3Y9P1WRfmJLyarMfA4PGv3UFAb9eh86 --env XGT_WITNESS_PRIVATE_KEY=5JsLyFWarvkXQyvXZ2XD3Y9P1WRfmJLyarMfA4PGv3UFAb9eh86 --env XGT_WIFS=5JsLyFWarvkXQyvXZ2XD3Y9P1WRfmJLyarMfA4PGv3UFAb9eh86 --env XGT_SEED_HOST=98.33.76.100:2001 rjungemann/xgt:1.4.8
```

The keys that were created:
```yaml
keys
    master 5KKCemKjiTrxh8NS2vtfWZvzzhhMNHARZYgfvoFkDwZpJh4g91H
    recovery_private 5JsLyFWarvkXQyvXZ2XD3Y9P1WRfmJLyarMfA4PGv3UFAb9eh86
    recovery_public XGT6AuTQeopoMyrwcbFhYJdv3G3MimjdVpATh9iVwWcN2TSmd1yYx
    money_private 5KM95toHur4ehkBMnQTGMcGeHqW2w9DdSU2dCMyWqMwgDobnLam
    money_public XGT5t9LwMxPEGQw8kDs6cfUtzHHkLTJHfNWMQKtNkm32gDAShV4Eg
    social_private 5KDyq1jfvVMXDWLW4UXAKVSpyYjjtzDb4sU6V8F2tkCXvTtsrDz
    social_public XGT7Jc414q6vg8hF2vBiUWUJFykYzbt1vXU5wpwWzcVxfzX6daHaF
    memo_private 5JUF9fzkzmgEL6LVME37wRpYRfHiM5jmx8sqpSy3SZPLCjFQK1k
    memo_public XGT5gBkQjx3zhT7PR6seJLMgzcEUWYCU33hM4zytQG9upMmVee76v
    wallet_name XGT3oKtXHRCJhc62YFfBmjpoKP9picBmRfkn77yUPmT
```

Will create a series of public and private keypairs, and a wallet address. Additionally, the command
will also register the address with the network, to enable mining.

## Getting the XGT Miner
Downloading and installing the miner is broadly similar in form to the wallet CLI.
```bash
docker pull rjungemann/xgt:1.4.8
```

### Creating the miner run command using the keys
The following command must be updated to use the wallet address AND the wallet recovery_private 
keys procured in the previous steps. In this case, `XGT_WALLET` needs to be set to the wallet address, and `XGT_RECOVERY_PRIVATE_KEY` needs to be set to the recovery private address.

```
sudo docker run --publish 8751:8751 --publish 2001:2001 --env XGT_WALLET=XGT3oKtXHRCJhc62YFfBmjpoKP9picBmRfkn77yUPmT --env XGT_RECOVERY_PRIVATE_KEY=5JsLyFWarvkXQyvXZ2XD3Y9P1WRfmJLyarMfA4PGv3UFAb9eh86 --env XGT_WITNESS_PRIVATE_KEY=5JsLyFWarvkXQyvXZ2XD3Y9P1WRfmJLyarMfA4PGv3UFAb9eh86 --env XGT_SEED_HOST=98.33.76.100:2001 rjungemann/xgt:1.4.8
```

### Mining process
Once a miner is attached to the network, either via the seed node or to another running node, then XGT will (in order)

1. Catch up the current block log, and sync with the network
2. Listen for transactions in the mempool
3. Attempt to calculate a valid SHA-256 for a block, using the current difficulty
4. Attempt to sign that block with the valid credentials
5. Broadcast the signed block, and get rewarded for the block mine.

## Tips

Save the docker run command as a cmd file (windows) or sh file (other platforms) to simplify starting the miner.

On linux, the engineering team uses systemd configurations to run the miner on startup. 
This can be achieved using the startup folder on windows, to start at login.

## Common problems

`Witness does not exist yet, bailing!`

This is caused by mining wallet not correctly being registered on the network. There was likely a problem communicating with the XGT seed node in the wallet set up phase, because either the address of the seed node was wrong, or the seed node was down. Set an alternate seed node by setting XGT_SEED_HOST to a node on the network.
