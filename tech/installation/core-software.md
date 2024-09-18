---
title: Core
description: 
published: true
date: 2024-09-18T05:36:00.024Z
tags: 
editor: markdown
dateCreated: 2024-09-17T08:16:38.266Z
---

# Core Client Protocol and Documentation

This page is intended for developers working on core Saito software clients. If you just want to run a node, visit our tutorial on how to [run a node](/tech/installation). If you just want to build applications, we have a [tutorial series](/tech/building_apps) to get you started too.

The rest of this page starts by exploring the three separate-but-related software packages that make up the Saito stack. The first step to doing protocol development work is understanding where the code exists that you will want to modify/change/update.


### [Saito Rust](/tech/installation/rust)
The Saito Rust client is a command-line client programmed in Rust and intended to server as a high-throughput network node. This is the version of Saito that you want to be running if you are installing the software for use in a colocation facility. This also includes the core consensus-level classes (block, transaction, peer, network) that other clients use, and is the best source of documentation on how the core protocol works.

### [Saito WASM](/tech/installation/wasm)

The Saito WASM library is compiled from the Rust code and consists of a compact library that exists in binary form and thus can be used by programs written in other languages like javascript and python that want to run a Saito node or otherwise interact with the Rust codebase.

If you update Saito Rust codebase and want to make those changes "visible" to applications or clients coded in different languages (like javascript) you will need to compile a new version of the Saito WASM binary so that your non-Rust software is using the version of Saito that has the changes you have made. 

### [Saito Lite (Rust)](/tech/installation)

Saito Lite (Rust) is a Saito client that is written in javascript and intended for use primarily in web-browsers. This is the version of Saito that you are using when you visit [saito.io](https://saito.io) and use the applications in your browser.

Saito Lite (Rust) uses the compiled WASM library to run a Saito client that can send-and-receive both on-chain and off-chain messages. It also includes support for most of the functions that applications will want to use. Most of the time if you are building Saito Applicaitons this is the version of Saito that you will want to be installing and playing with.

Applications like the [Saito Arcade](https://saito.io/arcade) are built using this client. If you are interested in building applications rather than contributing to core development, this is most likely what you need.

## Networking API

Documentation on the networking API can be found [here](/tech/core).

## External Resources

For more code and documentation please visit our public GitHub repository:

https://github.com/saitotech

This repository includes older branches and versions which are not being maintained. If you are interested in developing on the public site, please make sure you are using the latest two live repositories:

 - https://github.com/saitotech/saito-lite-rust
   ( JavaScript )

 - https://github.com/saitotech/saito-rust-workspace
   ( Rust )