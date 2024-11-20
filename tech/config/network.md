---
title: Network Configuration for Saito-lite-Rust
description: Information on network configuration files and settings for deployed Saito-lite-Rust nodes.
published: true
date: 2024-11-20T04:10:39.991Z
tags: 
editor: markdown
dateCreated: 2024-11-20T04:10:39.991Z
---

# Network Configuration for Saito-lite-Rust

The `config/options.conf` file specifies network configuration options like the IP address on which the server runs and the ports it should open and the peers to which it should connect.

The template file which comes with a fresh install, `config/options.conf.template`, can be used as a starting point and refernce, and will look similar to this:

```json
{
  "server": {
    "host": "localhost",
    "port": 12101,
    "protocol": "http",
    "endpoint": {
      "host": "localhost",
      "port": 12101,
      "protocol": "http"
    },
    "verification_threads": 4,
    "channel_size": 10000,
    "stat_timer_in_ms": 5000,
    "reconnection_wait_time": 10000,
    "thread_sleep_time_in_ms": 10,
    "block_fetch_batch_size": 10
  },
  "peers": [],
  "spv_mode": false,
  "browser_mode": false,
  "blockchain": {
    "last_block_hash": "0000000000000000000000000000000000000000000000000000000000000000",
    "last_block_id": 0,
    "last_timestamp": 0,
    "genesis_block_id": 0,
    "genesis_timestamp": 0,
    "lowest_acceptable_timestamp": 0,
    "lowest_acceptable_block_hash": "0000000000000000000000000000000000000000000000000000000000000000",
    "lowest_acceptable_block_id": 0,
    "fork_id": "0000000000000000000000000000000000000000000000000000000000000000"
  },
  "wallet": {}
}
```