---
title: Developing Saito Applications
description: 
published: true
date: 2025-05-19T18:06:06.051Z
tags: 
editor: markdown
dateCreated: 2022-01-07T07:06:32.790Z
---

# Developing Saito Applications

Want to build Saito applications? The first thing to do is get a local version of Saito running and learn how to install applications -- if you do not know how to run a node the first step is to [install](/install) Saito locally so you have a development environment.

Once you have built an application, you can visit this page to learn how to [compile it](/applications/compile) into a standalone .saito file that users can drag-and-drop into their browsers and start using in seconds. Before we are ready for that we'll need to build an app though, which is the focus on this page...

## Tutorials 

We have a full **[tutorial series](/tech/tutorials)** that starts with the basics and works towards more advanced materials. If you would like to learn something that is not covered, drop by RedSquare and mention it:

| Tutorial    | Title | Description |
|:----------- |:----- |:----------- |
| #1          | [Hello World](/tech/tutorials/01) | A barebones application that alerts the user every time their wallet loads. Demonstrates basic structure and workflow. |
| #2          | [Sending Transactions and UI Components](/tech/tutorials/02) | Adds a UI Component and click-event which creates a transaction and sends it into the network. |

## <div id="compile"> Distributing Apps </div>

If you've developed a Saito Application and are wondering how to distribute it to users, there are currently two options:

1. [Compile](/tech/tutorials/01#installing-and-compiling) and host on an SLR node.

2. [Compile and share a DCM file](https://wiki.saito.io/tech/compile/applications) for drag-and-drop installation.

## Documentation and External Resources

Visit the [Saito Docs](https://wiki.saito.io/en/tech/docs) for technical information.

Check out our [reference modules](https://github.com/SaitoTech/saito-lite-rust/tree/master/mods) to see what Saito developed applications look like.

Visit the community resource [Livedocs](https://github.com/mat888/saito-livedocs), which serves as a working demonstration and hackable template for basic Saito applications.

<!--
## Misc.

The **Module API** explains what functions you can include in your module. The **Events API** explain how to listen and respond to system-wide events that are triggered when events happen like a new block being found. The **Services API*** explains how peers can inform other peers that they can be queried for special types of data. Finally, our **Ui Components** and **CSS Design** specifications explain our standard approach for creating UI components that will work and look good regardless of the applications that users are running.

### [Module API](https://wiki.saito.io/en/tech/docs/module-api)
* Saito Modules inherit from the ```/lib/templates/modtemplate.js``` file. This template file defines a number of default functions that create the basic behavior for the module. If you overwrite these functions you can customize the behavior of your module, such as specifying what actions it should take when it receives a transaction or off-chain message. This API outlines these basic functions.

### [Events API](https://wiki.saito.io/en/tech/docs/events-api)
* Saito includes an event system where components may activate when significant events occur, such as the discovery of a golden ticket or the receipt of a new block that builds on the longest-chain, or the update of your wallet balance. Modules can subscribe to the ```app.connection``` channel to be notified when these various events happen - this API explains how to do that and provides a short list of available events.

### [Services API](https://wiki.saito.io/en/tech/docs/services-api)
* Saito modules can announce their support for arbitrary "Services" when connecting to other peers. This lets peers know they are available to handle specific requests. Modules can announce their support for various services, and use this information to request data from peers running similar modules or service protocols. 

### [UI Components and Templates](https://wiki.saito.io/en/tech/docs/ui-components)
* Saito comes with an extensive set of UIComponents and Templates that can be used to create applications with headers, sidebars, user-boxes and games and invites and much more. This section explains how to use existing components in your applications.

### [CSS Design](/tech/docs/saito-css)
* Saito comes with a default set of CSS classes that creates the colorful aesthetic behind our core applications. While developers can always create their own CSS designs, you can extend the core classes in our Saito CSS design for a faster path to having your module look good everywhere. -->