---
title: Network Configuration for Saito-lite-Rust
description: Information on network configuration files and settings for deployed Saito-lite-Rust nodes.
published: true
date: 2025-11-03T07:39:32.458Z
tags: 
editor: markdown
dateCreated: 2024-11-20T04:10:39.991Z
---

# Saito Node Configuration

Saito nodejs nodes keep all their configuration and operating data in `config/options`.

## Minimal Configuration

If no configuration is present the `compile` script will copy [a template config file](https://github.com/SaitoTech/saito/blob/master/node/config/.template.options.conf) to `config/options`.

This file contains minimal information for the node to run locally, responding on [http://localhost:12101](http://localhost:12101)

## Network Configuration

**Exposing your node**

The server url (protocol + host + port) is the local address and port of the node. This can usually be left unchanged.

The endpoint url is the address at which browsers and other nodes will connect to you. This is used when the public address or domain name for the node differs from local, for instance when behind a proxy or NAT.

**Connecting to other nodes**

The each peer in the peers collection is the endpoint url for a node on the network you want to connect to. This will be provided by them.
The `synctype` value determins the type of blocks requested from the peer. `lite` merkelerized blocks containing only relevant transactions or `full` blocks.

## Wallet Configuration

If no wallet data exists on start the node will auto generate a public/private key pair and store these in the wallet along with metadata for managing balances etc.

Once this is created it is persistent.

* To backup the wallet simply backup the `config/options` file.
* To encrypt the wallet, add a `SAITO_PASS` environment variable. This will cause the node to encrypt it's options on each save.

## All Configuration Values

The bulk of Saito's configuration is written by the node but exposed in the `config/options` file. There are two main sections.

Consensus information defaults to the values on the Saito Network. Blocks will be rejected by nodes on the network if they don't match the consensus variables of the exisitng chain. Do not edit consenus values unless you are running a test network or developing locally and want, for example, faster block times.

### User Editable Configuration

```json
{
  "server": {                                // node local and remote ip information
    "host": "localhost",                     // local host name or ip
    "port": 12101,                           // local port 
    "protocol": "http",                      // local protocol [http/https]
    "endpoint": {                            // external address to connect to this node on (usually reverse proxied)
      "host": "saitonode.example.com",       // external host name
      "port": 443,                           // external port (usually 443 for ssl/https and 80 for unencrypted connections)
      "protocol": "http"                     // external protocol [http,https]
    },
    "verification_threads": 4,               // number of verification threads (rust only)
    "channel_size": 10000,                   // size of a message buffer between threads
    "stat_timer_in_ms": 5000,                // how often the ./data/saito.stats file is written
    "reconnection_wait_time": 10000,         // time between reconnect attempts (doubles each unsuccessful reconnect attempt)
    "thread_sleep_time_in_ms": 10,           // thread sleep duration if there is no work to do
    "block_fetch_batch_size": 10             // count of blocks a node will fetch parallely from a peer any given time.
  },
  "peers": [                                 // ip/host information for other nodes - this should be provided to you by the peer
    {
      "host": "node.other.net",              // peer domain or address
      "port": 443,                           // peer's port
      "protocol": "https",                   // peer's connection protocol
      "synctype": "full"                     // determines if the node requests full (complete) or lite (merkelerized with only relevant transactions) blocks
    }
  ],
  "wallet": {                                // public and private key are generated on first run if not manually set.
    "publicKey": "",                         // the public key for the node's wallet
    "privateKey": ""                         // the private key for the node's wallet
  },
  "spv_mode": false,                         // full [false] or lite node [true]
  "consensus": {                             // do not edit these values unless you are connecting to a testnet with specific non-standard settings.
    "genesis_period": 80640,                 // number of blocks in the chain (before ATR)
    "heartbeat_interval": 30000,             // target time between blocks
    "prune_after_blocks": 99,                // how many blocks to keep live in memory (this can be reduced if memory is limited)
    "max_staker_recursions": 3,              //
    "default_social_stake": 100000000000000, // amount that must be staked to produce a block
    "default_social_stake_period": 100,      // number of blocks before the stake is spendable again.
    "block_confirmation_limit": 1,           // for each block, how many on confirmation callbacks are called
    "recollect_discarded_txs_mode": 2,       // recollect txs when a block reorged out of longest chain. 0 - recollect nothing, 1 - recollect txs with fees, 2 - recollect all
    "disable_block_production": false        // do not attempt to make blocks (only route transactions and blocks, and generate golden tickets)
  }
  }
```

### Node writen configuration

```Json
  // All information beyond here is machine generated do not edit.
  "blockchain": {  
    "last_block_hash": "",
    "last_block_id": 0,
    "last_timestamp": 0,
    "genesis_block_id": 0,
    "genesis_timestamp": 0,
    "lowest_acceptable_timestamp": 0,
    "lowest_acceptable_block_hash": "",
    "lowest_acceptable_block_id": 0,
    "fork_id": "0",
    "issuance_writing_block_interval": 10,
    "confirmations": []
  },
  // related to congestion controls. Whole thing can be deleted, But entries are not to be modified manually.
  "congestion": []
}
```
