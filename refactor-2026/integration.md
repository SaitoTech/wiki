---
title: Refactor 2026 - Integration
description: 
published: true
date: 2026-07-17T12:44:46.157Z
tags: 
editor: markdown
dateCreated: 2026-07-17T10:52:33.416Z
---

# Everything Works Together

Most blockchain applications are built as isolated products. They have their own tokens, their own marketplaces, their own wallets, and their own systems for managing users and digital assets. Even when they run on the same blockchain, connecting them together usually requires custom integrations and significant development effort.

Refactor 2026 takes a different approach.

Saito applications are built on a common platform. They share the same wallet, the same digital asset system, the same programmable ownership model, the same marketplace, and the same developer APIs. Features developed for one application automatically become available across the rest of the ecosystem.

The result is a platform where applications become more valuable as new ones are added.

## System Integration
- granulad events tracking SAITO/NFT transfters
- NFT creation overlays programmatically invokable
- app.core.* heirarchy brings Rust functions into JS

## Applications

- Publishing workflow integrated with NFT creation
- Access Keys can be created directly during publication
- Access Keys can be listed in the Store immediately after creation
- Saito NFT Listings integrate with Store listing components
- Store UI Components can be invokved by 3rd party apps
- Shared NFT ownership/display components Store and Wallet

## Links and Sharing

- Shortlink generation moved into `ModTemplate`.
- Modules can generate shareable links through a common API.
- Server-side shortlink routing standardized across applications.
- Open Graph support integrated into the shared shortlink architecture.


Other blockchain ecosystems are mostly composed of isolated applications that have little in common. These applications run on private servers with off-chain databases and restricted user accounts. They read and write transactions to the chain and have little else in common.

Saito is something different.

Refactor 2026 continues our work building the Saito network into a unified environment where wallets, digital assets and applications work together. Developers can provide applications that do not rely on existing components, but -- as in other open source ecosystems like Linux -- it is easier to integrate with other open source tools and benefit from existing network effects. 