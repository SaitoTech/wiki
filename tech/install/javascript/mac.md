---
title: Mac Installation Instructions
description: Installation Instructions -  Mac
published: true
date: 2024-11-16T21:59:48.769Z
tags: mac saito installation
editor: markdown
dateCreated: 2022-03-28T07:51:17.517Z
---

# Mac Installation Instructions

This page contains instructions on how to download and install the NodeJS javascript client on Windows. For instructions about installation on Ubuntu Click [here](./linux). We have a Rust client under development with its own [Installation Instructions](../rust).

## Requirements:

* OS: macOs 
* Build tools: git, node

#### 1. Install Dependencies

```
brew update
brew install node git python pyenv

```

#### 2. Download Saito from Github

Saito is open source software. The latest version of the Saito code is always available in our public [Github repository](https://github.com/saitotech/saito-lite-rust).

```
git clone https://github.com/saitotech/saito-lite-rust
cd saito-lite-rust
sudo npm install -g typescript 
npm install
```

NOTE: if you run into problems installing the dependencies and particularly if sqlite3 installation fails your base installation may lack ```pyenv``` or ```node-pre-gyp```. Please confirm you have installed the former as above, and try forcing a global installation of node-pre-gyp with ```npm install node-pre-gyp -g```. Then try ```npm install``` again. This [stackoverflow article](https://stackoverflow.com/questions/70098133/npm-error-cant-find-python-executable-in-macos-big-sur) may help.


#### 3. Compile and Run Saito

After you have downloaded the software, you need to run our compile script. This will delete any previously-existing databases and create fresh versions of the configuration files that Saito needs to run properly. It also compiles a compressed version of Saito for use in browsers.



```
./compile nuke
npm run dev
```
:warning: if step above throws an error:

```
sed -i -e 's/\r$//' compile
./compile nuke
npm run dev
```
If you ever update the javascript code or modify your configuration files to include additional modules, you will need to shutdown the server, re-run these two commands and then restart the server before your changes will take effect.


#### 3. Visit Saito in your Browser

Once you have run `npm run dev` above it will take a few moments for the Saito software to initialize and start. You will eventually see an animated Saito logo scroll across your terminal. Once that is done simply open a browser and visit:
https://localhost:12101/arcade

This will load the Saito Arcade - one of our default applications. If everything goes as plans, you now have a working version of Saito for use in local testing or development.

[Tutorial 1](https://wiki.saito.io/en/tech/tutorials/01) demonstrates how to build a simple application that connects to the network and renders content.




