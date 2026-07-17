---
title: Refactor 2026 - Integration
description: 
published: true
date: 2026-07-17T12:04:24.109Z
tags: 
editor: markdown
dateCreated: 2026-07-17T10:52:33.416Z
---

# Everything Works Together

Most blockchain applications are built as isolated products. They have their own tokens, their own marketplaces, their own wallets, and their own systems for managing users and digital assets. Even when they run on the same blockchain, connecting them together usually requires custom integrations and significant development effort.

Refactor 2026 takes a different approach.

Saito applications are built on a common platform. They share the same wallet, the same digital asset system, the same programmable ownership model, the same marketplace, and the same developer APIs. Features developed for one application automatically become available across the rest of the ecosystem.

The result is a platform where applications become more valuable as new ones are added.


## Stack Integration

- Publishing workflow integrated with NFT creation
- Access Keys can be created directly during publication
- Access Keys can be listed in the Store immediately after creation

## Store Integration

- Saito NFT Listings integrate with Store listing components
- Store UI Components can be invokved by 3rd party apps
- Shared NFT ownership/display components Store and Wallet

## Short Links

- Shortlink generation moved into `ModTemplate`.
- Modules can generate shareable links through a common API.
- Server-side shortlink routing standardized across applications.
- Open Graph support integrated into the shared shortlink architecture.


## More Than an Ecosystem

Many blockchain ecosystems are collections of independent applications that happen to share an underlying blockchain. Those applications are run by different developers on different servers and with private databases. Users must separately create accounts to create assets or list them.

Saito is becoming something different.

Refactor 2026 continues our work building the network into a unified application platform where wallets, digital assets, marketplaces and other applications are allowed to work together from the beginning. Developers can provide applications that limit how their own code is used, but cannot prevent users from bypassing it and interacting directly with the assets listed on-chain.

P2SH support and increasingly flexible core UI components make this form of integration much easier. Instead of developers preferring to stitch functionality together outside Saito, it is easier to bring external functionality into Saito and build on a foundation that already provides maximum utility.