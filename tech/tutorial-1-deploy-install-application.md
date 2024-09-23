---
title: Tutorial 1 Deploy and Install Application
description: Deploying and Installing Application in Saito
published: true
date: 2024-09-23T10:35:48.274Z
tags: 
editor: markdown
dateCreated: 2022-03-22T07:07:49.922Z
---

# Tutorial 1 – Hello World

This tutorial builds a simple application that alerts the user when they start-up their wallet and connect to the network. Our goal is to cover the absolute basics of how to develop applications. We assume that you have already installed a local copy of Saito and can start the node.

NOTE: you can access all of the files in this tutorial by downloading this [ZIP file](/tutorial01_(2).zip). If you want to skip the tutorial and see how the compiled application works in practice, you can also download this application as a [standalone Saito module] and install it into your wallet.

![appstore_screenshot.png](/appstore_screenshot.png)

## Creating the Application Directory

Navigate into your ```/mods``` directory and create a folder with the name ```tutorial01```. Within that directory create the file ```tutorial01.js```. Copy the text below and put into this this file.

```
var ModTemplate = require('../../lib/templates/modtemplate');

class Tutorial01 extends ModTemplate {

  constructor(app) {

    super(app);

    this.name            = "Tutorial01";
    this.slug            = "tutorial01";
    this.description     = "Introductory tutorial for Saito App Development";

    return this;

  }

}

module.exports = Tutorial01;
```

All Saito modules extend from the ModTemplate class, which we required at the top of our module. This parent class provides the default set of functions that are called by the Saito Wallet whenever specific actions happen, such as when a new block is received or a transaction arrives that may require processing.

Start by customizing the name and description of your module. The slug should be a lowercase alphanumeric strings (no spaces, no punctuation). It is standard to derive the slug from the module name. This will also be the "address" of the application (i.e. users who have this module installed will be able to "visit" it at /tutorial01).

## Adding Functionality

All Saito modules ultimately inherit from the ```/lib/templates/modtemplate``` class. You can look into this file to see a list of the functions that you can override in your own module. If you override a function then your function will run whenever that function is called.

In this case, we are going to override three specific functions. The first function ```initialize(app)``` runs whenever your wallet is initialized. First we pass control to the parent class to let it initialize your module. And then we add anything specific we want our module to do. In this case, if I am a browser, let's trigger an alert to let the user know that we've initialized our module!

```
  async initialize(app) { 
    super.initialize(app);
    if (app.BROWSER) { alert("Hello World - Initializing Tutorial01!"); 
  }
```

An important difference between Saito and other application platforms is that all modules are always initialized whenever Saito starts, and all modules are always running all-the-time. This can be a bit counterintuitive to web2 developers, because your applications can be running even when you are not interacting with them. But this is what needs to happen, because your applications always need to be ready to receive messages/instructions on-chain or off-chain.

```
  async render() { 
    if (document.querySelector(body)) {
       document.querySelector(body).innerHTML = "Hello World";  
       alert("Hello World!");
    }
  }
```

The second function we are going to override is the ```render()``` function. This is run whenever the user. We normally use it to initialize the UI for applications when users want to interact with them by viewing the application in the browser.

Here is the fun part -- the rendering is not done on the server. Saito has noticed that you are trying to interact with an application located at ```/tutorial01``` and it sees the slug assocaited with your module and instructs it to render itself. Even though we can install this application on the server, it is the browser that is rendering the webpage.

Add these functions to the body of our tutorial file. We are now ready to install this module and compile it.

## Installing and Compiling Your Application

Open the file ```/config/modules.config.js```. This file contains two lists of modules. The first list is in the ```core``` section -- it lists the modules that will run on your server. The second is in the ```lite``` section -- it lists the modules that you will compile for any lite-clients that connect to your server.

You can build modules that are designed to work ONLY for servers or ONLY for browsers, but most modules are written so that they work on both servers and lite-clients. If you need to disable functionality, you can check the ```app.BROWSER``` variable to see if you are running in a browser or not.

Follow the convention in this configuation file and include your tutorial in both the CORE and LITE sections of this file. Then navigate to ```/saito-lite-rust``` and compile

```
> npm run nuke
```

If this is not your first time compiling the software you can run ```npm run compile``` instead. The difference between ```nuke``` and ```compile``` is that ```nuke``` will purge all of the information. This makes it useful for debugging. If you don't want to purge your whole server or wallet, use ```compile``` instead.

The Saito install script will let. If everything goes well you'll If there are any problems, it means you have a typo or javascript error. Fix the problem and run ```npm run nuke``` again until it works. At that point you can start Saito by running ```npm start``` and test your action in real life.


## Using our Application

If you haven't removed any application froms the default set of applications in your 
Congratulations! You’ve just published your application. Technically, you’ve just sent that transaction (containing your app) out into the network along with metadata requesting that the AppStores on the network index and host your application. 

Surprise! If your browser sent the transaction properly, you’ll have received an email confirming your submission. Open this email and you’ll find your unique APP-ID along with a link you can click on to install the application. Anyone can use that link or your APP-ID to find your application. If you ever need to search manually, go back to the AppStore, click to launch the Saito Appstore and search for your APP-ID manually (note: if your application is not found right away, wait a minute until it is finished indexing). You should see this:

Click to view your app details and then click INSTALL. Upgrading your browser takes about 45 seconds. Watch the countdown and wait for your installation to complete. You’ll be asked to confirm you want to upgrade your client before the process is over. Click “CONFIRM”.

![tutorial1appstore.png](/installconfirm.png)

Look at the sidebar and you’ll see the application you just installed. Click on it and click on the button. Looks like this application creates a simple HTML interface and sends a transaction (with data) onto the network s, and then take a look at the [annotated source code](https://github.com/SaitoTech/saito-lite/blob/master/mods/tutorial01/tutorial01.js) to see how easy it was to build.

In our [next tutorial](/tech/tutorial-2-chat) we’ll create an application that can receive transactions in addition to sending them. Before we get to that, there’s something important you may have realized: the Saito AppStore is an application like any other application. Although our tutorial series starts with small applications, there’s no limit to the complexity of the applications that you want to build.

