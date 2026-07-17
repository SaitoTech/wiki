---
title: Refactor 2026 - User Experience
description: 
published: true
date: 2026-07-17T12:51:06.902Z
tags: 
editor: markdown
dateCreated: 2026-07-17T10:53:59.421Z
---

# Blockchain That Feels Like Software

For many people, the hardest part of using blockchain applications isn't understanding the technology—it's waiting for the technology to catch up.

Transactions disappear into the network without explanation. Interfaces freeze while waiting for confirmations. Wallets suddenly update without warning. Users are left wondering whether anything is happening at all.

Refactor 2026 redesigns the experience from the ground up. Applications communicate with users, explain what they're doing, and update continuously as the network progresses. Instead of exposing the mechanics of the blockchain, Saito lets people focus on the task they are trying to accomplish.

## Live Feedback

Applications no longer leave users guessing.

When the network is processing a transaction, applications display progress, estimate when the next block will arrive, and update automatically as new information becomes available.

Whether you're publishing a blog post, creating an NFT, making a purchase, or transferring digital assets, the interface explains what is happening instead of simply asking users to wait.

# User Experience

## Responsive Applications

- Rust broadcasts events to enable granular updates
- UI tracks transaction status throughout confirmation
- Reduced duplication and complexity in JS layer

## Guided Workflows

- NFT creation integrated directly into publishing workflows.
- Multi-step publishing workflow for access-controlled content.
- Progressive disclosure of advanced features.
- Simplified asset creation flows.

## Wallet Improvements

- Pending and confirmed balances displayed separately.
- Improved synchronization with blockchain state.
- More responsive balance updates.
- Native asset management integrated into the wallet.

## NFT Management

- Redesigned NFT management interface.
- Support for creating, viewing, splitting, and merging NFTs.
- Improved NFT creation overlays.
- Pre-populated NFT creation from applications.

## Shared UI Components

- Standardized overlay framework.
- Reusable interface components across applications.
- Common navigation and layout system.
- Shared asset management components.

## Application Interfaces

- RedSquare interface redesign.
- Explorer interface redesign.
- Store interface redesign.
- Stack publishing workflow redesign.

## Themes

- Default platform theme simplified.
- Theme architecture prepared for downloadable themes.
- Themes distributed as native digital assets.

## Platform Polish

- CSS cleanup across applications.
- Consistent styling throughout the platform.
- Responsive layout improvements.
- Standardized application behavior.

These combine into more "progressive workflows" where components take actions and monitor the state of the blockchain in real-time to notify users when actions are completed. "Distributed" no longer means the application cannot inform you when the next step is ready.

The means the biggest change in Refactor 2026 isn't any individual feature -- although there are many -- but how the platform feels when you use it:

* Applications are faster.

* Interfaces are clearer.

* Ownership is easier to understand.

Applications walk users through how to create access keys and NFTs and how to use them. The act of using the network provides a tutorial on how to use the network. By the time users are ready for more advanced features, they already have an intuitive understanding of how Saito works.
