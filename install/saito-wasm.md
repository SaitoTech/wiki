---
title: Saito WASM - Installation Instructions
description: 
published: true
date: 2025-05-19T15:35:26.365Z
tags: 
editor: markdown
dateCreated: 2023-10-13T08:35:18.101Z
---

# Saito WASM

First things first, if you do not know what WASM is you do not need this page and should look at installing the [default](/install) version of Saito instead. This version uses a version of the Saito WASM client that is precompiled and will support everything you need to run the software.

The reason you will need to modify this code is if you want to modify the core Rust-defined code and add additional functions that apps written in other languages can use to interact with it -- sending data into the core software or fetching fata from it. The code in the ```/saito/rust/saito-wasm``` subdirectory is what handles this, and will need to be modified in this case.

To make changes to Saito-WASM, you must first ```compile``` the code and then ```link``` it to your external application. This page contains instructions on how to do this.

#### Requirements:

* WASM-Pack [ [download](https://rustwasm.github.io/wasm-pack/installer/) ]

#### Installation

There are two steps to getting the Saito WASM library. The library must first be ```compiled``` from the Rust codebase. The compiled library must then be ```linked``` to the Saito Javascript codebase so that your local copy is used instead of the pre-compiled version hosted on NPM.

The following instructions work for most Linux environments. **If you are using a Mac** you will need [these instructions](./saito-wasm/mac) on compiling and linking the WASM library under MacOS instead.

```
sudo apt-get update && sudo apt install build-essential pkg-config libssl-dev
cd saito-rust-workspace
cp saito-rust/configs/config.template.json saito-rust/configs/config.json
cd saito-wasm
wasm-pack build --debug --target browser
```

