---
title: Refactor 2026 - Assets on the Network
description: 
published: true
date: 2026-07-17T11:14:58.171Z
tags: 
editor: markdown
dateCreated: 2026-07-17T10:47:29.982Z
---

# Assets on the Network

Refactor 2026 upgrades Saito to support DeFi-managed assets, while also improving the tools we have that let users create tokens and NFTs atop the network. Instead of existing as smart contracts that every application must integrate independently, digital assets on Saito are understood by the blockchain itself. Wallets, marketplaces, games, publishing platforms, and every other Saito application automatically recognize and support the same assets without additional development.

Updates affecting applications that create and use digital assets include:

## Native NFTs

- NFTs created directly by the wallet.
- Expanded NFT types including cryptocurrency tokens
- NFT ownership tracked by consensus.
- NFT splitting.
- NFT merging.
- Asset recombination support.
- P2SH NFTs (P2SH-protected NFTs)

## Programmable Ownership

- Multisignature ownership.
- Conditional ownership transfers.
- Time-locked ownership.
- Programmable royalty enforcement.
- Escrow-capable ownership.
- Script-controlled asset movement.

## Wallet Integration

- Native asset support in the wallet.
- Unified display of tokens and NFTs.
- Automatic asset discovery.
- Shared wallet APIs for every asset type.
- Pending and confirmed asset state.
- Improved asset synchronization.
- Native asset creation workflows.
- Asset management built into wallet UI.

## Marketplace Integration

- Assets immediately compatible with the Saito Store.
- Marketplace understands native assets automatically.
- No application-specific marketplace integration required.
- Atomic Swaps between assets during sales
- Programmable escrow during marketplace transactions.
- Asynchronous buying and selling.
- Shared marketplace infrastructure.

## Application Integration

- Assets usable across every Saito application.
- Common ownership model.
- Shared transfer APIs.
- Cross-application compatibility.
- Applications inherit asset support automatically.
- No custom token standards required.
- No per-application asset implementation.

## Publishing, Gaming & Access Control

- NFTs used as access keys.
- Subscription NFTs.
- Native game assets.
- Inventory items represented as NFTs.
- Transferable game objects.
- Stackable digital assets.
- Portable ownership between applications.
- Marketplace-ready game assets.

## Consensus Improvements

- New slip types supporting programmable ownership.
- Asset-aware transaction construction.
- Asset-aware transaction validation.
- Native asset serialization.
- Native asset propagation.
- Asset support integrated into consensus validation.

## Architectural Shift

- Digital assets become part of the consensus-layer instead of an authorization layer at the javascript boundary
- Tokens, NFTs, ownership, wallets, marketplaces, and scripting share a common foundation in the shared consensus hashmap.
- Every native asset becomes immediately portable across the Saito ecosystem with shared and consistent logic for NFT ids and shard ids, etc.
- Ownership, transfer, commerce, and programmability restrictions enforced by the core Rust / WASM layer rather than optionally implementable by every application.

In other blockchain ecosystems, NFTs are typically treated as numbers assigned to a publickey in a smart contract. Applications must be programmed to monitor those smart contracts and provide support to them. Users do not control how other parties can interact with their own NFT or token shards.

Saito shows a different and better way of handling digital ownership. All applications and user wallets inherit the ability to issue, manage, transfer, protect, and trade digital assets simply by using Saito to send a transaction into the network. Applications provide sensible defaults that get users "started" by making it easy to create this applications.

But NFTs are not limited in this way on the most fundamental level, and users have full power to upgrade and add additional restrictions on any assets or NFTs that they control in the network.