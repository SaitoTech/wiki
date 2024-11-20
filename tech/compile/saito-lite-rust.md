---
title: Compile Saito-lite-Rust Apps
description: Instructions for compiling Saito applications
published: true
date: 2024-11-20T03:22:04.713Z
tags: 
editor: markdown
dateCreated: 2024-11-20T03:22:04.713Z
---

# Saito-lite-Rust Application Compilation

When building applications with the [Saito-Lite-Rust](https://wiki.saito.io/en/tech/javascript) software, Javascript must first be compiled before it can ran on a *core-client* or served to *lite-clients* (like browsers). 

The core-client is a full node and more specifically, an [*application node*](https://github.com/SaitoTech/saito-lite-rust). This software is responsible for compiling and serving compiled applications to lite-clients which can be seen in action when using the [apps](/tech/applications) on [Saito.io](Saito.io).

## Config File

Your application won't be compiled until the compile configuration lists it. Below are the most basic instructions to compile, see the dedicated page for more information on [module configuration](/tech/config/applications).

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