---
title: Refactor 2026 - Rust Pipeline
description: 
published: true
date: 2026-07-17T11:04:42.604Z
tags: 
editor: markdown
dateCreated: 2026-07-17T10:45:19.381Z
---

# A Smoother Rust Pipeline

One of the biggest changes in Refactor 2026 is invisible to most users, but it affects almost everything they do. Saito's Rust/WASM/JS pipeline has been redesigned to make the network faster, simpler, and more intuitive. This reduces the amount of code required to connect applications to the consensus engine while exposing far more of the blockchain's functionality directly to developers.

The indirect result is a platform that feels more responsive. Applications load more quickly, blockchain operations integrate more naturally into user interfaces, and developers can build richer applications without reimplementing core functionality in JavaScript.

## Rust / WASM Architecture

- Significant expansion of the Rust ↔ WASM interface.
- Generic object bridge between Rust and JavaScript instead of many hand-written wrappers.
- Most Rust structs can now be exposed directly to JavaScript.
- JavaScript can invoke far more Rust functions directly.
- Reduced serialization and deserialization across the WASM boundary.
- Improved handling of large Rust objects without repeated conversion.
- Cleaner ownership and lifetime management for exported WASM objects.
- Better mapping of Rust APIs into idiomatic JavaScript.
- Removal of duplicated functionality implemented independently in Rust and JavaScript.
- Simplified build pipeline for Rust/WASM packages.
- Cleaner separation between `saito-core`, `saito-wasm`, and `saito-js`.

## SaitoJS NPM Layer

- New `app.core` abstraction exposing consensus functionality.
- Cleaner separation between consensus code and application code.
- Consistent APIs for blockchain, wallet, networking, cryptography, scripting, and storage.
- Better modularization of platform services.
- Less internal plumbing exposed to applications.
- Standardized interfaces across modules.

## Event System

- Replacement of coarse `wallet-updated` events with granular events.
- More specific blockchain lifecycle events.
- Better synchronization notifications.
- More granular wallet state updates.
- Better transaction lifecycle events.
- NFT-specific update events.
- Reduced need for polling.
- More reactive application architecture.

## Wallet / Blockchain APIs

- Direct access to blockchain objects from JavaScript.
- Cleaner blockchain API surface.
- Better access to blocks.
- Better access to transactions.
- Better access to slips.
- Better access to UTXOs.
- Better access to wallet state.
- Pending vs. confirmed balance tracking.
- Cached balance support.
- More efficient wallet refresh logic.

## Blockchain Objects

- Richer transaction objects.
- Richer block objects.
- Cleaner serialization.
- Better JavaScript representations of Rust objects.
- Improved access to transaction metadata.
- Better support for SPV objects.
- Improved scripting object representations.

## RustScript Integration

- Scripting engine moved into Rust.
- JavaScript parser retired.
- Script represented as a structured AST.
- JSON serialization of script trees.
- JavaScript can manipulate Rust script objects directly.
- Import and export of script structures.
- Shared scripting implementation between consensus and UI.
- Script testing against live transactions.
- Pay-to-Script-Hash (P2SH) integrated into consensus.

## Digital Asset Infrastructure

- Native token implementation.
- Native NFT implementation.
- NFT split support.
- NFT merge support.
- New slip types supporting programmable ownership.
- Better transaction construction APIs.
- Asset abstractions exposed through core APIs.

## Consensus / Networking

- Cleaner networking abstractions.
- Simplified peer lifecycle.
- Better synchronization pipeline.
- Reduced dispatcher complexity.
- Better routing between Rust and JavaScript networking layers.
- Cleaner initialization sequence.
- Simplified blockchain startup.

## Performance

- Less copying across the WASM boundary.
- Fewer temporary objects.
- Lower memory allocations.
- Reduced JavaScript/Rust context switching.
- Faster object access.
- More efficient event propagation.
- Reduced redundant synchronization.
- Better scalability under load.


## Architectural Shift

- `saito-core` becomes the authoritative implementation of blockchain functionality.
- `saito-wasm` becomes a thin interoperability layer between Rust and JavaScript.
- `saito-js` becomes an application framework built on top of consensus services rather than a parallel implementation.
- Consensus functionality is implemented once and consumed everywhere.
- New platform capabilities can be exposed to applications without duplicating implementation across languages.


The simplified architecture removes much of the boilerplate that previously surrounded blockchain development and has significantly improved the speed of development. As a result, features that previously required changes across multiple layers of the software stack can often be implemented in a single pass.

## A Foundation for the Future

While many Refactor 2026 features are immediately visible -- native digital assets, programmable ownership, the integrated marketplace, and redesigned applications -- they all build upon this underlying architectural work.

For most users, the only noticeable difference will be that Saito feels faster and nodes scale better. But for developers working on consensus-layer logic, these changes are among the most important.