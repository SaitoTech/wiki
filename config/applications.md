---
title: Application Configuration
description: Information on configuration settings for Saito-lite-Rust applications
published: true
date: 2025-05-20T15:43:37.820Z
tags: 
editor: markdown
dateCreated: 2024-11-20T03:23:11.530Z
---

# Configuring the Modules on Your Node

This page describes how to customize the modules/applications running on a Saito node. This is useful if you want users who visit your server to have a default set of applications available and avoid their needing to download or install applications separately through their browser.

We assume you are running the [default saito client](/install). Once the server is running, you can customize the modules it supports by editing the `/config/modules.config.js` file. NOTE: if this file is missing for any reason, you can rename `modules.default.js` to `modules.config.js` and use this file instead.

## Module Directory

Copy any modules that you want to provide to users by default into your local ```/mods``` directory. Unless you've been moving files around, this will be located at ```/saito/node/mods/```. If you aren't sure what kind of applications are available, considering browsing the [applications](/applications) section of this wiki.

If you are developing a Saito application you can put it directly into this directory. Once you have installed the applications you want you will need to tell your Saito installation to use the subset that you wish to make publicly available.

## Module Configuration

The `config/modules.config.js` file contains two sections ```core``` and ```lite```. The modules listed in ```core``` will run on your server. The modules listed in ```lite``` will be provided to any users who ask your server for a compiled copy of the blockchain. The file is structured like this (though the default will be more heavily populated with applications):

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

Add the modules that you wish. If you are developing a module, it is a great idea to add it to the list, as any compilation errors will be flagged when you attempt to compile the node, allowing you to iterate rapidly finding and fixing bugs in your application.

### Applying Changes

When you installed Saito for the first time you will have run the command `npm run nuke`. One of the things that this command does is initialize any modules you have installed on your server into a "new" state, and compile the modules in your ```lite``` list into a javascript file that will be provided to the users who connect to your server.

As a result, whenever you wish to update your list of supported applications, you should re-run this command. This will re-compile all of the applications and reset your server. Be warned that running `npm run nuke` will reset your client and clear any blockchain data.

If you wish to re-compile the applications supported by your server without resetting your local copy of the blockchain or deleting any existing application data, you can run the following instruction instead:

`npm run compile`

This updates the set of applications available to your server and any connecting clients, but preserves existing data and is intended for nodes running production-level infrastructure.

<hr>