---
title: Install
description: 
published: true
date: 2025-05-20T15:10:14.817Z
tags: 
editor: markdown
dateCreated: 2024-10-15T23:32:31.744Z
---

# Installing Saito

This page assumes you want to run a node on the Saito network or develop Saito Apps. If you are interested in another software package see our [overview](/install/overview) of all Saito-related projects. 

### Installation Requirements:

- Machine with at least 2GB RAM.
- Build tools: git, g++, make, python, tsc
- Stack: node.js (v.16+), npm (v6+)
- TypeScript

Most development machines with NodeJS installed will have these packages available. If you are missing any we have dedicated pages to help you install these tools for [Linux](/install/linux), [Mac](/install/mac) and [Windows](/install/windows). Once you have NodeJS installed, continue with the instructions below.


### 1) Download Saito

```
git clone https://github.com/saitotech/saito
cd saito/node
npm install
```

**Note:** if ```npm install``` fails to install a module, you may need to install `python-is-python3` to work around the problem. On Ubuntu this can be done with ```sudo apt-get install python-is-python3```.

<br />


### 2) Compile Saito

```
npm run nuke
npm start
```

After a few moments, you should see a large Saito ASCII logo appear on your screen. This indicates that Saito is running normally and you can move on to the next step.

### 3) Visit Saito in your Browser

Once Saito has started-up you will see an animated Saito logo scroll across your terminal. That is the the sign that the server has started and is ready to receive requests. Congratulations! You can now open a browser and visit:

> http://localhost:12101

If you are installing Saito on a remote server you will need to update your configuration files prior to running ```npm start```. We have a quick guide covering the configuration changes needed for remote deployment in this [deployment guide](/install/deploy).
