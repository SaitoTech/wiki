---
title: Saito Modules Protocol
description: API for Building Saito Modules
published: true
date: 2024-09-28T16:52:38.582Z
tags: 
editor: markdown
dateCreated: 2022-01-08T04:45:17.837Z
---

# Saito Module Protocol

The following document describes the basic structure of a Saito module and the core functions that most modules will extend. We recommend that total beginners work through our [first tutorial](/tech/tutorials/01) before reading this page.


## Directory Structure

Applications exist in standalone directories in the `/mods` directory. The name of the directory should be the lowercase, alphanumeric version of the application name without hyphens or spaces. The `Arcade` module can be found at `/mods/arcade` and the `RedSquare` module is in `/mods/appstore`.  Within each directory, applications share the same basic structure:

```
appname.js
lib/
sql/
web/
README.md.
```

The only necessary file is the `appname.js` file, which shares its name with the parent directory. The main class for the `Encrypt` module is thus `/mods/encrypt/encrypt.js`. If additional javascript files they should be included in the `/src` or `/lib` or `/docs` directories.

| directory | purpose |
| --------- | ------- |
| __/lib__  | directory for additional javascript files |
| __/doc__  | directory for docs and license info |
| __/sql__  | directory for sqlite3 database definition files (sqlite3 format). Saito clients with database support will automatically create a sqlite3 database (`/data/appname.sq3`) on installation if there are table definition files in this directory |
| __/web__  | directory for JS / HTML / CSS files. Saito clients with HTTP support will serve these files from the subdirectory of the application name (i.e. `https://appserver.com/appname`) with `index.html` as the default file to serve.
| __/src__ | some modules like `Red Imperium` are "compiled" into a single javascript file from multiple source files, using a compile script that is often also located in the main directory. The `/src` directory provides a place to put these files. |


## Main Application

Your main application file should extend from a class in the `/lib/templates` directory such as the `/lib/saito/templates/modtemplate` file. This ensures that the module supports all of the functions that are needed for operation, making the simplest document that is a valid module what follows:

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

The following variables may also be defined within the constructor.

| Variable  |  Type | Description |
|:--------------|:--------------|:------------|
| name          | String        | the name of the application |
| description   | String        | a brief description of the application |
| categories    | Array         | application categories |
| slug          | String        | custom application slug (alphanumeric, lowercase) |
| events        | Array         | list of events to which this module listens |



### Application Functions

The most common functions for modules to override are as follows:


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
  render(app) {}
```

__app__ - reference to the Saito application object.

(OPTIONAL) This function is run whenever the HTML/DOM is initialized in an application the user is seeking to interact with. This will be the case if the application slug matches the application the user has specified in their browser location bar.


```javascript
  async onConfirmation(blk, tx, conf, app) {}
```

__blk__ - the block which has just been added to the chain
__tx__ - the transaction being processed
__conf__ - the number of confirmations this transaction is receiving
__app__ - reference to the Saito application object

(OPTIONAL) This function is executed whenever a transaction receives an additional confirmation (conf). The first time it is executed conf will be provided as 0 rather than 1. The transaction is provided along with the block which contained the transaction. The block may or may not have the other transaction-level information stored depending on its depth in the chain.


```javascript
  async handlePeerTransaction(app, tx=null, peer, mycallback=null) {}
```

__app__ - reference to the Saito application object
__tx__ - the transaction being processed
__peer__ - the peer that has send us this transaction
__mycallback__ - a callback function to execute after processing

(OPTIONAL) This function is executed whenever a transaction is received from a peer over the peer-to-peer network (i.e. not an on-chain transaction). Modules that support both *handlePeerTransaction()* and *onConfirmation()* support both on-chain and off-chain messaging.


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






