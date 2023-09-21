---
title: Installation Instructions
description: Saito Node Installation Instructions
published: true
date: 2023-09-21T07:29:29.308Z
tags: 
editor: markdown
dateCreated: 2022-01-18T09:49:16.786Z
---

# Installation

Saito consists of a Rust client that participates in the blockchain and handles consensus and network operations. The Rust client can be compiled into a WASM library that is used by a javascript-wallet that runs applications in the browser.

## Saito Rust

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
RUST_LOG=debug cargo run
```
For those interested in exploring the Rust codebase, we have a separate page on [Rust Architecture and Design](/tech/rust-architecture). This briefly describes the organization of the repository for those interested in digging into the code itself.

## Saito WASM

Saito WASM is a library created by compiling parts of the core Rust software into WASM. This library provides a way for other languages like javascript to bundle Saito into other applications and interact with the software.

#### Requirements:

In addition to the tools required for installation of Saito Rust:

* WASM-Pack [download](https://rustwasm.github.io/wasm-pack/installer/)

#### Installation
```
sudo apt-get update && sudo apt install build-essential pkg-config libssl-dev
cd saito-rust-workspace
cp configs/saito.config.template.json configs/saito.config.json
cd saito-wasm
wasm-pack build --debug --target browser
```

## Saito Javascript

Saito Javascript is an in-browser lite-client that runs directly in the browser. The current version uses a compiled version of the Rust client which cna be compiled as above or downloaded from NPM as our saito-js library.

#### Requirements:

* Build tools: git, g++, make, python, tsc
* Stack: node.js (v.16+), npm (v6+)
* TypeScript
* https://github.com/saitotech/saito-lite-rust ( JavaScript )

#### Install Prerequisites

```
sudo apt-get update
sudo apt-get install g++ make git python node-typescript
curl -sL https://deb.nodesource.com/setup_16.x | sudo -E bash
sudo apt-get install -y nodejs
```

#### Install Saito-Lite-Rust

The latest version of the Saito code is always available in our public [Github repository](https://github.com/saitotech/saito-lite-rust).

> Note: do not clone into ```/var/www/``` as this will cause webpack to error during compilation.

```
git clone https://github.com/saitotech/saito-lite-rust
cd saito-lite-rust
npm install -g typescript 
npm install
```

#### Compile and Run Saito

After you have downloaded the software, you need to "nuke" your Saito installation to prepare it to run. This will delete any previously-existing databases and create fresh versions of the configuration files that Saito needs to run properly.  This command creates a clean ```./config/options``` file and a ```.config/modules.config.js``` file from the template files in those directories (if not exists).

```
npm run nuke
npm start
```
This compilation process also compiles a compressed version of Saito that will be fed out to any browsers that connect to your server. You can control which applications/modules will be included with this by editing your ```.config/modules.config.js``` file.

If you wish to change the applications supported on your server without resetting the blockchain, you can run the following instruction instead of "nuke"

```npm run compile```


##### Development 'dev' Flag

Both the `compile` and `nuke` scripts can be run with a `dev` flag:
```npm run compile dev``` and ```npm run nuke dev```

When this flag is used:

 * JavaScript is not minimised and source maps are shipped with the code 
   The payload is 2 to 3 times larger but in-browser debugging is possible.
   
 * CSS files are linked (```@include()``` CSS source files, rather than 
   being a concatentation of the source CSS). This makes CSS development
   slightly easier.
   
The result is that many more files are downloaded by the client, but in-browser debugging is much easier
  

## Using Saito in your Browser

Once you have run `npm start` above it will take a few moments for the Saito software to initialize and start. You will eventually see an animated Saito logo scroll across your terminal. Once that is done simply open a browser and visit:

https://127.0.0.1:12101/arcade

This will load the Saito Arcade - one of our default applications. If everything has gone as planned, you now have a working version of Saito for use in local testing or development. 

Take your next steps into application development with [tutorial one](https://wiki.saito.io/en/tech/tutorial-1-deploy-install-application) which explains how to build a simple application that attaches data to transactions and broadcasts them into the network.

### For more code and documentation please visit our public GitHub repository:

https://github.com/saitotech

This repository includes older branches and versions which are not being maintained. If you are interested in developing on the public site, please make sure you are using the latest two live repositories:

https://github.com/saitotech/saito-lite-rust
( JavaScript )
https://github.com/saitotech/saito-rust-workspace
( Rust )



