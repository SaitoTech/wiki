---
title: Saito Javascript - Installation Instructions
description: 
published: true
date: 2024-11-01T00:11:50.654Z
tags: 
editor: markdown
dateCreated: 2023-10-13T08:41:59.352Z
---

# Saito Javascript (saito-lite-rust) Installation 

[Saito-Lite-Rust](https://github.com/SaitoTech/saito-lite-rust) (SLR) is primarily intended to serve and run applications in the browser via a Javascript Client. Saito-Lite-Rust runs atop NodeJS. Once the prerequisite software is installed, `npm` scripts to complete installation are provided.

## Installation Instructions

Specific instructions for installing the necessary tools are available for [Linux](/tech/installation/javascript/linux), [Mac](/tech/installation/javascript/mac) and [Windows](/tech/installation/javascript/windows).

### Requirements:
- Machine with at least 2GB RAM.
- Build tools: git, g++, make, python, tsc
- Stack: node.js (v.16+), npm (v6+)
- TypeScript
- Saito-Lite-Rust - [Github](https://github.com/saitotech/saito-lite-rust)

<hr>

Once prerequisites are installed, the following instructions should be similar for Mac, Windows and the broader audience of Linux users; if you are not using Ubuntu, substitute in your package manager where appropriate.

### 1) Download Saito

```
git clone https://github.com/saitotech/saito-lite-rust
cd saito-lite-rust
npm install
```
**Note:** If npm fails to install a module, you may need to install `python-is-python3`.

On Ubuntu:
`sudo apt-get install python-is-python3`

<br />


### 2) Compile and Run Saito
```
npm run nuke
npm start
```

If after a few moments with no errors a large Saito ASCII Logo appears on screen, move on to the next step.

It is common that errors at this stage are related to your NodeJS install, so consider first searching for NodeJS troubleshooting help if you can't get Saito running at this stage.

<br />

### 3) Visit Saito in your Browser
Once you have run ```npm start``` it will take a few moments for the Saito software to initialize and start. You will eventually see an animated Saito logo scroll across your terminal. Once that is done simply open a browser and visit:
> http://localhost:12101

To visit your Saito instance on your VPS:
>http://<your_server_ip>:12101
<!--
To generate a custom options file make a `options.conf` in the `config/` folder with the following content; be sure to set your endpoint to your domain:
```
{
	"server":{
		"host":"localhost",
		"port":12101,
		"protocol":"http"
		"endpoint":{
			"host":"your_domain.com",
			"port":12101,
			"protocol":"http"
		}
	}
}
```
-->

Any changes can be compiled with `npm run nuke`. The final compiled file will rest in `config/options`.

### Compilation and Configuration

- Visit the page [compiling and configuring](https://wiki.saito.io/tech/compile) for more information on setting up your SLR Node.

<br />

## Building Apps

You are now ready to modify, build and compile Saito applications. Head over to the [tutorial](https://wiki.saito.io/en/tech/applications/building_apps) section to get started!

<!-- this belongs on an info page not install
This application is coded as a lite-client capable of supporting SPV blocks but is techcally capable of supporting full-blocks and functioning as a full standalone application.

Our Github repository for this client is "saito-lite-rust", referring to the fact that this our lite-client ("saito-lite") coded to have binary-compatibility with data-sharing formats used in the main Rust codebase ("-rust"). To simplify development, this client will run using a pre-compiled version of the Saito WASM library by default, but can be configured to use a locally-compiled version of the Saito WASM library for development and debugging if needed.
-->

<!-- OLD AS HECK
#### Installation

First, ensure your machine has NodeJS installed:

```
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install g++ make git python node-typescript
curl -sL https://deb.nodesource.com/setup_16.x | sudo -E bash
sudo apt-get install -y nodejs
```

Second, download the latest version of our Saito Javascript client and install it along with typescript:

> Note: do not clone into ```/var/www/``` as this will cause webpack to error during compilation.

```
git clone https://github.com/saitotech/saito-lite-rust
cd saito-lite-rust
npm install -g typescript 
npm install
```

Finally, compile and run the software. This requires entering the saito-lite-rust directory and running the following commands:

```
npm run nuke
npm start
```
-->