---
title: Core
description: 
published: true
date: 2025-04-17T06:14:37.357Z
tags: 
editor: markdown
dateCreated: 2024-09-17T08:16:38.266Z
---

# Core Development

This page provides information on the full Saito Software Stack, including [Saito's Core Node](https://github.com/saitotech/saito-rust-workspace) software. Developers who want to audit or modify the core Saito protocol or client software should focus on *Saito Rust.*

If you're simply looking to build applications, go [here](/tech/applications/building_apps).


## [Saito Rust](/tech/install/rust)
The core software is the Saito Rust client. This consists of a command-line client programmed in Rust that is intended to serve as a high-throughput network node. This is the version of Saito you want to be running if you are installing the software for use processing a high-throughput blockchain. This repository also includes the consensus-level classes (block, transaction, peer, network) that are compiled into the WASM binary that other clients use.

## [Saito WASM](/tech/install/wasm)

The Saito WASM library is compiled from the Rust code to create a compact binary library that can be used by programs written in other languages like javascript and python. The in-browser javascript wallet uses this WASM binary in order to run its own in-browser client.

If you update Saito Rust codebase and want to make those changes "visible" to applications or clients coded in different languages (like javascript) you will need to compile a new version of the Saito WASM binary so that your non-Rust software is using the version of Saito that has the changes you have made. 

## [SLR - Saito Lite Rust](/tech/install/javascript)

Saito Lite (Rust) is a Saito client written in javascript that is intended for use in web browsers. This is the version of Saito that you are using when you visit [saito.io](https://saito.io) and use the applications in your browser.

Saito Lite (Rust) uses the compiled WASM library to run a Saito client. It defines  provides most support for most of the functions that applications will want to use. Most of the time if you are building Saito Applicaitons this is the version of Saito that you will want to be installing and playing with.

Applications like the [Saito Arcade](https://saito.io/arcade) are built using this client. If you are interested in building applications rather than contributing to core development, this is most likely what you need.


<!--
## Resources

 ### Networking API

Documentation on the networking API can be found [here](/tech/core).

### Source Code

For more code and documentation please visit our public GitHub repository:

https://github.com/saitotech

This repository includes older branches and versions which are not being maintained. If you are interested in developing on the public site, please make sure you are using the latest two live repositories:

 - https://github.com/saitotech/saito-lite-rust
   ( JavaScript )

 - https://github.com/saitotech/saito-rust-workspace
   ( Rust )
-->