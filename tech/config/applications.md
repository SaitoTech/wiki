---
title: Application Configuration
description: Information on configuration settings for Saito-lite-Rust applications
published: true
date: 2024-11-20T03:36:06.973Z
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

Running `npm run nuke` will create fresh versions of these configuration files from template files that are stored in the `config` directory. It will also compiles a compressed version of Saito from the `modules.config.js` that will be fed out to browsers which connect to the server and request the default Javascript.

- You can also copy `modules.default.js` and rename it to `modules.config.js` if the latter file is missing for any reason.

Be warned that running `npm run nuke` will reset your client and reset your blockchain data.

If you wish to change the applications supported on your server without resetting the blockchain, you can run the following instruction instead:

`npm run compile`

## Advanced Usage of the `compile` Script

The `compile` script supports additional logging options, which can be specified using the `--loglevel` or `-l` flags. This feature allows you to set the desired log level for the compilation process.

### Usage:

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


### Javascript Client 'dev' Flag

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
   being a concatenation of the source CSS). This makes CSS development
   slightly easier.
   
The result is that many more files are downloaded by the client, but in-browser debugging is much easier
