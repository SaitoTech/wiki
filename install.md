---
title: Install
description: 
published: true
date: 2026-01-19T06:50:27.269Z
tags: 
editor: markdown
dateCreated: 2024-10-15T23:32:31.744Z
---

# Installing Saito

This page assumes you want to run the NodeJS Saito server locally run or develop applications like the Saito Arcade, Videocall, or RedSquare. If you want to run Saito on a remote machine, we have a [remote deployment guide](/install/deploy) that includes a script which automates entire setup process. The rest of this page assumes you are installing on a local machine.

### Installation Requirements:

- Machine with at least 4GB RAM.
- Build tools: git, g++, make, python, tsc
- Stack: node.js (v.16+), npm (v6+)
- TypeScript

If you are missing any of these tools we have dedicated pages to help you install them for [Linux](/install/linux), [Mac](/install/mac) and [Windows](/install/windows). The remainder of these instructions assumes you have these packages installed and are comfortable using the command-line.


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


## Development Setup

### 1. Git clone repo
```
git clone https://github.com/saitotech/saito
```

### 2. Run dev setup script
```
cd <repo>/rust/scripts
./dev_setup.sh
```

Provide any expected inputs and wait till the script completes. Script will install all the required software, compile the code and locally link the npm packages.

### 3. Link local saito-js package

```
cd <repo>/node/
npm install
npm link saito-js
npm run reset
```