---
title: Linux Installation
description: Linux SLR Installation Instructions
published: true
date: 2024-11-16T21:54:14.873Z
tags: 
editor: markdown
dateCreated: 2022-01-18T09:49:16.786Z
---

# Linux Installation

The instructions below are for developers building on Linux. We have separate installation instructions for [Mac users](./mac) and [Windows users](./windows).


### 1) Install Dependencies (Ubuntu 22.04 (LTS) x64)
```
sudo apt-get update
sudo apt-get install g++ make git python-is-python3 npm
curl -sL https://deb.nodesource.com/setup_16.x | sudo -E bash
sudo apt-get install -y nodejs
```

<br />

### 2) Download Saito

The following instructions should be similar for Mac, Windows and the broader audience of Linux users; if you are not using Ubuntu, substitute in your package manager where appropriate.

```
git clone https://github.com/saitotech/saito-lite-rust
cd saito-lite-rust
npm install
```
**Note:** If npm fails to install a module, you may need to install `python-is-python3`.

On Ubuntu:
`sudo apt-get install python-is-python3`

<br />


### 3) Compile and Run Saito
```
npm run nuke
npm start
```

If after a few moments with no errors a large Saito ASCII Logo appears on screen, move on to the next step.

If you do see an error, it is common that errors at this stage are related to your NodeJS install, be sure each of the dependencies is properly installed.

<br />

### 4) Visit Saito in your Browser
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

<br />

### Compilation and Configuration

- Visit the page [compiling and configuring](https://wiki.saito.io/tech/compile) for more information on setting up your SLR Node.


