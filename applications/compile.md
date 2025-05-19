---
title: Dynamically Compiled App Deployment
description: Instructions for compiling and installing DCM, also known as, standalone applications
published: true
date: 2025-05-19T17:58:57.507Z
tags: 
editor: markdown
dateCreated: 2024-11-21T20:05:12.071Z
---

# Standalone Applications (DCM)

Want to distribute an application without the need to run a server? This page explains how to compile a Saito application into a *dynamically compiled module* (DCM). These are applications that users can *drag-and-drop* into their browser.

## Confirm Local Compilation

Make sure the application compiles and runs locally before trying to compile into a DCM. If you have any issues installing and compile your module locally, you will need to fix them before remote compilation will work. But once you have a working module...

## Compile with Devtools

Make sure your local Saito node is compiled with both CORE and LITE support for the `devtools` module. Start your server and visit `/devtools` in your browser. Alternately, try the version of devtools running on our staging server: 

https://staging.saito.io/devtools/

When the site loads you will see a drag-and-drop target.

<br />
<img src="/compile-01.png" style="width:600px" />

Create a ZIP file of your module and drag it into the drag-and-drop target in your browser. If your module is extremely large you may want to remove the /web directory from your module before zipping it to reduce it to a compilable size.

If the ZIP file contains ONLY the module directory, your browser should show a popup shortly confirming the details of the application. Immediately below that you will see a button you can click to generate the DCM module file.

Wait for package compilation to complete (be patient, as there may be no indicator) - once finished, the tool will offer to save the package on your local machine. This is your .saito application file.


## Installation

To install a DCM module, click on the top-right menu in any Saito application and click on the Account button below your wallet balance. On the overlay that appears, look for the "+" button that shows up on the top-right of your installed modules.

<br />
<img src="/compile-03.png" style="width:600px" />

Click on that add button and you'll see another drag-and-drop target. Drag the application package that you previously compiled into this window.

<br />
<img src="/compile-04.png" style="width:600px" />

A popup will appear to confirm installation. Confirm that you want to install this application and click "Install" if so. 

<br />
<img src="/compile-05.png" style="width:600px" />

Your browser will unpack the application, save it in your browser and refresh. Once your browser reloads it will load the application you have just installed along with all other modules. You can now toggle it on-or-off like any other module.

NOTE: locally-installed applications will persist in your browser even if you nuke your wallet for a new identifiy and public/private keypair. To remove an installed DCM module for good, click on the *Clear Local Cache* option that is at the top of the Account overlay, next to the buttons used to backup your wallet.