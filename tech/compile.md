---
title: Compiling Standalone Applications
description: This page convers how to turn your module into an installable Saito Application
published: true
date: 2024-11-09T02:44:26.539Z
tags: 
editor: markdown
dateCreated: 2024-09-27T09:25:06.675Z
---

# Compiling & Configuration

This page demonstrates the various methods of compiling and distributing Saito applications, including compiling and serving directly from an *Application (serving) Full Node*, or dynamically compiled [standalone bundles](#distribution) which users can drag-and-drop install onto their clients.

[Advanced configuration](#aconf) options are described at the bottom of the page.

Even if you plan to use dynamically compiled [standalone bundles](#distribution), it is useful to follow the *Application Node Compile* steps below and run apps locally to quickly test and debug them.

## Application Node Compile

When building applications with the [Saito-Lite-Rust](https://wiki.saito.io/en/tech/javascript) software, Javascript must first be compiled before it can ran on a *core-client* or served to *lite-clients* (like browsers). 

The core-client is a full node and more specifically, an [*application node*](https://github.com/SaitoTech/saito-lite-rust). This software is responsible for compiling and serving compiled applications to lite-clients which can be seen in action when using the [apps](/tech/applications) on [Saito.io](Saito.io).

### Config File

Your application won't be compiled until the compile configuration lists it.

Open the file `/saito-lite-rust/config/modules.config.js`.

<!-- This file contains two lists of modules. The first list is in the `core` section -- it lists the modules that will run on your full node server. The second is in the `lite` section -- it lists the modules that your server will compile for any lite-clients that connect to it and ask for the default set of applications. -->

Add `myApp/myApp.js` to `core`, `lite` or both.

```js
core [
     'myApp/myApp.js',
...
lite: [
    'myApp/myApp.js',
...
```

Then navigate to `/saito-lite-rust` and compile the Javascript bundle:

```bash
> npm run nuke
```

If this is not your first time compiling the software you can run `npm run compile` instead. Once compilation finishes, start Saito by running:

```bash
> npm start
```
<br>

## <div id="distribution">Dynamic Module Compilation for Severless Distribution</div>

*Dynamic Module Compilation* can be used to compile modules into standalone bundles users can drag-and-drop to [install](#install) into their browser. This precludes the need for developers to run infrastructure which serves the application bundles.

The following section shows how to compile applications into this format.

### AppStore - Compilation

Make sure your local Saito node is compiled with both CORE and LITE support of the ```devtools``` module, and then start your server and visit ```/devtools``` in your browser. You will see a drag-and-drop target.

<br />
<img src="/compile-01.png" style="width:600px" />

Provide ZIP file of your module directory and a popup will appear confirming the details of the application. If there is an issue reading the .zip file you likely have a problem with the application -- make sure it compiles and runs locally before you attempt to compile for remote installation. Otherwise click the button to generate the application.

Once you click the button, it may take a short while, but your machine will compile your module into a standalone file and download it to your machine. Find that file - this is the application-file that browsers will be able to install. <!-- Be sure it has a `.saito` file extension. -->

### <div id="install">AppStore - Installation</div>

To install these standalone application packages, click on the top-right menu in any Saito application and click on the Account button below your wallet balance. On the overlay that appears, look for the "+" button that shows up on the top-right of your installed modules. 

<br />
<img src="/compile-03.png" style="width:600px" />

Click on the add button and you'll get another drag-and-drop target. Drag the application package that you previously compiled into this window.

<br />
<img src="/compile-04.png" style="width:600px" />

A popup will appear to confirm installation. Confirm that you want to install this application and click "Install" if so. 

<br />
<img src="/compile-05.png" style="width:600px" />

Your browser will unpack the application, save it in your wallet and refresh. Once your browser reloads it will load the application you have just installed along with all other modules. You can now toggle it on-or-off like any other module.


## <div id="aconf">Advanced Configuration</div>

<!--
Once you have installed Saito-Lite-Rust you will be ready to configure the server to run the applications you wish to support and provide them to browsers on-demand. This section covers these follow-on configuration steps. -->

Saito uses two main configuration files. The first is ```config/options``` which specifies network configuration options like the IP address on which the server runs and the ports it should open and the peers to which it should connect. A second ```config/modules.config.js``` file specifies which modules should run on the server and any browsers that connect to it.

Running ```npm run nuke``` will create fresh versions of these configuration files from template files that are stored in the ```config``` directory. It will also compiles a compressed version of Saito from the ```modules.config.js``` that will be fed out to browsers which connect to the server and request the default Javascript.

You can always reset your client by running the "nuke" command, but if you wish to change the applications supported on your server without resetting the blockchain, you can run the following instruction instead:

```npm run compile```


### Advanced Usage of the `compile` Script

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
   being a concatenation of the source CSS). This makes CSS development
   slightly easier.
   
The result is that many more files are downloaded by the client, but in-browser debugging is much easier
