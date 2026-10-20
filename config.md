---
title: Configure Saito-lite-Rust
description: Directory for information on the various configuration files which dictate how a Saito-lite-Rust client operates.
published: true
date: 2026-10-20T08:38:51.699Z
tags: 
editor: markdown
dateCreated: 2024-11-20T04:13:39.150Z
---

# Configure Saito

The easiest way to configure Saito is using the Admin module, which runs on all servers at ```/admin```. The first thing you will need to do is backup the wallet your browser has created to administer the server: 

![admin_set_access_key.png](/img/admin_set_access_key.png)

When you click this button the wallet will download a backup of the wallet that your browser has created to admin the server. We recommend keeping a copy of this file in case you need to restore this account in a different browser in the future.

To change the set of modules installed on your server, visit the Modules section of the admin application:

![admin_configure_modules.png](/img/admin_configure_modules.png)

Click on any application to toggle between running it on only on your server, providing it only to browsers, or running it on your server and providing it to browsers as well (recommended).

Follow the instructions on the page after making any changes.

## Manual Configuration

To configure Saito manually, the two most important files you will need to customize are the following:

- `config/modules.config.js` specifies which modules run on the server (core) and which modules run on lite-clients (lite). After making changes here run ```npm run nuke``` to re-compile the version of Saito intended for lite-clients..

- `config/options.conf` holds your wallet keypair. When you run Saito for the first time, this file is copied over into ```config/options``` and a new keypair is generated for your server -- you can backup your wallet anytime by securing this file.

- `config/options.conf` also holds your network settings. We have a dedicated page describing [how to configure this file](/config/network) to change your server settings. By default, Saito is pre-configured to start your Saito node on localhost at port 12101.


## Restoring to Factory Defaults

Run the following command anytime to restore Saito to a clean default factory-fresh state and recompile the javascript offered to users based on any changes to your modules config file.

```
npm run nuke
```

If you wish to recompile without nuking your wallet:

- `npm run compile`


## Advanced Options for Developers


Both the `compile` and `nuke` scripts can be run with a `dev` flag:

* ```npm run compile dev```
* ```npm run nuke dev```

When this flag is used:

 * JavaScript is not minimized and source maps are shipped with the code 
   The payload is 2 to 3 times larger than otherwise but makes in-browser 
   debugging possible.
   
 * CSS files are linked (```@include()``` CSS source files, rather than 
   being a concatentation of the source CSS). This makes CSS development
   slightly easier.
   
The result is that many more files are downloaded by the client, but in-browser debugging is easier. For further help with application or network configuration, see:

- [applications configuration](/config/applications)

- [Network configuration](/config/network)






