---
title: Windows Installation
description: 
published: true
date: 2022-05-30T09:53:07.391Z
tags: 
editor: markdown
dateCreated: 2022-05-30T09:53:07.391Z
---

# Windows Installation

#### Requires:

* build tools: git, g++, make, python, tsc
* node.js (v.16+), npm (v6+)
* typescript

#### 1. Download Saito

Saito is open source software. The latest version of the Saito code is always available in our public [Github repository](https://github.com/saitotech/saito-lite-rust).

```
git clone https://github.com/saitotech/saito-lite-rust
cd saito-lite-rust
npm install -g typescript 
npm install
```

#### 3. Compile and Run Saito

After you have downloaded the software, you need to run our compile script. This will delete any previously-existing databases and create fresh versions of the configuration files that Saito needs to run properly. It also compiles a compressed version of Saito for use in browsers.

```
npm run init
npm run dev
```

If you ever update the javascript code or modify your configuration files to include additional modules, you will need to shutdown the server, re-run these two commands to recompile the javascript code.


#### 3. Visit Saito in your Browser

Once you have run `npm run dev` above it will take a few moments for the Saito software to initialize and start. You will eventually see an animated Saito logo scroll across your terminal. Once that is done simply open a browser and visit:

https://localhost:12101/arcade

This will load the Saito Arcade - one of our default applications. If everything goes as plans, you now have a working version of Saito for use in local testing or development. Why not get take your next steps by checking out [our very first tutorial](https://wiki.saito.io/en/tech/tutorials/tutorial-1) which demonstrates how to build a simple application that attaches data to transactions and broadcasts them into the network.
