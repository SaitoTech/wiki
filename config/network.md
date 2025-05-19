---
title: Network Configuration for Saito-lite-Rust
description: Information on network configuration files and settings for deployed Saito-lite-Rust nodes.
published: true
date: 2025-05-19T17:05:35.501Z
tags: 
editor: markdown
dateCreated: 2024-11-20T04:10:39.991Z
---

# Saito Network Configuration

The `config/options.conf` file specifies network configuration options like the IP address on which the server runs and the ports it should open and the peers to which it should connect. The template file `config/options.conf.template` will run a server at `http://localhost:12101` by default. You can rename or edit it as you'd like.

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

### Configuration Reference

- host: IP address the server listens on. 127.0.0.1 for localhost.
- port: Port number for the server. Default is 12101.
- protocol: Network protocol, http in this case.
- endpoint: Specifies the endpoint details, mirroring the server's configuration for external access.
- verification_threads: Number of threads for processing verification tasks.
- channel_size: Maximum number of queued tasks or messages.
- stat_timer_in_ms: Interval for reporting stats or performing periodic checks.
- reconnection_wait_time: Wait time before attempting reconnection in ms. Default is 10000.
- thread_sleep_time_in_ms: Sleep time for background threads in ms
- block_fetch_batch_size: Number of blocks fetched per batch during sync.

### Peers Configuration
- peers: An array of peer nodes the server will connect to.

Note that each peer object includes host, port, protocol, and synctype. Since these connections will be made over-the-network, the `host` and `port` you provide for any peers should be the publicly-available information provided in *their* options.conf as an endpoint.
