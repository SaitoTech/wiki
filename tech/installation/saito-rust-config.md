---
title: How to use saito-rust configuration file
description: 
published: true
date: 2024-02-06T05:21:45.836Z
tags: 
editor: markdown
dateCreated: 2024-02-06T05:03:07.560Z
---

## Configuration File Explanation
The config.template.json file is essential for configuring your Saito node. Below is an explanation of its structure:

### Server Configuration
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
- peers: An array of configurations for peer nodes the server will connect to.
Each peer object includes host, port, protocol, and synctype
This configuration is crucial for setting up how your node interacts with the network, manages resources, and synchronizes data with peers.

