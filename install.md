---
title: Install
description: 
published: true
date: 2026-10-20T09:12:35.929Z
tags: 
editor: markdown
dateCreated: 2024-10-15T23:32:31.744Z
---

# Installing Saito

This page is for those interested in running a Saito node. If you are installing Saito on a remote VSP, we recommend using our [remote deployment script](/install/deploy) to automate installment. To install Saito on a local machine, we suggest the instructions below.

### Machine Requirements:

- Machine with at least 4GB RAM.
- Build tools: git, g++, make, python, tsc
- Stack: node.js (v.16+), npm (v6+)
- TypeScript

Instructions for installing these tools are available for [Linux](/install/linux), [Mac](/install/mac) and [Windows](/install/windows).

### 1. Download Saito

Download Saito from the official github repository. The server software is in the ```node``` sub-directory. Navigate into it and run ```npm install``` to install the supporting packages.

```
git clone https://github.com/saitotech/saito
cd saito/node
npm install
```


### 2) Compile Saito

Run the following scripts. The first compiles Saito into a compressed javascript file that contains all of the modules your browsers will use. The second starts the server:

```
npm run nuke
npm start
```

After a few moments, you should see a large Saito ASCII logo appear on your screen. This indicates that Saito is running normally and you can start using it!

### 3) Visit Saito in your Browser

You can now open a browser and visit:

> http://localhost:12101/admin

Follow the instructions in your browser to [configure](/config) your server.


## Troubleshooting

* if ```npm install``` fails to install a module, you may need to install `python-is-python3` to work around the problem. On Ubuntu this can be done with ```sudo apt-get install python-is-python3```.

* Saito is configured to use a pre-compiled version of the backend Rust software. If you wish to compile your own locally, we have a separate page with [instructions on how to compile and link](/install/full) the full Rust code on your machine.
