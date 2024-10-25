---
title: Run a Node
description:
published: true
date: 2024-10-16T01:06:59.198Z
tags:
editor: markdown
dateCreated: 2024-10-15T23:32:31.744Z
---

# Running a Node

This page provides information for running a [Saito-Lite-Rust Node](https://github.com/SaitoTech/saito-lite-rust), which is typically the best option for hosting and developing [Web 3 applications on Saito](/tech/applications). See our page for [building applications](https://wiki.saito.io/en/tech/building_apps) once installation is complete.

If you are interested in protocol development, visit the page for our [Core Rust Node](/tech/rust).

## [Installation](/tech/installation/javascript)

See the [installation](/tech/installation/javascript) page for instructions on installing, configuring and building applications on Saito-Lite-Rust. It accommodates Linux, Mac and Windows.

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
-->

## [Building Apps](/tech/building_apps)

If you want to get started building applications, we recommend starting with our [tutorial series](/tech/building_apps) for new Application Developers.

Applications like the [Saito Arcade](https://saito.io/arcade) run inside the Saito Wallet, which receives on-chain and off-chain messages and passes them into the modules that are running inside the user wallet. See our [applications page](/tech/applications) for examples and descriptions of the Web 3 apps currently running on Saito.

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

For more code and documentation please visit our public GitHub repository:

https://github.com/saitotech

This repository includes older branches and versions which are not being maintained. If you are interested in developing on the public site, please make sure you are using the latest two live repositories:

https://github.com/saitotech/saito-lite-rust
( JavaScript )
https://github.com/saitotech/saito-rust-workspace
( Rust )
