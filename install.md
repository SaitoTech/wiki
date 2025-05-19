---
title: Install
description: 
published: true
date: 2025-05-19T16:16:51.037Z
tags: 
editor: markdown
dateCreated: 2024-10-15T23:32:31.744Z
---

# Installing Saito

This page assumes you want to run a node on the Saito network or develop Saito Apps. This page walks you through the process of installing the default Saito client. On a machine with standard dev-tools installed, the process should take about 10 minutes. If you are looking to install something else, we have an [overview](/install/overview) of several other Saito-related software packages.

### Installation Requirements:

- Machine with at least 2GB RAM.
- Build tools: git, g++, make, python, tsc
- Stack: node.js (v.16+), npm (v6+)
- TypeScript

Most development machines will have these packages installed. If your machine does not we have dedicated pages describing the process of installing these tools for [Linux](/install/linux), [Mac](/install/mac) and [Windows](/install/windows).

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

