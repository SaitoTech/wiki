---
title: Architecture and Design - Rust
description: Installation instructions for Saito-Rust
published: true
date: 2023-09-21T07:03:55.291Z
tags: 
editor: markdown
dateCreated: 2022-03-23T07:18:36.618Z
---


# Rust Architecture and Design

Documentation on the Rust client is fairly minimal as the codebase and architecture is still under active development. Our main Rust repository contains three major components:

 - saito-core
 - saito-rust  
 - saito-wasm  

**Saito-Core** contains the majority of the code that runs the blockchain. This code is intended to be compiled into a binary package that can also be deployed to browsers (and integrated with other programming languages) as part of the WASM library. Clients that use this optimized bundle will simply need to pass a series of handlers into the code on initialization that will receive outbound messages and handle language-specific tasks like networking and data storage.

**Saito-Rust** contains the Rust-specific code that makes **Saito-Core** fully functional. It initializes the components contained in **Saito-Core**, and passes them the Network and Storage handlers needed for the core components to save the blockchain and interact with the network.

**Saito-Wasm** contains the middleware needed for javascript clients and applications to interact with **Saito-Core**. It defines the functions that javascript applications like the in-browser wallet call to interact with the consensus-handling parts of the Rust / WASM libraries.

## Limitations

The Rust software is under heavy development. It is not intended to be a useable network client for third-party developers. You are welcome to download the software, and participate in development. Or just explore the repository and see how we are doing.

