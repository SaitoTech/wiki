---
title: Saito Applications
description: 
published: true
date: 2024-10-29T21:10:00.519Z
tags: 
editor: markdown
dateCreated: 2022-01-07T07:06:32.790Z
---

# Building Saito Applications

In order to build and test Saito blockchain applications you first need to [install](/tech/installation/javascript) a Saito Lite Rust (SLR) node.

Then visit our [full tutorial series](/tech/tutorials) for new developers or jump in with the beginner lessons below:

## Tutorials for Beginners

| Tutorial    | Title | Description |
|:----------- |:----- |:----------- |
| #1          | [Hello World](/tech/tutorials/01) | Build an application that installs into the User's wallet and alerts the user every time their wallet loads. This explains the structure of a Saito application, the basic information you should provide to users, and how to compile and distribute your applications. All of the other tutorials in this series assume that you understand the basics covered in this tutorial. |
| #2          | [Sending Transactions and UI Components](/tech/tutorials/02) | This tutorial modifies the application we built in our first tutorial. This time we use a UI Component to display a button on the page and attach a click-event. When the button is clicked, this event first and calls a function inside our module that creates a transaction and sends it out into the network. This tutorial teaches the basics of creating UI components and connecting them to functions in your core module. |

| ... | [More tutorials](/tech/tutorials) | See the complete [tutorial series](/tech/tutorials) for more advanced lessons.

## Compiling and Distributing

Once your application is built you can package it so that any wallet can install it by using our instructions on [compiling applications for drag-and-drop install](/tech/compile).


## API Documentation

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

## External Resources

If you are an advanced developer our directory of [reference modules](https://github.com/SaitoTech/saito-lite-rust/tree/master/mods) may be of use for those who want to build "standard" applications in the same style and approach as our default application suite. You can also check out the community resource [Livedocs](https://github.com/mat888/saito-livedocs), which serves as a working demonstration and hackable template for basic Saito applications.