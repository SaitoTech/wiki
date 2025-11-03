---
title: Network Configuration for Saito-lite-Rust
description: Information on network configuration files and settings for deployed Saito-lite-Rust nodes.
published: true
date: 2025-11-03T05:40:12.038Z
tags: 
editor: markdown
dateCreated: 2024-11-20T04:10:39.991Z
---

# Saito Network Configuration

The `config/options.conf` file specifies network configuration options like the IP address on which the server runs and the ports it should open and the peers to which it should connect. The template file `config/options.conf.template` will run a server at `http://localhost:12101` by default. You can rename or edit it as you'd like.

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
You do not need to provide information for most of these fields. The most important are the following:

```json
  "server": {
    "host": "localhost",
    "port": 12101,
    "protocol": "http",
    "endpoint": {
      "host": "localhost",
      "port": 12101,
      "protocol": "http"
    },
```

`host` and `port` indicate the address of the server as visible to the operating system and any local apps. If you are running Saito on a remote server you should provide the `host` and `port` that users will use to connect to the server as the `endpoint`. 

### Configuration Reference

- `host`: IP address the server listens on. 127.0.0.1 for localhost.
- `port`: Port number for the server. Default is 12101.
- `protocol`: Network protocol, http in this case.
- `endpoint`: Specifies the endpoint details, mirroring the server's configuration for external access.
- `verification_threads`: Number of threads for processing verification tasks.
- `channel_size`: Maximum number of queued tasks or messages.
- `stat_timer_in_ms`: Interval for reporting stats or performing periodic checks.
- `reconnection_wait_time`: Wait time before attempting reconnection in ms. Default is 10000.
- `thread_sleep_time_in_ms`: Sleep time for background threads in ms
- `block_fetch_batch_size`: Number of blocks fetched per batch during sync.

### Peers Configuration
- `peers`: An array of peer nodes the server will connect to.

Note that each peer object includes host, port, protocol, and synctype. Since these connections will be made over-the-network, the `host` and `port` you provide for any peers should be the publicly-available information provided in *their* `options.conf` as an endpoint.
