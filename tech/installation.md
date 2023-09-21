---
title: Installation Instructions
description: Saito Node Installation Instructions
published: true
date: 2023-09-21T10:03:31.795Z
tags: 
editor: markdown
dateCreated: 2022-01-18T09:49:16.786Z
---

# Installation

Saito consists of three separate-but-related software packages. This page contains instructions on installing and compiling all three packages as well as testing that they are working properly once setup:

 - Saito Rust
 - Saito WASM
 - Saito Javascript
 
The Saito Rust client is a command-line application built to handle consensus and network operations. If you want to run a high-throughput network node this is the software you need.

The Saito WASM library is compiled from the Rust code and consists of a compact library that can be included in programs written in other programming languages like javascript and python to permit them to host wallets and run Saito applications.

The javascript client uses the WASM library to create an in-browser application stack that can send-and-receive both on-chain and off-chain messages and run Saito applications. Applications like the [Saito Arcade](https://saito.io/arcade) are built using this client. If you are interested in building applications rather than contributing to core development, you should start with the javascript client.


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
git checkout develop
cd saito-rust
cp configs/config.template.js configs/config.json
RUST_LOG=debug cargo run --bin saito-rust
```

## Saito WASM

Saito WASM is a version of the Rust core compiled into a portable library that can interact with other programming languages like javascript. To use Saito WASM you must first ```compile``` the code and then ```link``` it to your external application.

#### Requirements:

* WASM-Pack [ [download](https://rustwasm.github.io/wasm-pack/installer/) ]

#### Installation

There are two steps to getting the Saito WASM library. The library must first be ```compiled``` from the Rust codebase. The compiled library must then be ```linked``` to the Saito Javascript codebase so that your local copy is used instead of the pre-compiled version hosted on NPM.

The following instructions work for most Linux environments. If you are using a Mac you will need [these instructions](/tech/linking_installations_mac) on compiling and linking the WASM library under MacOS instead.

```
sudo apt-get update && sudo apt install build-essential pkg-config libssl-dev
cd saito-rust-workspace
cp saito-rust/configs/config.template.json saito-rust/configs/config.json
cd saito-wasm
wasm-pack build --debug --target browser
```

## Saito Javascript

Saito Javascript is an in-browser lite-client that runs directly in the browser. It uses a compiled version of the Rust client by default, but can be connected to a locally-compiled version of the Saito WASM library for core development if needed.

#### Requirements:

* Build tools: git, g++, make, python, tsc
* Stack: node.js (v.16+), npm (v6+)
* TypeScript
* https://github.com/saitotech/saito-lite-rust ( JavaScript )

#### Installation

First, ensure your machine has NodeJS installed:

```
sudo apt-get update
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

#### Configuration

Saito uses two main configuration files. The first is ```config/options``` which specifies network configuration options like the IP address on which the server runs and the ports it should open and the peers to which it should connect. A second ```config/modules.config.js``` file specifies which modules should run on the server and any browsers that connect to it.

Running ```npm run nuke``` will create fresh versions of these configuration files from template files that are stored in the ```config``` directory. It will also compiles a compressed version of Saito from the ```modules.config.js``` that will be fed out to browsers which connect to the server and request the default javascript.

You can always reset your client by running the "nuke" command, but if you wish to change the applications supported on your server without resetting the blockchain, you can run the following instruction instead:

```npm run compile```


##### Javascript Client 'dev' Flag

Both the `compile` and `nuke` scripts can be run with a `dev` flag:

```
npm run compile dev
npm run nuke dev
```

When this flag is used:

 * JavaScript is not minimized and source maps are shipped with the code 
   The payload is 2 to 3 times larger than otherwise but makes in-browser 
   debugging possible.
   
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



