---
title: Install
description: 
published: true
date: 2026-07-04T13:44:32.349Z
tags: 
editor: markdown
dateCreated: 2024-10-15T23:32:31.744Z
---

# Installing Saito

This page is for those interested in running a Saito node. If you are interested in installing Saito on a remove VPS, we recommend using our [remote deployment guide](/install/deploy) to automate installment on new machines. To install Saito on a local machine, we suggest the following instructions.

### Machine Requirements:

- Machine with at least 4GB RAM.
- Build tools: git, g++, make, python, tsc
- Stack: node.js (v.16+), npm (v6+)
- TypeScript

If you are missing any of these tools we have dedicated pages to help you install them for [Linux](/install/linux), [Mac](/install/mac) and [Windows](/install/windows).

### 1. Download Saito

Clone the official Saito repository and move into the ```node``` sub-directory. Run ```npm install``` to download all of the packages you will need to run Saito, including a pre-compiled version of the Rust codebase.

```
git clone https://github.com/saitotech/saito
cd saito/node
npm install
```

**Note:** if ```npm install``` fails to install a module, you may need to install `python-is-python3` to work around the problem. On Ubuntu this can be done with ```sudo apt-get install python-is-python3```.



### 2) Compile Saito

These instructions run a script that compiles Saito into a compressed javascript file that can be served to browsers and contains all of the modules your browsers will use. The second starts the server:

```
npm run nuke
npm start
```

After a few moments, you should see a large Saito ASCII logo appear on your screen. This indicates that Saito is running normally and you can start using it!

### 3) Visit Saito in your Browser

Congratulations! You can now open a browser and visit:

> http://localhost:12101

Ready to change the default set of modules on your machine? For detailed instructions on compiling the node.js stack refer to the [Compilation Guide](/install/compile). If you run into problems installing Saito on a remote machine, check the configuration changes needed for remote deployment in our [remote deployment guide](/install/deployment).


## Rust Client and WASM Support

The version of Saito that will be installed above includes the saito-js NPM package. This is a pre-compiled binary of the backend Rust code as a WASM object. This binary object is what handles consensus operations such as block and transaction validation and most network operations.

If you want to modify this backend code as part of development, it is easy to set this up, but it requires support for Rust to be installed, so we have a separate page with [instructions on how to compile and link](/install/full) the Rust backend code on your machine.
