---
title: Saito Tutorials
description: How to Build Applications on Saito
published: true
date: 2024-09-28T09:44:50.936Z
tags: 
editor: markdown
dateCreated: 2024-09-28T09:43:23.468Z
---

# Saito Application Tutorials

This tutorial series is designed to get you developing Saito applications quickly. Our first tutorial explains the basics of what an application is and how it works. We recommend all developers new to Saito start by at least reading it. The remaining tutorials cover specific topics – you can look for one that is close to the kind of application that you want to build and use it as a starting point.We  You can also see how existing modules work by checking out the modules directory in our main repository.

| Tutorial    | Title | Description |
|:----------- |:----- |:----------- |
| #1          | [Hello World](/tech/tutorials/01) | Build an application that installs into the User's wallet and alerts the user every time their wallet loads. This explains the structure of a Saito application, the basic information you should provide to users, and how to compile and distribute your applications. All of the other tutorials in this series assume that you understand the basics covered in this tutorial. |
| #2          | [Sending Transactions and UI Components](/tech/tutorials/02) | This tutorial modifies the application we built in our first tutorial. This time we use a UI Component to display a button on the page and attach a click-event. When the button is clicked, this event first and calls a function inside our module that creates a transaction and sends it out into the network. This tutorial teaches the basics of creating UI components and connecting them to functions in your core module. |
| #3          | [Receiving On-Chain Transactions](/tech/tutorials/03) | This tutorial continues our basic application. Now in addition to sending a transaction, the module will listen on the blockchain for the transactions that we have created and update our UI whenever we receive one with the information that was delivered. At this point, our tutorials have now covered how to create a simple interface and send transactions and process them on receipt... |
| #4          | [Chat Monitor](/tech/tutorials/04) | Build a chatbot that listens for chat messages received on-chain, off-chain and/or through server relays. Whenever a transaction is received, this module processes the transaction and decides how to respond based on some simple metrics. |
| #5          | Adding Menu Items | Build a module that inserts a link into several of the menus available for desktop and mobile users. If you're building an application and want to make it show up in the default menu list, this is the tutorial for you. |
| #6          | Modifying CSS | Want to experiment with CSS? This module shows how to programmatically update/change/delete CSS entries. We'll also cover some basic techniques for modifying webpages that already exist even if they are provided by other modules. |
| #7          | Keyword-Filtering | Build an application that adds keyword filtering rules to determine whether transaction should be permitted past content filters  |
| #8          | Advertising Module |  |
| #9          | Drag-and-Drop and DOM Manipulation | This tutorial covers some very useful techniques for creating an manipulating the HTML used by applications to build and show UI elements. The shortcuts in this tutorial have saved us significant time. |
| #10          | Tic-Tac-Toe | This tutorial covers the basics of how to build a simple, simple game that shows up on the Saito Arcade and can be used. If you are interested in building games, this will provide a useful introduction to how games works generally.  |

