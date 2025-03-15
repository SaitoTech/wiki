---
title: Run a Node
description: 
published: true
date: 2025-03-15T05:17:57.828Z
tags: 
editor: markdown
dateCreated: 2024-10-15T23:32:31.744Z
---

# Running a Node

Running a Saito node requires downloading our Rust software client and configuring it to run whichever modules you want installed on your node. This page describes the process of doing this. We assume a Linux or Mac system and basic familiarity with teh comand-line.

For installation instructions, visit our page on installing our [Saito Rust](https://github.com/SaitoTech/saito-lite-rust) client. This page covers the process of downloading the software, installing any necessary dependencies, and configuring.

Once you have installed the Rust client, we have a description of how to build and host [Web 3 applications on Saito](/tech/applications).

See our section for [building applications](https://wiki.saito.io/en/tech/building_apps) once installation is complete.

Note that an application serving Saito Node, or Saito Nodes generally, do not generate passive validator income like PoS. Saito rewards nodes which generate transaction fees through applications or wallet software, i.e. rewards require bringing value to users.

## [Installation](/tech/install/javascript)

See the [installation](/tech/install/javascript) page for instructions on installing, configuring and building applications on Saito-Lite-Rust. SLR supports Linux, Mac and Windows.

#### Requirements:
- Machine with at least 2GB RAM.
- Build tools: git, g++, make, python, tsc
- Stack: node.js (v.16+), npm (v6+)
- TypeScript
- Saito-Lite-Rust - [Github](https://github.com/saitotech/saito-lite-rust)



<!--
Saito-Lite-Rust runs atop NodeJS. Instructions for installing are available for:

- [Linux](/tech/installation/javascript/linux)
- [Mac](/tech/installation/javascript/mac)
- [Windows](/tech/installation/javascript/windows)


## [Building Apps](/tech/applications/building_apps)

If you want to get started building applications, we recommend starting with our [tutorial series](/tech/applications/building_apps) for new Application Developers.

Applications like the [Saito Arcade](https://saito.io/arcade) run inside the Saito Wallet, which receives on-chain and off-chain messages and passes them into the modules that are running inside the user wallet. See our [applications page](/tech/applications) for examples and descriptions of the Web 3 apps currently running on Saito.
-->
## [Deploy](/tech/javascript/deployment) Your Node
Visit the [deploy instructions](/tech/javascript/deployment) to learn how to connect your Saito-Lite-Rust Node to the public internet.
  
<!--
## Using Saito in your Browser

Once you have run `npm start` above it will take a few moments for the Saito software to initialize and start. You will eventually see an animated Saito logo scroll across your terminal. Once that is done simply open a browser and visit:

https://127.0.0.1:12101/arcade

This will load the Saito Arcade - one of our default applications. If everything has gone as planned, you now have a working version of Saito for use in local testing or development. 

Take your next steps into application development with [tutorial one](https://wiki.saito.io/en/tech/tutorial-1-deploy-install-application) which explains how to build a simple application that attaches data to transactions and broadcasts them into the network.
-->


## External References

Source code and more documentation available on our public GitHub repository:

https://github.com/saitotech/saito-lite-rust


