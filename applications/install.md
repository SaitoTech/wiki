---
title: Installing Saito Applications
description: 
published: true
date: 2025-05-26T09:43:00.339Z
tags: 
editor: markdown
dateCreated: 2025-05-26T09:43:00.339Z
---

# Installing Saito Applications

This page assumes you are a Saito user who wants to drag-and-drop a Saito module into your browser to install it, as similar to the .saito files that can be found in our [applications](/applications) section. If you are trying to install modules onto a server node, see our separate page for [server app-configuration](/config).

To install a DCM module, click on the top-right menu in any Saito application and click on the Account button below your wallet balance. On the popup overlay that appears, look for the "+" button that shows up on the right-hand side above your list of installed modules.

<br />
<img src="/compile-03.png" style="width:600px" />

Click on that add button and you'll see another drag-and-drop target. Drag the application package (.saito file) that you previously compiled or downloaded into this window.

<br />
<img src="/compile-04.png" style="width:600px" />

A popup will appear to confirm installation. This shows the name of the application and the publickey of the publisher who compiled it. Confirm that you want to install this application and click "Install" if so.

<br />
<img src="/compile-05.png" style="width:600px" />

Your browser will unpack the application, save it in your browser and refresh. Once your browser reloads it will load the application you have just installed along with all other modules. You can now toggle it on-or-off like any other module.

NOTE: locally-installed applications will persist in your browser even if you nuke your wallet for a new identity and public/private keypair. To remove an installed DCM module for good, click on the *Clear Local Cache* option that is at the top of the Account overlay, next to the buttons used to backup your wallet.