---
title: Configure Saito-lite-Rust
description: Directory for information on the various configuration files which dictate how a Saito-lite-Rust client operates.
published: true
date: 2025-05-19T17:04:43.402Z
tags: 
editor: markdown
dateCreated: 2024-11-20T04:13:39.150Z
---

# Saito Configuration

After [installing](/install) Saito you will be ready to configure the server to run the applications you wish to support. You can also configure it to run on a specific domain or IP address and use a specific publickey and much more. This section introduces the configuration steps.

## Configuration Files

Saito uses two main configuration files. 

- `config/options`
- `config/modules.config.js`

`config/options` contains network configuration options like the IP address on which the server runs and the ports it should open and the peers to which it should connect. This file will *also* contain the public and privatekey of your server -- you can backup your server wallet anytime by backing up this file.

`config/modules.config.js` specifies which modules will run on the server (core) and which modules will be served to any browsers that connect to it (lite).

## Compilation

Compiling produces a compressed version of Saito which will include the modules listed in `modules.config.js` - this compiled Javascript is then served to browsers which connect to the server and request the default modules.

There are two primary compilation commands. 

- `npm run nuke`
- `npm run compile`

The first time you run Saito you should run the more extreme `npm run nuke` command as it will reset the blockchain and offers a *hard reset* of sorts. It also *nukes* your wallet and restores it to a pristine state using the template config files stored in your `config` directory.

Use `npm run compile` if you wish to change or update the applications supported and distributed on your server without resetting the blockchain or affecting the server wallet - better for [deployed](https://wiki.saito.io/en/tech/deployment) nodes connected to mainnet.

### Advanced Usage of the `compile` Script

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
   being a concatentation of the source CSS). This makes CSS development
   slightly easier.
   
The result is that many more files are downloaded by the client, but in-browser debugging is much easier. For further information on application and network configuration, see the following two pageS:

- [applications configuration](/config/applications)

- [Network configuration](/config/network)


