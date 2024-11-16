---
title: Saito WASM - Installation Instructions
description: 
published: true
date: 2024-10-16T01:14:42.252Z
tags: 
editor: markdown
dateCreated: 2023-10-13T08:35:18.101Z
---

# Saito WASM

Saito WASM is a version of the Rust core compiled into a portable library that can interact with other programming languages like javascript. To use Saito WASM you must first ```compile``` the code and then ```link``` it to your external application.

#### Requirements:

* WASM-Pack [ [download](https://rustwasm.github.io/wasm-pack/installer/) ]

#### Installation

There are two steps to getting the Saito WASM library. The library must first be ```compiled``` from the Rust codebase. The compiled library must then be ```linked``` to the Saito Javascript codebase so that your local copy is used instead of the pre-compiled version hosted on NPM.

The following instructions work for most Linux environments. **If you are using a Mac** you will need [these instructions](/tech/linking_installations_mac) on compiling and linking the WASM library under MacOS instead.

```
sudo apt-get update && sudo apt install build-essential pkg-config libssl-dev
cd saito-rust-workspace
cp saito-rust/configs/config.template.json saito-rust/configs/config.json
cd saito-wasm
wasm-pack build --debug --target browser
```

