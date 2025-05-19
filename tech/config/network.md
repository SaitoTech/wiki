---
title: Network Configuration for Saito-lite-Rust
description: Information on network configuration files and settings for deployed Saito-lite-Rust nodes.
published: true
date: 2025-05-19T16:48:21.008Z
tags: 
editor: markdown
dateCreated: 2024-11-20T04:10:39.991Z
---

# Network Configuration for Saito-lite-Rust

The `config/options.conf` file specifies network configuration options like the IP address on which the server runs and the ports it should open and the peers to which it should connect.

The template file which comes with a fresh install, `config/options.conf.template`, can be used as a starting point and reference. It will look similar to this:

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

You do not need to provide information for most of these fields. The most important are the following:

```
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