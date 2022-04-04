---
title: Mac Installation Instructions
description: Installation Instructions -  Mac
published: true
date: 2022-03-28T08:22:16.987Z
tags: mac saito installation
editor: markdown
dateCreated: 2022-03-28T07:51:17.517Z
---

# Mac Installation Instructions
This page contains instructions on how to download and install the NodeJS javascript client on MacOs. For instructions about installation on Ubuntu <a href="https://wiki.saito.io/en/tech/installationt"> Click here</a>. We have a Rust client under development with its own <a href="https://wiki.saito.io/en/tech/installation-rust"> Installation Instructions</a>


## Requirements:

* OS: macOs 
* Build tools: git, node


#### 1. Install Dependencies

```
brew update
brew install node git python

```

#### 2. Download Saito from Github

Saito is open source software. The latest version of the Saito code is always available in our public [Github repository](https://github.com/saitotech/saito-lite-rust).

```
git clone https://github.com/saitotech/saito-lite-rust
cd saito-lite-rust
sudo npm install -g typescript 
npm install
```




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

(https://wiki.saito.io/en/tech/tutorials/tutorial-1) which demonstrates how to build a simple application that attaches data to transactions and broadcasts them into the network.




