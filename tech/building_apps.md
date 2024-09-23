---
title: Saito Applications
description: 
published: true
date: 2024-09-23T06:54:29.515Z
tags: 
editor: markdown
dateCreated: 2022-01-07T07:06:32.790Z
---

# Building Saito Applications

This section is for developers who want to build applications to run inside user browsers or on servers. An application can be as simple as a module that listens and responds to a certain type of transaction, or as complicated as any of the standalone apps with their own UIs that already run on Saito such as [RedSquare](/en/applications/redsquare) or any of the games available on the [Saito Arcade](/en/applications/arcade).

The first step in building Saito applications is to install a local copy of Saito. You will need to have a local version of Saito installed in order to test that your modules can compile properly. If you have not already installed Saito you can find [installation instructions](/en/tech/installation) here on getting Saito running locally. Once you have Saito installed you'll be able to confirm your modules are working properly and prepare compile binaries that other users can install direectly into their wallet.


## Tutorials

A good place to start is our [tutorial series](/tech/tutorials) for new developers. These tutorials start by teaching the absolute basics: how to build modules that send and receive transactions, and display UI elements and overlays that let the user. The more advanced tutorials explain how to get your module to insert itself into the existing UI elements like the standard drop-down menu.

More advanced developers can check our directory of [reference modules](https://github.com/SaitoTech/saito-lite-rust/tree/master/mods) which show exactly how the existing applications work. You can often consult an existing module to see how it works or modify an existing application to customize it and get it to do what you want.

You can also check out the community resource [Livedocs](https://github.com/mat888/saito-livedocs), which serves as a working demonstration and hackable template for basic Saito applications.


## API Documentation

If you are an advanced developer already familiar with how to build applications, we have the follow reference pages available that may be of use for those who want to build "standard" applications in the same style and approach as the default modules that we have hosted on our main site. 

The **Module API** explains what functions you can include in your module. The **Events API** explain how to listen and respond to system-wide events that are triggered when events happen like a new block being found. The **Services API*** explains how peers can inform other peers that they can be queried for special types of data. Finally, our **Ui Components** and **CSS Design** specifications explain our standard approach for creating UI components that will work and look good regardless of the applications that users are running.

### [Module API](/tech/applications/module-api)
* Saito Modules inherit from the ```/lib/templates/modtemplate.js``` file. This template file defines a number of default functions that create the basic behavior for the module. If you overwrite these functions you can customize the behavior of your module, such as specifying what actions it should take when it receives a transaction or off-chain message. This API outlines these basic functions.

### [Events API](/tech/applications/events-api)
* Saito includes an event system where components may activate when significant events occur, such as the discovery of a golden ticket or the receipt of a new block that builds on the longest-chain, or the update of your wallet balance. Modules can subscribe to the ```app.connection``` channel to be notified when these various events happen - this API explains how to do that and provides a short list of available events.

### [Services API](/tech/applications/services-api)
* Saito modules can announce their support for arbitrary "Services" when connecting to other peers. This lets peers know they are available to handle specific requests. Modules can announce their support for various services, and use this information to request data from peers running similar modules or service protocols. 

### [UI Components and Templates](/tech/applications/ui-components)
* Saito comes with an extensive set of UIComponents and Templates that can be used to create applications with headers, sidebars, user-boxes and games and invites and much more. This section explains how to use existing components in your applications.

### [CSS Design](/tech/applications/saito-css)
* Saito comes with a default set of CSS classes that creates the colorful aesthetic behind our core applications. While developers can always create their own CSS designs, you can extend the core classes in our Saito CSS design for a faster path to having your module look good everywhere.


