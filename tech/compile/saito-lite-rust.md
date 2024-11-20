---
title: Compile Saito-lite-Rust Apps
description: Instructions for compiling Saito applications
published: true
date: 2024-11-20T03:43:07.986Z
tags: 
editor: markdown
dateCreated: 2024-11-20T03:22:04.713Z
---

# Saito-lite-Rust Application Compilation

When building applications with the [Saito-Lite-Rust](https://wiki.saito.io/en/tech/javascript) software, Javascript must first be compiled before it can ran on a *core-client* or served to *lite-clients* (like browsers). 

The core-client is a full node and more specifically, an [*application node*](https://github.com/SaitoTech/saito-lite-rust). This software is responsible for compiling and serving compiled applications to lite-clients which can be seen in action when using the [apps](/tech/applications) on [Saito.io](Saito.io).

## Config File

Your application won't be compiled until the compile configuration file at `config/modules.config.js` lists it in the *core* or *lite* sections.

The `core` section lists the modules that will run on your full node server. The `lite` section lists the modules that your server will compile and serve by default for any lite-clients that connect to it.

Below are the most basic instructions to compile, see the dedicated page for complete information on [module configuration](/tech/config/applications).

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

Then navigate to `/saito-lite-rust` and compile the Javascript bundle:

```
npm run nuke
```

If this is not your first time compiling the software you can run `npm run compile` instead. Once compilation finishes, start Saito by running:

```
npm start
```

## Advanced Usage of the `compile` Script

The `compile` script supports additional logging options, which can be specified using the `--loglevel` or `-l` flags. This feature allows you to set the desired log level for the compilation process.

### Usage:

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
