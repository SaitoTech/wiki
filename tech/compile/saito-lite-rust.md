---
title: Compile Saito-lite-Rust Apps
description: Instructions for compiling Saito applications
published: true
date: 2024-11-20T23:21:39.208Z
tags: 
editor: markdown
dateCreated: 2024-11-20T03:22:04.713Z
---

# Saito-lite-Rust Application Compilation

When building applications with the [Saito-Lite-Rust](https://wiki.saito.io/en/tech/javascript) software, Javascript must first be compiled before it can ran on a *core-client* or served to *lite-clients* (like browsers).  The *core-client* is a full node and more specifically, an [*application node*](https://github.com/SaitoTech/saito-lite-rust). The [Saito-lite-Rust]() core-client is responsible for compiling and serving compiled applications to lite-clients such as the [apps](/tech/applications) on [Saito.io](Saito.io).

## Compile List

Application won't be compiled until the compile configuration file at `config/modules.config.js` lists it in the *core* or *lite* sections. The `core` section lists the modules that will run on your full node server. The `lite` section lists the modules that your server will compile and serve by default for any lite-clients that connect to it (these apps can run without any central server once launched).

- See the dedicated page for complete information on [module configuration](/tech/config/applications).

### Quickstart Compile

Open the file `/saito-lite-rust/config/modules.config.js`.

Add `myApp/myApp.js` to `core`, `lite` or both.

```js
core [
     'myApp/myApp.js',
...
lite: [
    'myApp/myApp.js',
...
```
The JavaScript bundle can created with either of the following commands:

Navigate to `/saito-lite-rust`.

First-time compilation or a chain and databse reset (sometimes useful for debugging) can be achieved with:

```
npm run nuke
```

To preserve data and just recompile the new JavaScript:
```
npm run compile
``` 
Once compilation finishes, start Saito by running:
```
npm start
```

## Compilation

As touched on above, Saito-lite-Rust compilation takes two primary forms:

1. `npm run nuke` which clears out persistent data.
2. `npm run compile` command which preserves all data except previously compiled JS.

The compilation commands have their procedures explicitly defined in `scripts/install.js` - what follows is a summary.

### Nuke

Running `npm run nuke` will remove and reset the `/data` directory, which includes application databases, block and transaction data, bundler data and more. The full extent of the reset is defined in the following functions contained in `scripts/install.js`:
```js
reset_nonpersistent();
reset_persistent();
reset_bundler();
```



#### Configuration Files

The following JS code pertaining to the `config/` folder is executed on `npm run nuke`.
```js
	if (!fs.existsSync('../config/modules.config.js')) {
		copyDir('../config/modules.default.js', '../config/modules.config.js');
	}

	if (fs.existsSync('../config/options.conf')) {
		copyDir('../config/options.conf', '../config/options');
	}
```


 The [networking configuration](/tech/config/network) file `./config/options` is replaced with `./config/options.conf`, if the latter (`.conf` version) exists.

If a `./config/modules.config.js` file does not exist, the *nuke* command will create one from the given default: `./config/modules.default.js`.

<hr><hr>

Running ```npm run nuke``` will create fresh versions of these configuration files from template files that are stored in the ```config``` directory. It will also compiles a compressed version of Saito from the ```modules.config.js``` that will be fed out to browsers which connect to the server and request the default Javascript.

You can always reset your client by running the "nuke" command, but if you wish to change the applications supported on your server without resetting the blockchain, you can run the following instruction instead:

```npm run compile```
<br>
<!--
Saito uses two main configuration files. The first is ```config/options``` which specifies network configuration options like the IP address on which the server runs and the ports it should open and the peers to which it should connect. A second ```config/modules.config.js``` file specifies which modules should run on the server and any browsers that connect to it.
-->

### Advanced Usage of the `compile` Script

The `compile` script supports additional logging options, which can be specified using the `--loglevel` or `-l` flags. This feature allows you to set the desired log level for the compilation process.

#### Usage:

To set a specific log level, use one of the following commands:

```
npm run compile -- --loglevel=<level>
```

or 
```
npm run compile -- -l <level>
```

Where level can be one of the following:

- `error`
- `warn`
- `info`
- `trace`
- `debug`

For example, to set the log level to `warn`, you can use either:

```
npm run compile -- --loglevel=warn
```

```
npm run compile -- -l warn

```

#### Javascript Client 'dev' Flag

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
