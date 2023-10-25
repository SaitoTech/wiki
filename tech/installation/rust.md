---
title: Saito Rust - Installation Instructions
description: 
published: true
date: 2023-10-25T16:17:07.851Z
tags: 
editor: markdown
dateCreated: 2023-10-13T08:32:52.212Z
---

# Saito Rust

The Saito Rust client is the main network client. Compiling it requires the standard command-line tools bundled with X-Code in Mac and included with most  most Linux distributions. On Ubuntu you can install them as follows:

#### Requirements

* OS: Ubuntu 20.04 (MacOS instructions)
* Build tools: git, g++, make
* Stack: cargo rust (v.1.5.7+)
* https://github.com/saitotech/saito-rust-workspace

#### Installation
```
git clone https://github.com/saitotech/saito-rust-workspace
cd saito-lite-workspace
git checkout develop
cd saito-rust
cp configs/config.template.json configs/config.json
RUST_LOG=debug cargo run --bin saito-rust
```
