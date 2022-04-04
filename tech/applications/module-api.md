---
title: Saito Modules Protocol
description: API for Building Saito Modules
published: true
date: 2022-03-25T04:39:32.500Z
tags: 
editor: markdown
dateCreated: 2022-01-08T04:45:17.837Z
---

# Saito Module Protocol


## Abstract

The following standard describes the expected functionality available to javascript applications installed into the javascript Saito client. This standard provides basic functionality that allow modules to interact with the blockchain, process messages received over the blockchain, as well as handle common user-interface needs.


| Field   | Value             |
| ------- | ----------------- |
| Author  | David Lancashire  |
| Status  | Published         |
| Type    | Protocol Standard |
| Created | January 8, 2021   |

## Module Filename Conventions

Applications exist in standalone directories in the `/mods` directory. The name of the directory should be the lowercase, alphanumeric version of the application name without hyphens or spaces. The `Arcade` module should be installed at `/mods/arcade`. The `AppStore` module should be installed at `/mods/appstore`. 

Within their directory, all applications share the same basic directory structure:

```
appname.js
lib/
sql/
web/
README.md.
```

The only necessary file is the `appname.js` file, which should share its name with the parent directory. The main class for the `Encrypt` module is thus `/mods/encrypt/encrypt.js`. If additional files are needed they should be included in the `/src` or `lib` or `docs` directories.

__lib/__
Optional directory to place additional javascript files.

__doc/__
Optional directory for documentation and license information.

__sql/__
Optional directory for database definition files (sqlite3 format). Saito clients with database support will automatically create a sqlite3 database (`/data/appname.sq3`) on installation if there are table definition files in this directory.

__web/__
Optional directory for JS / HTML / CSS files. Saito clients with HTTP support will serve these files from the subdirectory of the application name (i.e. `https://appserver.com/appname`) with `index.html` as the default file to serve.

__src/__
Optional directory for pre-compiled files. Some modules like `Red Imperium` are "compiled" into a single javascript file prior to release. Including the source files in this `/src` directory will prevent errors bundling the entire Saito codebase into a single javascript file or code-duplication when compiling.

## Local Module Installation / Compilation

In the `/config` directory you'll find a file named `modules.config.js`. This file is created from a default file we make available, but is not overwritten if it already exists. To customize which modules are installed you will need to edit this file.

The `/config/modules.config.js` file contains two lists of modules: `core` and `lite`. Any modules included in the `core` list will run on the server when you start it. Any modules included in the `lite` list will be compiled into the bundled javascript file that is made available to browsers by default.

Once your module is in the config file you should run *./compile nuke* which will compile the file `saito.js` and copy it into the web directory at `/web/saito/saito.js`. The core code will serve this file at localhost:12101/saito/saito.js. If your application starts from a standalone webpage, this file should be included in the index.html file in the `/web` directory in your module.

The server can then be started by running `npm run dev`.

## Publishing Modules to the Network

Publishing an application involves compressing it into a .zip file and publishing that zip file the network by attaching it to a special transactions. AppStores listening on the network monitor the blockchain for these types of transactions and when they see new applications elect to index them applications (or update existing applications) as they are published.

The easiest way to publish an application is to go into the application directory and compress the contents of that directory into a .zip file (`zip -r appname.zip .`). The AppStore module is bundled with most Saito Wallets. It creates a panel in the Dev application that will automatically create a Saito transaction with this format:

```javascript
  tx.msg = {
    module: "AppStore",
    request: "submit module",
    module_zip: appname.zip,
    name: appname
  };
```

AppStores will index your application, identifying it with a unique ID created by hashing the timestamp and signature of the transaction you created containing the application payload. Users download the application by fetching the full transaction, and can verify the application is signed and the code has not been altered before installing it locally. Some AppStores offer remote app-compilation as a service.


## Building the Application (Saito API)

All modules should extend from a class in the `/lib/templates` directory. The most basic module should inherit from the `/lib/saito/templates/modtemplate` file. The most basic requirement for a valid module is a constructor and name as follows:

```javascript
const ModTemplate = require('../../lib/templates/modtemplate');

class ModuleName extends ModTemplate {

  constructor(app) {
    super(app);
    this.name          = "ModuleName";
  }

}

module.exports = ModuleName;
```

### Optional Class Variables

The following variables may also be defined within the constructor:

