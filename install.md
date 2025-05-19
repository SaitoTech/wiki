---
title: Install
description: 
published: true
date: 2025-05-19T12:59:20.113Z
tags: 
editor: markdown
dateCreated: 2024-10-15T23:32:31.744Z
---

# Install Saito

The default [Saito](https://github.com/saitotech/saito) client is programmed in NodeJS and serves Saito applications to browsers. It also serves as a contact point on the network for other wallets and servers that form the P2P network. This page contains instructions on how to setup a default node. 

## Installation Instructions

This page describes the Specific instructions for installing the necessary tools are available for [Linux](./javascript/linux), [Mac](./javascript/mac) and [Windows](./javascript/windows).

### Requirements:

- Machine with at least 2GB RAM.
- Build tools: git, g++, make, python, tsc
- Stack: node.js (v.16+), npm (v6+)
- TypeScript

We have dedicated pages describing the process of installing these prerequisite tools for [Linux](/install/linux), [Mac](/install/mac) and [Windows](/install/windows).

Once prerequisites are installed, the following instructions should be similar for Mac, Windows and the broader audience of Linux users; if you are not using Ubuntu, substitute in your package manager where appropriate.

### 1) Download Saito

```
git clone https://github.com/saitotech/saito
cd saito
npm install
```

**Note:** If ```npm install``` fails to install a module, you may need to install `python-is-python3` to work around the problem. On Ubuntu this can be done with ```sudo apt-get install python-is-python3```.

<br />


### 2) Compile Saito

```
npm run nuke
npm start
```

After a few moments, you should see a large Saito ASCII logo appear on your screen. This indicates that Saito is running normally and you can move on to the next step.

### 3) Visit Saito in your Browser

Once Saito has started-up you will see an animated Saito logo scroll across your terminal. That is the the sign that the server has started and is ready to receive requests. You can now open a browser and visit:

> http://localhost:12101

If you are running Saito on a remote server: 

>http://<your_server_ip>:12101

Visit your server and you will see further instructions on how to add modules to your server and restart it. At this point you can decide what modules you want to install and edit your configuration files to run the applications you want.

