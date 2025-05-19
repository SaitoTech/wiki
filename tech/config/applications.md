---
title: Application Configuration
description: Information on configuration settings for Saito-lite-Rust applications
published: true
date: 2025-05-19T16:34:06.366Z
tags: 
editor: markdown
dateCreated: 2024-11-20T03:23:11.530Z
---

# Application Configuration for Saito-lite-Rust

This page describes how to customize the modules/applications running on a Saito node. This is useful if you want users who visit your server to have a default set of applications available and avoid their needing to download or install applications separately through their browser.

We assume you are running the [default saito client](/install). Once the server is running, you can customize the modules it supports by editing the `/config/modules.config.js` file.

## Module Directory

Copy any modules that you want to provide to users by default into your local ```/mods``` directory. Unless you've been moving files around, this will be located at the ```/saito/node/mods/``` sub-directory in your local repository -- you'll see that this directory already contains a number of modules by default.

You can find many more in our own [Saito modules repository](https://github.com/SaitoTech/saito/tree/master/node/mods). If you aren't sure what kind of applications are available, considering browsing through the [applications](/applications) section of this wiki. 

## Module Configuration

The `config/modules.config.js` file contains two sections ```core``` and ```lite```. The  whether an application in the `mods/` folder should run on the server, the browsers connected to it, or both. The file is structured like this (though the default will be more heavily populated with applications):

```js
module.exports = {
	core: [
		'arcade/arcade.js',
		'encrypt/encrypt.js',
		'explorer/explorer.js',
		'redsquare/redsquare.js',
	],
	lite: [
		'arcade/arcade.js',
		'encrypt/encrypt.js',
		'explorer/explorer.js',
		'redsquare/redsquare.js',
	],
};

```

### Applying Changes

Running `npm run nuke` will create fresh versions of these configuration files from template files that are stored in the `config` directory. It will also compiles a compressed version of Saito from the `modules.config.js` that will be fed out to browsers which connect to the server and request the default Javascript.

- You can also copy `modules.default.js` and rename it to `modules.config.js` if the latter file is missing for any reason.

Be warned that running `npm run nuke` will reset your client and reset your blockchain data.

If you wish to change the applications supported on your server without resetting the blockchain, you can run the following instruction instead:

`npm run compile`

This uses your updated configuration files and preserves vital data for nodes running production-level infrastructure.

<hr>