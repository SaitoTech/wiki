---
title: Tutorial 1 Deploy and Install Application
description: Deploying and Installing Application in Saito
published: true
date: 2024-09-23T09:18:33.117Z
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
```

All Saito modules extend from the ModTemplate class, which we required at the top of our module. This parent class provides the default set of functions that are called by the Saito Wallet whenever specific actions happen, such as when a new block is received or a transaction arrives that may require processing.

Start by customizing the name and description of your module. The slug should be a lowercase alphanumeric strings (no spaces, no punctuation). It is standard to derive the slug from the module name. This will also be the "address" of the application (i.e. users who have this module installed will be able to "visit" it at /tutorial01).

## Adding Functionality

All Saito modules ultimately inherit from this class. You can look into thi file to see a list of the functions that you can override in your module. If you override a function then your module will run that function whenever the action

In this case, we are going to override three specific functions. The first function ```initialize(app)``` runs whenever . 

```
  async initialize(app) { 
    super.initialize(app);
    console.log("Hello World - Initializing Tutorial01!"); 
  }
```

An important difference between Saito and other application platforms is that all modules are always . This . All applications are always primed. This is a . Even if you are chatting with someone, your wallet can still receive a game move.


The initialize function is called whenever the Saito Wallet boots-up.
In this case, we want to use or over-ride, but the first step to customizing your application is creating   You can change the name and description of the module to whatever you want. The slug of the application should map to the name of the directory that contains the module, and the name of the main application javascript file.




Congratulations! You’ve just published your application. Technically, you’ve just sent that transaction (containing your app) out into the network along with metadata requesting that the AppStores on the network index and host your application. 

Surprise! If your browser sent the transaction properly, you’ll have received an email confirming your submission. Open this email and you’ll find your unique APP-ID along with a link you can click on to install the application. Anyone can use that link or your APP-ID to find your application. If you ever need to search manually, go back to the AppStore, click to launch the Saito Appstore and search for your APP-ID manually (note: if your application is not found right away, wait a minute until it is finished indexing). You should see this:

Click to view your app details and then click INSTALL. Upgrading your browser takes about 45 seconds. Watch the countdown and wait for your installation to complete. You’ll be asked to confirm you want to upgrade your client before the process is over. Click “CONFIRM”.

![tutorial1appstore.png](/installconfirm.png)

Look at the sidebar and you’ll see the application you just installed. Click on it and click on the button. Looks like this application creates a simple HTML interface and sends a transaction (with data) onto the network s, and then take a look at the [annotated source code](https://github.com/SaitoTech/saito-lite/blob/master/mods/tutorial01/tutorial01.js) to see how easy it was to build.

In our [next tutorial](/tech/tutorial-2-chat) we’ll create an application that can receive transactions in addition to sending them. Before we get to that, there’s something important you may have realized: the Saito AppStore is an application like any other application. Although our tutorial series starts with small applications, there’s no limit to the complexity of the applications that you want to build.