| Variable Name | Variable Type | Description |
|---------------|---------------|-------------|
| name          | String        | the name of the application |
| description   | String        | a brief description of the application |
| categories    | String        | application categories |
| slug          | String        | custom slug (alphanumeric, lowercase) |
| events        | Array         | list of events to which this module listens |



### Application Functions

```javascript
installModule(app) {}
```

__app__ - reference to the Saito application object.

(OPTIONAL) This function will be run the first time Saito initializes after the module is loaded. If you override this function and still wish your application to handle default on-install functionality, call the super.installModule(app) function within your own.


```javascript
  initialize(app) {}
```

__app__ - reference to the Saito application object.

(OPTIONAL) This function is run every time the module is initialized. Note that all modules are initialized every time that Saito loads, not just the module with which the user is interacting. So this function is executed every time Saito initializes.


```javascript
  initializeHTML(app) {}
```

__app__ - reference to the Saito application object.

(OPTIONAL) This function is run whenever the HTML/DOM is initialized in an application the user is seeking to interact with. It is the recommended place to manipulate the DOM and add new components.


```javascript
  attachEvents(app) {}
```



__app__ - reference to the Saito application object.

(OPTIONAL) This function is run after `initializeHTML(app)` is executed in an application that the user has loaded to interact with through a web interface. It is traditionally used to attach events to DOM objects every time the module is initialized.


```javascript
  async onConfirmation(blk, tx, conf, app) {}
```

__blk__ - the block which has just been added to the chain
__tx__ - the transaction being processed
__conf__ - the number of confirmations this transaction is receiving
__app__ - reference to the Saito application object

(OPTIONAL) This function is executed whenever a transaction receives an additional confirmation (conf). The first time it is executed conf will be provided as 0 rather than 1. The transaction is provided along with the block which contained the transaction. The block may or may not have the other transaction-level information stored depending on its depth in the chain.

```javascript
  onNewBlock(blk, lc) {}
```

__blk__ - the block which has just been added to the chain
__lc__ - is this block part of the longest chain (0 or 1)

(OPTIONAL) This function is executed whenever a new block is added to the chain. Modules can overwrite this function to take action when blocks are received. It differs from onConfirmation in that it will be triggered by any blocks, not just those that add to the longest-chain.

```javascript
  onChainReorganization(bid, bsh, lc, pos) {}
```

__bid__ - the id / height of the block being reorganized
__bsh__ - the hash of the block being reorganized
__lc__ - 1 if block moved onto the longest chain, 0 if removed
__pos__ - the position of the block in the blockchain.index

(OPTIONAL) This function is executed whenever there is a chain reorganization. This means it is also executed when a new block is added to the chain. The most common use-case is putting code here that executes when a transaction is received.


```javascript
  shouldAffixCallbackToModule(modname, tx=null) {}
```

__modname__ - the name of the module, as identified by its name variable
__tx__ - the transaction containing the module

RETURNS boolean (1 or 0)

(OPTIONAL) This function is executed to see if a module wishes to process a specific transaction. It is handed the modname (name of the module specified in the txmsg.module field) along with the full transaction in case it wishes to apply more complicated criteria. By default this will pass through transactions that are addressed to the module.


```javascript
  webServer(app, expressapp, express) {
```
__app__ - the Saito application object
__expressapp__ - the Express Webserver object
__express__ - the Express Web Server

(OPTIONAL) The default version of this function examines the module directory to see if it contains a `/web` folder and -- if so -- hooks up the routing on the main server so that this directory is hosted at that address, i.e. `https://saito.io/arcade`. You may override this function to provide more advanced routing logic.


```javascript
  respondTo(type) {}
```

RETURNS Object or null

__type__ - the request-type to which our application may choose to respond

(OPTIONAL) Modules can interact by querying other modules to see if they "respondTo" specific opportunities. An example is the Saito Arcade which queries installed games which `respondTo('arcade-games')` with an object. The object returns and its protocol is defined on a module-by-module basis. Modules which implement this are responding to opportunities for interactivity created by other modules.

```javascript
  receiveEvent(evtname, data) {}
```

RETURNS Object or null

__evtname__ - the name of the event to which we respond
__data__ - the data object emitted by the event originator

(OPTIONAL) Modules can listen to events by including the names of those events in the events Array in their constructor. Implement this function to catch those events as they are triggered. You may skip this and have your module hook manually onto the `app.connector` object.




