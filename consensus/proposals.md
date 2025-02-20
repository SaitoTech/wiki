---
title: Saito Implementation Proposals
description: 
published: true
date: 2025-02-20T10:32:34.394Z
tags: 
editor: markdown
dateCreated: 2022-05-06T09:39:55.380Z
---

# Saito Implementation Proposals

A list of proposals for how to improve our implementation of Saito Consensus. To submit a proposal, you may send a pull request on the proposals folder on our [Saito Proposal Repository](https://github.com/SaitoTech/saito-implementation-proposals).

## 001 Simplified Staking (active)

Proposal to re-use the ATR rebroadcast mechanism as the staking payment mechanism. Under this approach, while UTXO are charged per-byte fees for each rebroadcast, they are also eligible for a subsidy based on the amount locked-up in the UTXO. Benefits include a fully open staking table, savings in calculating payouts, and the ability for users to target "forever storage" by creating transactions where staking income compensates for data-rebroadcast. 

[Link to Official Proposal](https://github.com/SaitoTech/saito-implementation-proposals/blob/main/proposals/001_simplified_staking.md)


## 002 One-Time Receive Outputs (not active)
Proposal to add a specific of scripting use-case in Saito that would make it easier to support NFTs. From the in-house dev perspective, the question is how much something like would be simplier if we implemented a P2SH system and -- if so -- when and how we should implement that. Right now scripting is set for 4th era, but perhaps we should push that up to make NFT-trading easier once the WASM client is done. Feedback on this is very welcome. Thank you to Matt for writing this up.

[Link to Official Proposal](https://github.com/mat888/saito-implementation-proposals/blob/main/proposals/002_one-time-receive-outputs/002_one-time-receive-outputs.md)


## 003 Bound UTXO (under consideration)
Proposal to add a specific class of transaction slip that must be moved in concert with another normal UTXO slip (the "bound" UTXO) in a way that prevents the duplication of a the bound slip once it has been created. This mechanism can be used to add support for NFTs and colored coins, w divisibility.

[Link to Official Proposal](https://github.com/SaitoTech/saito-implementation-proposals/blob/main/proposals/003_bound_utxo.md)

