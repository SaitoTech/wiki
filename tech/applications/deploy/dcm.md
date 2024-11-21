---
title: Dynamically Compiled App Deployment
description: Instructions for compiling and installing DCM, also known as, standalone applications
published: true
date: 2024-11-21T20:14:40.373Z
tags: 
editor: markdown
dateCreated: 2024-11-21T20:05:12.071Z
---

# Standalone (DCM) Application 

This page gives instructions on the compilation and installation steps for standalone applications - those that don't require a node to serve compiled code to users. Also known as *Dynamically Compiled Modules.*

## Compile

Make sure your local Saito node is compiled with both CORE and LITE support of the `devtools` module, and then start your server and visit `/devtools` in your browser. You will see a drag-and-drop target.

The tool is also hosted on our Saito Node at:
- https://saito.io/devtools/

<br />
<img src="/compile-01.png" style="width:600px" />

Be sure the application compiles and runs locally before compiling for remote installation to avoid any issues.

Provide ZIP file of the module directory and confirm the details of the application in the popup, then generate the application package.

Wait for package compilation to complete (be pateint, as there may be no indicator) - once finished, the tool will offer to save the package on the local machine. This is the application-file that browsers will be able to install.

<!--
### Compile

Developers, modders, or auditors will want to first compile their modules to reduce the steps needed for anyone wishing to install the module.

On any operating Saito-lite-Rust Node, a web page will be hosted at `/devtools` which will the compiler in the browser and offer further instructions.

The tool is also hosted on our Saito Node at:
- https://saito.io/devtools/
-->

## Install

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