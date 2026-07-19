---
title: Refactor 2026 - User Experience
description: 
published: true
date: 2026-07-19T03:51:36.102Z
tags: 
editor: markdown
dateCreated: 2026-07-17T10:53:59.421Z
---

# Blockchain That Feels Like Software

For many people, the hardest part of using a blockchain isn't sending a transaction but wondering what is happening in the "void" that follows after the transaction is broadcast.

In networks with this problem, transactions disappear without explanation. Interfaces freeze while waiting for confirmations. Wallets receive payments and NFTs silently and the users are left wondering whether they have done everythign correctly and anything is happening at all.

Refactor 2026 includes upgrades that make these issues disappear. Applications have been upgraded to communicate with users after transactions have been broadcast, explain what is happening and how long users should wait, and track the blockchain continuously to update as soon as the network confirms the results. Applications no longer leave users guessing.

Whether users are publishing blog posts, creating NFTs, making purchases, or testing application scripts, the improvements below allow applications to explain what is happening instead of just asking users to wait and trust the process....

## A More Response Wallet

- Rust broadcasts granular events on network/wallet updates
- Pending and confirmed balances displayed separately
- UI tracks balance changes throughout confirmation
- Elimination of edge-cases created by JS data-caches
- Similar updates on NFT transfers and more

## UI Components

- NFT creation is slick
- Simplified asset transfer/receipt flows
- Progressive disclosure of advanced features
- Applications can "pre-populate" NFT creation UIs
- Applications can "pre-populate" Store listings

## Application Interfaces

- General CSS upgrade
- RedSquare interface redesign
- Explorer interface redesign
- Store interface redesign
- Stack publishing workflow redesign
- Videocall interface redesign
- CSS Themes distributed as native digital assets.

The most noticable change across applications is a shift to "progressive workflows" where UI components monitor the state of the blockchain and notify users when actions are expected to be completed, and then update again once they are. This removes a lot of uncertainty that users naturally have when using a distributed application.

These changes mean the biggest change in Refactor 2026 isn't any individual feature, the platform now teaches you what is happening as you use it. Instead of asking users to understand NFTs, transactions, blocks and confirmations, the network provides a tutorial on them through casual updates. By the time users are ready for more advanced features, they already have an intuitive understanding of how blockchain works.
