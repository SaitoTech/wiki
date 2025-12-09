---
title: Install
description: 
published: true
date: 2025-12-09T02:55:23.673Z
tags: 
editor: markdown
dateCreated: 2024-10-15T23:32:31.744Z
---

# Installing Saito

This page assumes you want to run the NodeJS Saito node (best for app hosting and development!). If you are interested in running the command-line Rust client or another software package see our [overview](/install/overview) of all Saito-related resources.


If you are unsure what you want to do read [Running a Saito Node](running_a_node) for more information.

# Options

Install a local development node (Get started for module development) SEE BELLOW

[Install a Web Node](/install-web) (Can run modules like chat, redsquare and videocall)

Intsall a rust rouding node (Heavy duty routing node with no front end) TBD

## Requirements

* A computer/server with 4GB of RAM and two modern processor cores.
* A connection with 5MB/s download capacity

To share blocks:
* Public IP address or domain name. (We use and recommend [Lets Encrypt](https://letsencrypt.org/) for SSL certificates.
* A constant 5MB/s connection (both directions) to the internet.

*Note: these requirements, particularly bandwidth, will increase as network throughput increases.*


## Quick Deploy Script
Please read the below and the  [deployment guide](/install/deploy) so you understand the steps undertaken, but if you just want to get a node running, use this:
**[Quick Deploy Script for Ubuntu 24.04](https://gist.github.com/arpee/22cec55b8e74c09c2e17e5a42eead6cf)**.

---

### Installation Requirements:

- Machine with at least 4GB RAM.
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

#### Quick Unbunto 24.04 instructions:
```
apt install npm
git clone https://github.com/saitotech/saito
cd saito/node
npm install
```

<br />


### 2) Compile Saito

The first instruction runs a script that compiles Saito into a compressed javascript file that can be served to browsers and contains the modules browsers will need to interact with it. The second starts the server:

```
npm run nuke
npm start
```

For detailed instructions on compiling the node.js stack refer to the [Compilation Guide](/install/compile).

After a few moments, you should see a large Saito ASCII logo appear on your screen. This indicates that Saito is running normally and you can start using it!

### 3) Visit Saito in your Browser

Congratulations! You can now open a browser and visit:

> http://localhost:12101

Note that if you are installing Saito on a remote server and cannot access the server through localhost you will need to update your [server configuration file](/configuration/wallet) prior to running ```npm start```. We have a quick guide covering the configuration changes needed for remote deployment in this [deployment guide](/install/deploy).
