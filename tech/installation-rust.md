---
title: Installation Instructions - Rust
description: Installation instructions for Saito-Rust
published: true
date: 2023-04-04T04:46:59.701Z
tags: 
editor: markdown
dateCreated: 2022-03-23T07:18:36.618Z
---


# Rust Installation Instructions

This page contains instructions on how to download and install the current Rust client (under development, intended for deployment on core routing nodes as the network scales). If you are looking to develop applications we recommend using the javascript client instead.

## Requirements:

* OS: Ubuntu 20.04 (MacOS instructions)
* Build tools: git, g++, make
* Stack: cargo rust (v.1.5.7+)
* https://github.com/saitotech/saito-rust-workspace


## Installing Saito Rust
```
git clone https://github.com/saitotech/saito-rust-workspace
cd saito-lite-workspace
RUST_LOG=debug cargo run
```

Please inform us if you have difficulty with the installation process so that we can update this WIKI.


## Architecture and Design

Documentation on the Rust client is fairly minimal as the architecture is still under active change and development. Our main Rust repository contains three major components:

 - saito-core
 - saito-rust  
 - saito-wasm  

**Saito-Core** contains the majority of the code that runs the blockchain. This code is intended to be compiled into a binary package that can also be deployed to browsers (and integrated with other programming languages). Clients that use this optimized bundle will simply need to pass a series of handlers into the code on initialization that will receive outbound messages and handle language-specific tasks like networking and data storage.

**Saito-Rust** contains the Rust-specific code that makes **Saito-Core** fully functional. It initializes the components contained in **Saito-Core**, and passes them the Network and Storage handlers needed for the core components to save the blockchain and interact with the network.

**Saito-Wasm** contains the middleware needed for javascript clients and applications to interact with **Saito-Core**. It is needed by javascript applications that want to run full or lite-nodes. Our goal is to eventually replace the current javascript client with one that uses **Saito-Wasm** to interact with the compiled **Saito-Core** codebase.

## Limitations

The Rust software is under heavy development. It is not intended to be a useable network client for third-party developers. You are welcome to download the software, and participate in development. Or just explore the repository and see how we are doing.

Developers should note that the Rust client does not currently support anything other than transaction processing. There is no built-in server on which applications can be deployed or installed.
