---
title: Refactor 2026 - Decentralized Finance
description: 
published: true
date: 2026-07-17T11:41:49.841Z
tags: 
editor: markdown
dateCreated: 2026-07-17T10:49:32.009Z
---

# Decentralized Finance

Refactor 2026 brings native P2SH support to Saito, allowing users to transfer SAITO and NFTs to addresses which impose restrictions on who can subsequently transfer, split, merge or destroy them. As unlike assets locked into third-party smart contracts, these criteria are set by the users who create the transactions.

Among the various updates that relate to the launch of programmatic finance on Saito with this release are:

## Native Digital Assets

- RustScript integrated into the consensus engine.
- JS/APP layer access to script execution/validation through app.core.*
- Pay-to-Script-Hash (P2SH) support in transaction validation.
- Bitcoin-style basic OPCODE support (checksig, checkhash, etc.)
- Saito-style advanced OPCODE support (checkpathhop, checkownnft, etc.)
- Native escrow primitives
- New address format for P2SH addresses (0x00)

## Marketplace and Applications

- Saito Store support for asynchronous NFT transfers
- Saito Store supports all NFT-encoded assets.
- atomic swaps for NFT <-> Saito asset transfers
- UI components for NFT creation / transfer / management
- UI updates on NFT transfer / arrival / update
- Rustscript supports click-to-build scripting
- Rustscript supports click-to-unlock scripting
- Rustscript advanced publishing and testing features

## Developer Platform

- ccnsensus services exposed as reusable platform APIs.
- New slip types supporting programmable ownership.
- Shared transaction construction APIs.
- Shared cryptographic primitives.
- Improved consensus object access from JavaScript.

## Architectural Shift

- applications publish into other applications via P2SH transactions
- UI Components that receive objects and monitor user actions to determine if they have been broadcast into the network as P2SH transactions and of what kind, permitting cross-application notification of user intent without imposing restrictions on underlying functionality
- P2SH formatted transactions as a meta-protocol for distributed comms

These features may seem abstract, but provide the foundation for a new generation of decentralized applications that are not limited by the architecture of virtual machines or smart contracts. And which provide protection against certain types of MEV that cannot be stopped in those network.

With these improvements hitting Saito's application layer, every Saito wallet is now capable of creating NFTs and other digital assets automatically, and creating advanced scripts through a new UI that makes it easy 