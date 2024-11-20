---
title: Application Configuration
description: Information on configuration settings for Saito-lite-Rust applications
published: true
date: 2024-11-20T03:59:10.585Z
tags: 
editor: markdown
dateCreated: 2024-11-20T03:23:11.530Z
---

# Application (Saito-lite-Rust) Configuration

This page is dedicated to configuring how Saito applications are compiled, served and run on a [Saito-lite-Rust]() Node. It focuses on modifications which can be made to the `/config/modules.config.js` file.

## Module Configuration (modules.config.js)

<!--
Once you have installed Saito-Lite-Rust you will be ready to configure the server to run the applications you wish to support and provide them to browsers on-demand. This section covers these follow-on configuration steps. -->

<!--
Saito uses two main configuration files. The first is ```config/options``` which specifies network configuration options like the IP address on which the server runs and the ports it should open and the peers to which it should connect.-->

The `config/modules.config.js` file specifies whether an application in the `mods/` folder should run on the server, the browsers connected to it, or both. The file is structured like this (though the default will be more heavily populated with applications):

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