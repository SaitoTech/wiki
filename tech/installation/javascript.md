---
title: Saito Javascript - Installation Instructions
description: 
published: true
date: 2024-09-21T14:12:58.831Z
tags: 
editor: markdown
dateCreated: 2023-10-13T08:41:59.352Z
---

# Saito Javascript (saito-lite-rust)

The Saito repository that runs applications in the browser is a javascript client intended to be run directly in the browser. This application is coded as a lite-client capable of supporting SPV blocks but is techcally capable of supporting full-blocks and functioning as a full standalone application.

Our Github repository for this client is "saito-lite-rust", referring to the fact that this our lite-client ("saito-lite") coded to have binary-compatibility with data-sharing formats used in the main Rust codebase ("-rust"). To simplify development, this client will run using a pre-compiled version of the Saito WASM library by default, but can be configured to use a locally-compiled version of the Saito WASM library for development and debugging if needed.

#### Requirements:

* Build tools: git, g++, make, python, tsc
* Stack: node.js (v.16+), npm (v6+)
* TypeScript
* https://github.com/saitotech/saito-lite-rust ( JavaScript )

#### Installation

First, ensure your machine has NodeJS installed:

```
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install g++ make git python node-typescript
curl -sL https://deb.nodesource.com/setup_16.x | sudo -E bash
sudo apt-get install -y nodejs
```

Second, download the latest version of our Saito Javascript client and install it along with typescript:

> Note: do not clone into ```/var/www/``` as this will cause webpack to error during compilation.

```
git clone https://github.com/saitotech/saito-lite-rust
cd saito-lite-rust
npm install -g typescript 
npm install
```

Finally, compile and run the software. This requires entering the saito-lite-rust directory and running the following commands:

```
npm run nuke
npm start
```