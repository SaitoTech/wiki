---
title: Compiling Standalone Applications
description: This page convers how to turn your module into an installable Saito Application
published: true
date: 2024-09-27T10:05:41.726Z
tags: 
editor: markdown
dateCreated: 2024-09-27T09:25:06.675Z
---

# Compiling Standalone Application

The default way to compile applications is to edit the ```/config/modules.config.js``` file on your server. Modules that are included in the CORE section of that file are installed on the server. Modules that are included in the LITE section of that file are compiled into the ```saito.js``` file that the server will distribute to any browsers that ask for a copy.

The downside of this approach is that you need to run a node, and/or users need to visit your Saito node in order to use your application. For this reason, Saito supports the ability to compile applications into special application-packages that browsers can install by drag-and-drop into their wallet.

## AppStore - Compilation

Make sure your local Saito node is compiled with both CORE and LITE support of the ```appstore``` module, and then start your server and visit ```/appstore``` in your browser. You will see a drag-and-drop target.

<br />
<img src="/compile-01.png" style="width:600px" />

Drag your ZIP file onto this target and a popup will appear confirming the details of the application. If there is an issue reading the .zip file you likely have a problem with the application -- make sure it compiles and runs locally before you attempt to compile for remote installation. Otherwise click the button to generate the application.

Once you click the button, it may take a short while, but your machine will compile your module into a standalone file and download it to your machine. Find that file -- this is the application-file that browsers will be able to install.

<br />
<img src="/compile-03.png" style="width:600px" />

## AppStore - Installation

To install these standalone application packages, click on the top-right menu in any Saito application and click on the Account button below your wallet balance. On the overlay that appears, look for the "+" button that shows up on the top-right of your installed modules. 

<br />
<img src="/compile-03.png" style="width:600px" />

Click on the add button and you'll get another drag-and-drop target. Drag the application package that you previously compiled into this window.

<br />
<img src="/compile-04.png" style="width:600px" />

A popup will appear to confirm installation. Confirm that you want to install this application and click "Install" if so. 

<br />
<img src="/compile-05.png" style="width:600px" />

Your browser will unpack the application, save it in your wallet and refresh. Once your browser reloads it will load the application you have just installed along with all other modules. You can now toggle it on-or-off like any other module.



