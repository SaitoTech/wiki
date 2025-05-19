---
title: Run a Node
description: 
published: true
date: 2025-05-19T10:21:52.495Z
tags: 
editor: markdown
dateCreated: 2024-10-15T23:32:31.744Z
---

# Running a Node

Running a Saito node requires downloading our a Saito client and configuring it to run any modules you wish. This page describes the first step in doing this -- downloading and installing the default Saito client. We assume a Linux or Mac system and basic familiarity with the comand-line.

#### Requirements:
- Machine with at least 2GB RAM.
- Build tools: git, g++, make, python, tsc
- Stack: node.js (v.16+), npm (v6+)
- TypeScript
- https://github.com/saitotech/saito-lite-rust


#### Installation Instructions:

Instructions for installing Saito are available for the following platforms:

- [Linux](/tech/installation/javascript/linux)
- [Mac](/tech/installation/javascript/mac)
- [Windows](/tech/installation/javascript/windows)



<!------

## [Building Apps](/tech/applications/building_apps)

If you want to get started building applications, we recommend starting with our [tutorial series](/tech/applications/building_apps) for new Application Developers.

Applications like the [Saito Arcade](https://saito.io/arcade) run inside the Saito Wallet, which receives on-chain and off-chain messages and passes them into the modules that are running inside the user wallet. See our [applications page](/tech/applications) for examples and descriptions of the Web 3 apps currently running on Saito.
-->
## Deploy Your Node
Visit the [deploy instructions](/tech/applications/deploy/saito-lite-rust) to learn how to connect your Saito-Lite-Rust Node to the public internet.
  
<!--
## Using Saito in your Browser

Once you have run `npm start` above it will take a few moments for the Saito software to initialize and start. You will eventually see an animated Saito logo scroll across your terminal. Once that is done simply open a browser and visit:

https://127.0.0.1:12101/arcade

This will load the Saito Arcade - one of our default applications. If everything has gone as planned, you now have a working version of Saito for use in local testing or development. 

Take your next steps into application development with [tutorial one](https://wiki.saito.io/en/tech/tutorial-1-deploy-install-application) which explains how to build a simple application that attaches data to transactions and broadcasts them into the network.
-->


## Looking for Something Else?

Source code and more documentation available on our public GitHub repository:

https://github.com/saitotech/saito

Tutorials on building applications are available in our section for [building applications](/tech/applications/building_apps) once installation is complete.


