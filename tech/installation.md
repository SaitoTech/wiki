---
title: Installation Instructions
description: Saito Node Installation Instructions
published: true
date: 2024-09-17T07:50:21.617Z
tags: 
editor: markdown
dateCreated: 2022-01-18T09:49:16.786Z
---

# Installation

This section of the Saito Wiki is intended for developers interested in building applications for Saito, or contributing to the development of the protocol and the core software that runs the nodes on the network.

## Quick Install - Ubuntu 22.04 (LTS) x64

Requirements:
- Machine with at least 2GB RAM.
- Domain
- Build tools: git, g++, make, python, tsc
- Stack: node.js (v.16+), npm (v6+)
- TypeScript
---
## 1) Install Dependencies
SSH to your VPS and run:
```
sudo apt-get update
sudo apt-get install g++ make git python3
curl -sL https://deb.nodesource.com/setup_16.x | sudo -E bash
sudo apt-get install -y nodejs
```

## 2) Download Saito
```
git clone https://github.com/saitotech/saito-lite-rust
cd saito-lite-rust
npm install
```
> note: in case npm fails to install a module, you might need to `sudo apt-get install python-is-python3`.
## 3) Compile and Run Saito
```
npm run nuke
npm start
```
## 4) Visit Saito in your Browser
Once you have run ```npm start``` it will take a few moments for the Saito software to initialize and start. You will eventually see an animated Saito logo scroll across your terminal. Once that is done simply open a browser and visit:
> http://localhost:12101


To visit your Saito instance on your VPS:
>http://<your_server_ip>:12101

To generate a custom options file make a `options.conf` on `config/` folder, now set your endpoint to your domain with the following:
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
Compile with ```npm run nuke```, final compiled file is on config/options


## Module and Application Development

Applications like the [Saito Arcade](https://saito.io/arcade) run inside the Saito Wallet, which receives on-chain and off-chain messages and passes them into the modules that are running inside the user wallet. If you want to get started building applications, we recommend starting with our tutorial series for new Application Developers.


## Core Client Installation and Development

Saito consists of three separate-but-related software packages. The following links contain more detailed information on these packages along with instructions on how to compile and install them under Linux. We have a separate page with installation instructions for [Mac users](/tech/installation/mac).

 - [Saito Rust](/tech/installation/rust)
 - [Saito WASM](/tech/installation/wasm)
 - [Saito Lite (Rust)](/tech/installation/javascript)
 
The Saito Rust client is a command-line application built to handle consensus and network operations. If you want to run a high-throughput network node this is the software you need.

The Saito WASM library is compiled from the Rust code and consists of a compact library that can be included in programs written in other programming languages like javascript and python. This section of our wiki also contains instructions on compiling a NPM package that contains this WASM code and makes it easy to write NodeJS applications atop Saito.

Saito Lite (Rust) is a lite-client coded in javascript and designed for binary compatibility with the Rust client. It uses the compiled WASM library to support an in-browser wallet that can send-and-receive both on-chain and off-chain messages and run Saito applications. Applications like the [Saito Arcade](https://saito.io/arcade) are built using this client. If you are interested in building applications rather than contributing to core development, this is most likely what you need.


## Installation

Please see the relevant sections above for detailed instructions on installing the software packages you need. If you are building applications you will only need to install Saito-Lite-Rust. If you are interested in contributing to protocol development you will need to install the Rust codebases as well.


## Configuration

Once you have installed Saito-Lite-Rust you will be ready to configure the server to run the applications you wish to support and provide them to browsers on-demand. This section covers these follow-on configuration steps.

Saito uses two main configuration files. The first is ```config/options``` which specifies network configuration options like the IP address on which the server runs and the ports it should open and the peers to which it should connect. A second ```config/modules.config.js``` file specifies which modules should run on the server and any browsers that connect to it.

Running ```npm run nuke``` will create fresh versions of these configuration files from template files that are stored in the ```config``` directory. It will also compiles a compressed version of Saito from the ```modules.config.js``` that will be fed out to browsers which connect to the server and request the default javascript.

You can always reset your client by running the "nuke" command, but if you wish to change the applications supported on your server without resetting the blockchain, you can run the following instruction instead:

```npm run compile```


#### Advanced Usage of the `compile` Script

The `compile` script supports additional logging options, which can be specified using the `--loglevel` or `-l` flags. This feature allows you to set the desired log level for the compilation process.

#### Usage:

To set a specific log level, use one of the following commands:

```bash
npm run compile -- --loglevel=<level>
```

or 
```
npm run compile -- -l <level>
```

Where level can be one of the following:

- error
- warn
- info
- trace
- debug
For example, to set the log level to 'warn', you can use either:

```
npm run compile -- --loglevel=warn


or

npm run compile -- -l warn

```


##### Javascript Client 'dev' Flag

Both the `compile` and `nuke` scripts can be run with a `dev` flag:

```
npm run compile dev
npm run nuke dev
```

When this flag is used:

 * JavaScript is not minimized and source maps are shipped with the code 
   The payload is 2 to 3 times larger than otherwise but makes in-browser 
   debugging possible.
   
 * CSS files are linked (```@include()``` CSS source files, rather than 
   being a concatentation of the source CSS). This makes CSS development
   slightly easier.
   
The result is that many more files are downloaded by the client, but in-browser debugging is much easier
  

## Using Saito in your Browser

Once you have run `npm start` above it will take a few moments for the Saito software to initialize and start. You will eventually see an animated Saito logo scroll across your terminal. Once that is done simply open a browser and visit:

https://127.0.0.1:12101/arcade

This will load the Saito Arcade - one of our default applications. If everything has gone as planned, you now have a working version of Saito for use in local testing or development. 

Take your next steps into application development with [tutorial one](https://wiki.saito.io/en/tech/tutorial-1-deploy-install-application) which explains how to build a simple application that attaches data to transactions and broadcasts them into the network.

### For more code and documentation please visit our public GitHub repository:

https://github.com/saitotech

This repository includes older branches and versions which are not being maintained. If you are interested in developing on the public site, please make sure you are using the latest two live repositories:

https://github.com/saitotech/saito-lite-rust
( JavaScript )
https://github.com/saitotech/saito-rust-workspace
( Rust )



