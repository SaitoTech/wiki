---
title: Saito Applications
description: 
published: true
date: 2023-01-23T00:38:26.646Z
tags: 
editor: markdown
dateCreated: 2022-01-07T07:06:32.790Z
---

# Saito Applications

Saito application are modules that get installed into the wallet. Applications use on-chain and off-chain messages to communicate and can plug into other applications.

If you are getting started programming on Saito, a good place to start is our [tutorial series](/tech/tutorials) for new developers. Our Github repository also has a directory full of [reference modules](https://github.com/SaitoTech/saito-lite-rust/tree/master/mods) you can modify or consult if you are curious how the existing applications work.

The following documentation may be useful for those doing more advanced development. The **Module API** explains what functions you can include in your module. The **Events API** explain how to listen and respond when system-wide events occur (like a new block being found). The **Services API*** explains how peers can inform other peers of value-added services they are running.

### [UI Components and Templates](/tech/applications/ui-components)
* Saito comes with an extensive set of UIComponents and Templates that can be used to create applications with headers, sidebars, user-boxes and games and invites and much more. This section explains how to use existing components in your applications.

### [CSS Design](/tech/applications/saito-css)
* Saito comes with a default set of CSS classes that creates the colorful aesthetic behind our core applications. While developers can always create their own CSS designs, you can extend the core classes in our Saito CSS design for a faster path to having your module look good everywhere.


### [Module API](/tech/applications/module-api)
* Saito Modules inherit from the ```/lib/templates/modtemplate.js``` file. This template file defines a number of default functions that create the basic behavior for the module. If you overwrite these functions you can customize the behavior of your module, such as specifying what actions it should take when it receives a transaction or off-chain message. This API outlines these basic functions.

### [Events API](/tech/applications/events-api)
* Saito includes an event system where components may activate when significant events occur, such as the discovery of a golden ticket or the receipt of a new block that builds on the longest-chain, or the update of your wallet balance. Modules can subscribe to the ```app.connection``` channel to be notified when these various events happen - this API explains how to do that and provides a short list of available events.

### [Services API](/tech/applications/services-api)
* Saito modules can announce their support for arbitrary "Services" when connecting to other peers. This lets peers know they are available to handle specific requests. Modules can announce their support for various services, and use this information to request data from peers running similar modules or service protocols. 
