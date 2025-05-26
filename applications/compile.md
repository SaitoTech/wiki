---
title: Dynamically Compiled App Deployment
description: Instructions for compiling and installing DCM, also known as, standalone applications
published: true
date: 2025-05-26T09:43:04.726Z
tags: 
editor: markdown
dateCreated: 2024-11-21T20:05:12.071Z
---

# Standalone Applications (DCM)

This page explains how to compile a Saito application into a *dynamically compiled module* (DCM) also known as a Saito module (*.saito). These are applications that users can *drag-and-drop* into their browser to start using.

## Compile with Devtools

Make sure your local Saito node is compiled with both CORE and LITE support for the `devtools` module. Then start your server and visit `/devtools` in your browser. You can also try to use the version of /devtools we keep running on our staging server: 

https://staging.saito.io/devtools/

When the site loads you will see a drag-and-drop target.

<br />
<img src="/compile-01.png" style="width:600px" />

Create a ZIP file of your module directory and drag it into the drag-and-drop target in your browser. If your module is extremely large you may want to remove the /web directory from your module before zipping it to reduce it to a compilable size.

If you created the .ZIP file properly, you will see a popup showing you the name of the file and top-level information about the module you are compiling. Immediately below that you will see a button you can click to generate the DCM module file. This file will be compiled by the server and signed by the privatekey in your browser so others will be able to confirm it was produced by you.

Click to compile your module and wait 20-30 seconds for package compilation to complete (be patient, as there is no progress indicator) - once finished, the tool will offer to save the package on your local machine. This is your .saito application file.

Looking to install a DCM module (*.saito)? We have a separate page with screenshots showing how to drag-and-drop them into your browser [right here](/applications/install).
