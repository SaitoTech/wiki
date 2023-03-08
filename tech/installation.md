---
title: Installation Instructions
description: Saito Node Installation Instructions
published: true
date: 2023-03-08T02:34:56.978Z
tags: 
editor: markdown
dateCreated: 2022-01-18T09:49:16.786Z
---

# Installation

This page contains instructions on how to download and install the NodeJS JavaScript client which currently forms the backbone of the network and is the best platform for developing applications and learning how Saito works. We have a Rust client under development with its own [installation instructions](https://wiki.saito.io/en/tech/installation-rust).

#### Requirements:

* Build tools: git, g++, make, python, tsc
* Stack: node.js (v.16+), npm (v6+)
* TypeScript

If you do not have these dependencies installed on your machine, we have instructions on how to install the necessary packages for [MacOS](/tech/installation/mac), [Ubuntu Linux](/tech/installation/linux) and [Windows](/tech/installation/windows). If you run into problems please flag so we can keep these pages updated as system requirements change.

#### 1. Install Dependencies

```
sudo apt-get update
sudo apt-get install g++ make git python node-typescript
curl -sL https://deb.nodesource.com/setup_16.x | sudo -E bash
sudo apt-get install -y nodejs
```

#### 2. Download Saito

Saito is open source software. The latest version of the Saito code is always available in our public [Github repository](https://github.com/saitotech/saito-lite-rust).
> Note: do not clone into ```/var/www/``` as this will cause webpack to error during compilation.

```
git clone https://github.com/saitotech/saito-lite-rust
cd saito-lite-rust
npm install -g typescript 
npm install
```

#### 3. Compile and Run Saito

After you have downloaded the software, you need to run our compile script. This will delete any previously-existing databases and create fresh versions of the configuration files that Saito needs to run properly. It also compiles a compressed version of Saito for use in browsers.

```
npm run nuke
npm start
```

##### 3.1 Compilation Types

There are two compilation options:

```npm run compile``` - creates the client JavasScript and CSS for deployment or testing and leaves the blockchain and other data structures in tact. Use this option during development.

```npm run nuke``` - creates the client JavaScript and CSS for deployment or testing, deletes the blockchain and data structures. This command also creates a clean ```./config/options``` file (```.config/options.conf``` is used as a template if it exists) and updates ```.config/modules.config.js``` file (```.config/modules.default.js``` is used as a template if the ```modules.config.js``` files does not exist.

##### 3.1 Compilation 'dev' Flag

Both the `compile` and `nuke` scripts can be run with a `dev` flag:
```npm run compile dev``` and ```npm run nuke dev```

When this flag is used:

 * JavaScript is not minimised and source maps are shipped with the code 
   The payload is 2 to 3 times larger but in browser debugging is possible.
   
* CSS files are linked (```@include()``` CSS source files, rather than being a concatentation of the source CSS).
  Many more files are downloaded by the client, but in browser debugging is possible.
  
  ---


#### 3. Visit Saito in your Browser

Once you have run `npm start` above it will take a few moments for the Saito software to initialize and start. You will eventually see an animated Saito logo scroll across your terminal. Once that is done simply open a browser and visit:

https://localhost:12101/arcade

This will load the Saito Arcade - one of our default applications. If everything goes as plans, you now have a working version of Saito for use in local testing or development. Why not get take your next steps by checking out [tutorial one](https://wiki.saito.io/en/tech/tutorial-1-deploy-install-application) which demonstrates how to build a simple application that attaches data to transactions and broadcasts them into the network.



