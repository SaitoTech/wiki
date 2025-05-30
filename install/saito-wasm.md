---
title: Saito WASM - Installation Instructions
description: 
published: true
date: 2025-05-20T06:05:19.804Z
tags: 
editor: markdown
dateCreated: 2023-10-13T08:35:18.101Z
---

# Saito WASM

If you do not know what WASM is you do not need this page and should install the [default](/install) version of Saito. This page describes how to compile a custom Saito WASM binary from the code on your computer. A pre-compiled version of this software is already available and used by default by the other clients.

This means the only reason you will need to modify this code is if you want to program  the core Rust-defined code and add additional functions that apps written in other languages can use to interact with it -- sending data into the core software or fetching fata from it. The code in the ```/saito/rust/saito-wasm``` subdirectory is what handles this, and will need to be modified in this case.

To make changes to Saito-WASM, you must first ```compile``` the code and then ```link``` it to your external application. This page contains instructions on how to do this.

#### Requirements:

* WASM-Pack [ [download](https://rustwasm.github.io/wasm-pack/installer/) ]

#### Installation

There are two steps to getting the Saito WASM library. The library must first be ```compiled``` from the Rust codebase. The compiled library must then be ```linked``` to the Saito Javascript codebase so that your local copy is used instead of the pre-compiled version hosted on NPM. The following instructions work for most Linux environments.

```
sudo apt-get update && sudo apt install build-essential pkg-config libssl-dev
cd saito-rust-workspace
cp saito-rust/configs/config.template.json saito-rust/configs/config.json
cd saito-wasm
wasm-pack build --debug --target browser
```

Once you have compiled the software you can follow these instructions to (./saito-wasm/linking) link the binary version of the software you just compiled to your NodeJS version of Saito. This replaces the pre-compiled version of Saito that is used by the NodeJS version by default with the compiled version running on your machine.

**NOTE** -- if you are using a Mac** you will need [these instructions](./saito-wasm/mac) on compiling and linking the WASM library under MacOS instead.

