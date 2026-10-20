---
title: Saito Documentation
description: 
published: true
date: 2026-10-20T09:12:05.828Z
tags: 
editor: markdown
dateCreated: 2024-10-29T21:33:20.620Z
---

# Development and Documentation

The easiest way to develop on Saito is point your local AI at our [files for coding agents](https://github.com/SaitoTech/saito/tree/prod/README), installed locally at:

```/saito/README/```

The two subdirectories in this folder contain the files needed to understand *how Saito Consensus works* and *how to develop applications atop the platform*. Any modern AI should be able to consume these files and produce reasonable code based on your requirements.

If you run into problems with development please reach out to a member of the team. Project members are happy to support with application development and we like to update the AI docs as we learn of problems that people run into, so don't be afraid to reach out by email at info@saito.io.


## Manual Documentation

Learning Saito development requires a conceptual shift if you want to do the work manually without AI assistance. The server-client model melts away as applications run simultaneously on all nodes. The links in this section provide reference information on how to build these applications.

### [General Conventions](/docs/modules)
General guideline and instructions for working with and creating Saito Modules. This page focuses on what makes Saito modules truly web3 and different than what passes for "peer-to-peer" applications on other networks.


### [UI Components and Templates](/docs/ui-components) 
Many Saito applications re-use the same UI components (Saito Overlay, Saito User, Saito Menu). This sections explains some of the UI Components that exists and how you can quickly and easily incorporate them in your own applications.

### [CSS Design](/docs/css)
Want your application to "fit in" visually with the other applications in the Saito stack? This section of our docs explains the standard CSS classes that are available to ALL applications by default. Using these can save time and effort when polishing the look-and-feel of an application.

### [ZK-Proofs Support](/docs/zk-proofs)
This section contains a quick tutorial on how to get ZK-Snarks working in your Saito Application. This is a useful approach for building privacy-protecting apps on the Saito tech stack.

### [Wasm Support](/docs/wasm)
This section contains guidelines on how to use external WASM libraries into your Saito Application. Useful if you want to incorporate third-party code that is only available as a WASM binary.

## APIs

### [Transaction API](/docs/transactions)
The Module API explains the functions that your module can include and extend to react to common events (inbound transactions, peer messages, chain-reorganizations, etc) and to store data and send messages to other peers on the network.

### [Scripting API](/docs/scripting)
The Scripting API explains the basics needed to start writing Saito Scripts that your modules and NFTs can include to enable advanced forms of cryptographic validation like multi-sig support and token-ownership validation.

### [Module API](/docs/module-api)
The Module API explains the functions that your module can include and extend to react to common events (inbound transactions, peer messages, chain-reorganizations, etc) and to store data and send messages to other peers on the network.

### [Events API](/docs/events-api)
Modules can communicate with each other by broadcasting events and listening for events broadcast by other modules. The Events API explains how to listen for these events and respond when they are triggered, such as running specific code when a user adds a friend's contact information to their wallet.

### [Services API](/docs/services-api)
Services are used to provide data to other nodes on the network, such as sharing RedSquare transactions or providing DNS lookup services for peers. The Services API explains how peers can inform other peers that they can be queried for special types of data.

### [Network API](/docs/network-api)
Interface with Saito nodes of all types via the networking API. The network layer that underpins the Saito client. Since messages are passed between nodes in a binary format, this section is primarily intended for developers who wish to modify the core routing software or add additional features to the core network stack.

