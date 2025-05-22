---
title: Install
description: 
published: true
date: 2025-05-22T05:31:38.199Z
tags: 
editor: markdown
dateCreated: 2024-10-15T23:32:31.744Z
---

# Installing Saito

This page assumes you want to run a Saito node or develop Saito Apps using the default network client. If you are interested in running the command-line Rust client or another software package see our [overview](/install/overview) of all Saito-related resources.

### Installation Requirements:

- Machine with at least 2GB RAM.
- Build tools: git, g++, make, python, tsc
- Stack: node.js (v.16+), npm (v6+)
- TypeScript

You will need a machine with NodeJS and Git installed. If you are missing either of these tools we have dedicated pages to help you install them for [Linux](/install/linux), [Mac](/install/mac) and [Windows](/install/windows). The remainder of this tutorial assumes you have both packages installed and are comfortable using the command-line.


### 1) Download Saito

Clone the Saito repository and go into the ```node``` sub-directory. This is where the NodeJS version of Saito is located. Running ```npm install``` from here downloads all of the packages you will need to run your server, including a pre-compiled version of the Rust codebase located elsewhere in our repository.

```
git clone https://github.com/saitotech/saito
cd saito/node
npm install
```

**Note:** if ```npm install``` fails to install a module, you may need to install `python-is-python3` to work around the problem. On Ubuntu this can be done with ```sudo apt-get install python-is-python3```.

<br />


### 2) Compile Saito

The first instruction runs a script that compiles Saito into a compressed javascript file that can be served to browsers and contains the modules browsers will need to interact with it. The second starts the server:

```
npm run nuke
npm start
```

After a few moments, you should see a large Saito ASCII logo appear on your screen. This indicates that Saito is running normally and you can start using it!

### 3) Visit Saito in your Browser

Congratulations! You can now open a browser and visit:

> http://localhost:12101

Note that if you are installing Saito on a remote server and cannot access the server through localhost you will need to update your [server configuration file](/configuration/wallet) prior to running ```npm start```. We have a quick guide covering the configuration changes needed for remote deployment in this [deployment guide](/install/deploy).
