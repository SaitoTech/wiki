---
title: Core
description: 
published: true
date: 2024-09-17T08:16:38.266Z
tags: 
editor: markdown
dateCreated: 2024-09-17T08:16:38.266Z
---

# Core Client Installation and Development

Saito consists of three separate-but-related software packages. The following links contain more detailed information on these packages along with instructions on how to compile and install them under Linux. We have a separate page with installation instructions for [Mac users](/tech/installation/mac).

 - [Saito Rust](/tech/installation/rust)
 - [Saito WASM](/tech/installation/wasm)
 - [Saito Lite (Rust)](/tech/installation/javascript)
 
The Saito Rust client is a command-line application built to handle consensus and network operations. If you want to run a high-throughput network node this is the software you need.

The Saito WASM library is compiled from the Rust code and consists of a compact library that can be included in programs written in other programming languages like javascript and python. This section of our wiki also contains instructions on compiling a NPM package that contains this WASM code and makes it easy to write NodeJS applications atop Saito.

Saito Lite (Rust) is a lite-client coded in javascript and designed for binary compatibility with the Rust client. It uses the compiled WASM library to support an in-browser wallet that can send-and-receive both on-chain and off-chain messages and run Saito applications. Applications like the [Saito Arcade](https://saito.io/arcade) are built using this client. If you are interested in building applications rather than contributing to core development, this is most likely what you need.