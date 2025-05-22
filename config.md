---
title: Configure Saito-lite-Rust
description: Directory for information on the various configuration files which dictate how a Saito-lite-Rust client operates.
published: true
date: 2025-05-22T09:20:45.654Z
tags: 
editor: markdown
dateCreated: 2024-11-20T04:13:39.150Z
---

# Saito Configuration

After [installing](/install) Saito you will be ready to configure the server. This involves editing the two main configuration files used by the node:

- `config/modules.config.js` specifies which modules run on the server (core) and which modules are compiled for any lite-clients that connect to the server (lite).

- `config/options.conf` is the main configuration file, specifying the IP address on which the server runs and the ports it should open and the peers to which it should connect.  When you run Saito for the first time, this file is copied over into ```config/options``` which will contain your configuration options along with wallet information like the public and privatekey of your server -- you can backup your wallet anytime by backing up this file.

Almost anything you want to configure for Saito can be accomplished by editing one of these two files.

## Configuring Network

```/config/options.conf``` is the template file used to configure your server. We have a dedicated page describing [how to configure this file](/config/network) to change your server settings. By default, this file will come pre-configured to start your Saito node on localhost at port 12101.


## Configuring Applications

You may remember the instruction we ran to compile Saito during our initial [install](/install):

```
npm run nuke
```

In addition to restoring Saito to a *factory-fresh* condition, this command compiles a compressed version of the Saito which will include any modules listed in `modules.config.js` as available for lite-clients. This compressed file will be served to any browsers which connect to the server and request a copy of the software.

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


