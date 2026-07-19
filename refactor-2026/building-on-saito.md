---
title: Refactor 2026 - Building on Saito
description: 
published: true
date: 2026-07-19T03:48:11.240Z
tags: 
editor: markdown
dateCreated: 2026-07-17T10:54:52.819Z
---

# Building on Saito

Refactor 2026 is more than a collection of new features, it is a **new foundation for application development**. The platform has been redesigned to reduce complexity, eliminate duplication, and expose far more of the blockchain's capabilities directly to developers.

Instead of spending weeks integrating wallets, tokens, NFTs, marketplaces, scripting systems, and blockchain APIs, developers can begin building immediately on top of infrastructure that is already shared across the network.

## Core Architecture

- Reorganized `saito-core` into clearer architectural boundaries, separating consensus functionality from peer-to-peer networking.
- Consensus logic consolidated under `core/consensus`, with networking infrastructure consolidated under `core/network`.
- Simplified repository structure to better reflect the architecture of the platform.
- Removed legacy abstractions and duplicate code paths accumulated over multiple development cycles.
- Standardized naming conventions across the Rust, WASM, and JavaScript layers to reduce cognitive overhead when moving between codebases.
- Simplified startup flow throughout the platform so components initialize through a more consistent lifecycle.

## Rust ↔ WASM ↔ JavaScript

- Significantly expanded the Rust ↔ WASM interface, exposing substantially more consensus functionality to JavaScript.
- `app.core.*` now provides direct access to consensus functionality without requiring application-specific wrappers.
- Reduced the amount of custom middleware required when exposing new Rust functionality.
- Streamlined the Rust → WASM → `saito-js` development pipeline, reducing the feedback loop for exposing new consensus functionality to applications.
- Simplified object translation between Rust and JavaScript.
- Reduced serialization overhead across the WASM boundary.
- Standardized interface patterns across exported Rust modules.

## Networking

- Redesigned peer ownership model so peer objects exist independently of handshake completion.
- Peer handshake and blockchain synchronization now execute in parallel rather than sequentially.
- Faster initial synchronization for newly connected peers.
- Simplified peer lifecycle throughout the networking layer.
- Peer message handling no longer depends on taking ownership of peer objects.
- Reduced contention when multiple messages are processed simultaneously.
- Internal peer identity separated from public keys through unique peer UIDs.
- Cleaner separation between peer identity, cryptographic identity, and network connections.
- Improved congestion-control infrastructure for managing peer traffic.
- Added gatekeeper functionality to monitor peer behavior and message throughput in real time.
- Foundation for future bandwidth management and DDoS mitigation policies.

## Event System

- Reworked event architecture throughout the platform.
- Clearer distinction between internal messages and application events.
- More granular wallet lifecycle events.
- More granular blockchain synchronization events.
- More granular NFT lifecycle events.
- Applications can react to specific state changes rather than broad refresh events.
- Reduced reliance on polling throughout the platform.

## Wallet & Assets

- Wallet updated to support the native digital asset system.
- Native support for programmable NFTs.
- NFT split and merge operations integrated into wallet workflows.
- Improved wallet notifications for asset lifecycle events.
- Better synchronization between wallet state and application interfaces.

## RustScript

- Complete scripting engine moved from JavaScript into Rust.
- Consensus and application scripting now share a single implementation.
- Human-readable scripting language with structured internal representation.
- Script Abstract Syntax Tree (AST) represented as JSON for editing and serialization.
- Common parser shared between consensus validation and development tools.
- Native Pay-to-Script-Hash (P2SH) support added to the consensus engine.
- Extensible opcode architecture simplifies the addition of new scripting primitives.
- Built-in facilities for importing, testing, and debugging scripts against live transactions.

## Developer Workflow

- Simplified project layout throughout the repository.
- Configuration files consolidated into dedicated configuration directories.
- Startup scripts consolidated into dedicated script directories.
- Browser, server, and export builds now follow a more consistent application structure.
- Reduced number of supported startup paths throughout the codebase.
- Simplified local development workflow.
- New local linking pipeline allows developers to build against locally compiled Rust libraries without publishing intermediary packages.
- Improved automation for local development environment setup.
- Faster iteration when modifying consensus code.

## Performance

- Reduced waiting on asynchronous operations throughout the networking layer.
- Greater use of parallel execution where dependencies allow.
- Less copying of objects between Rust and JavaScript.
- Lower runtime memory usage.
- Reduced synchronization bottlenecks.
- Faster propagation of blockchain events to applications.
- Faster peer synchronization.
- Better scalability under heavy network load.

## User Interface Framework

- Continued migration toward a consistent component model based around `render()`.
- Shared overlay architecture reused across applications.
- More reusable UI components throughout the platform.
- Better separation between application logic and presentation.

## Documentation & Maintainability

- Cleaner internal APIs.
- More consistent naming throughout the platform.
- Reduced boilerplate when exposing consensus functionality.
- Simplified extension points for new consensus features.
- Improved code organization across all three layers (`saito-core`, `saito-wasm`, and `saito-js`).
- Lower maintenance burden through removal of duplicated implementations.


Whether developers are building games, financial applications, or working to improve the scalability of consensus code, all of these changes simplify the development experience. Many of the improvements outlined elsewhere in this upgrade would not have been possible were it not for these changes improving the speed of development and easy of Rust <--> JS integration.
