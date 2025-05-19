---
title: Install
description: Installation directory for various Saito clients
published: true
date: 2025-05-19T16:12:34.034Z
tags: 
editor: markdown
dateCreated: 2024-11-20T02:40:42.538Z
---

# Install

If you are new to Saito and want to start using the network to play around with software development, you probably want our [install instructions](/install) for the Saito client. This is the server that runs on [saito.io](https://saito.io) and supports most of the web3 applications in common use. This page is for developers who want a deeper understanding of what Saito is and its parts.

Specifically, if you download the [Saito Repository](https://github.com/saitotech/saito) you'll see there are a number of sub-folders organized in two main directories. The ```node``` sub-directory contains the main Saito client and is what 99% of developers will want to install and use. It is coded in NodeJS and most development work is in javascript. The ```rust``` subdirectory contains more specialized and high-performance software coded in the Rust programming language, including a version of the client that simply focuses on high-performance routing.

This page offers a quick introduction to the various major software packages that combine to form the Saito project. It is intended to provide a brief overview for developers and is of primary use to those who wish to do lower-level consensus development.


## Saito

The 'official' Saito-Lite client is written in NodeJS and designed to run web3 applications and support browser wallest. If you are developing apps or want to run a node on the network this is most likely the software you want. All of the applications available on [saito.io](https://saito.io) were built atop this client and application developers will find it immediately useful for building peer-to-peer applications.

- [Github Repository](https://github.com/saitotech/saito/tree/master/node)

- [Installation instructions](./install/javascript)


## Saito-Core

Embedded within the Saito application above is a special core of Rust-software with the cryptographic functions and consensus logic used by the blockchain. A version of this is compiled and included by default in the NodeJS application, but it is available for inspection and development in the main repository. Those interested in blockchain operations can find the main files at ```/saito/rust/saito-core/src/core/consensus```.

- [Github Repository](https://github.com/saitotech/saito/tree/master/rust/saito-core)

- [Installation instructions](./install/saito-core)


## Saito-Rust

This distribution contains a pure Rust implementation of Saito Consensus in the the form of a Rust client. This is a high-performance client designed for high-throughput nodes. It differs from the NodeJS client in that it does not support offering web3 applications or data to connecting clients.

- [Github Repository](https://github.com/saitotech/saito/tree/master/rust/saito-rust)

- [Installation instructions](./install/saito-rust)



## Saito-WASM

The software in the Saito-Core repository is made available to the NodeJS javascript client as a binary WASM file. The code in this directory provides the support needed to generate this file. The installation instructions below include instructions on compiling this package and linking it with the NodeJS package. 

- [Github Repository](https://github.com/saitotech/saito/tree/master/rust/saito-wasm)

- [Installation instructions](./install/saito-wasm)

