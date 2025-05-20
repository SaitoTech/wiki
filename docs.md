---
title: Saito Documentation
description: 
published: true
date: 2025-05-20T03:28:41.139Z
tags: 
editor: markdown
dateCreated: 2024-10-29T21:33:20.620Z
---

# Saito Documentation

This section of the Saito Wiki contains documentation and reference materials for developers. If you are totally new to application development, we recommend that you start by visiting our [tutorial section](/tutorials) and seeing how a basic application is written.

## Saito Modules

Saito Applications (also known as modules) require a conceptual shift. The server-client model melts away as applications run simultaneously on all nodes. As unlike almost every other tech architecture in the space, applications do not use JSON-fetches and API-keys to fetch data from databases -- information requests are submitted in real-time over the network to peer nodes.

### [General Conventions](/docs/modules)
General guideline and instructions for working with and creating Saito Modules. This page focuses on what makes Saito modules truly web3 and different than what passes for "peer-to-peer" applications on other networks.

### [Module API](/docs/module-api)
The Module API explains the functions that your module can include and extend to react to common events (inbound transactions, peer messages, chain-reorganizations, etc) and to store data and send messages to other peers on the network.

### [Events API](/docs/events-api)
Modules can communicate with each other by broadcasting events and listening for events broadcast by other modules. The Events API explains how to listen for these events and respond when they are triggered, such as running specific code when a user adds a friend's contact information to their wallet.

### [Services API](/docs/services-api)
Services are used to provide data to other nodes on the network, such as sharing RedSquare transactions or providing DNS lookup services for peers. The Services API explains how peers can inform other peers that they can be queried for special types of data.

### [UI Components and Templates](/docs/ui-components) 
Many Saito applications re-use the same UI components (Saito Overlay, Saito User, Saito Menu). This sections explains some of the UI Components that exists and how you can quickly and easily incorporate them in your own applications.

### [CSS Design](/docs/saito-css)
Want your application to "fit in" visually with the other applications in the Saito stack? This section of 
YMany Saito applications re-use the same UI components (Saito Overlay, Saito User, Saito Menu). This sections explains some of the UI Components that exists and how you can quickly and easily incorporate them in your own applications.



## Network

### [Network API](/tech/docs/wasm)
Interface with Saito nodes of all types via the networking API.

## Using Wasm in Saito Apps

### [Wasm Guideline](/tech/docs/wasm)
Guideline on how to use Wasm in saito apps
