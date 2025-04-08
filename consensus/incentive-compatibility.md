---
title: Saito Consensus and Incentive Compatibility
description: 
published: true
date: 2025-04-08T19:32:16.781Z
tags: 
editor: markdown
dateCreated: 2025-04-07T19:21:22.502Z
---

# Incentive Compatibility

Saito Consensus is the first distributed consensus mechanism believed to be incentive compatible with the social choice rule of pareto optimality. It works by creating a combinatorial auction that forces trade-offs between the various forms of utility that can be mediated through a blockchain to affect the production and consumption of contending forms of utility simultaneously:

1. **Blockspace**
2. **Speed-of-Inclusion** 
3. **Collusion Goods** (off-chain kickbacks)

Users reveal their private valuations for all three goods by manipulating two strategic levers: bid distribution (how the bid is broadcast into the network) and bid amount (the fee that is paid). These preferences are revealed indirectly in the way that transactions are submitted to the distributed auction.

Producers reveal their competitive advantage at producing all three forms of utility through the optional decision to include their own fees in blocks, an act which -- if taken -- always increases the efficiency with which the network produces whatever forms of utility are favoured by honest users.

The mechanism achieves incentive compatibility because users who dictate any two forms of utility must let the third be set at market rates by the most efficient producer, and the mechanism rewards producers who drive the network towards optimality by advantaging them in both the production of blocks and (later) collection of payments.

Routing work mechanisms qualify as an indirect mechanism with truthful preference revelation in the tradition of Hurwicz and Maskin. They also meet the criteria Hurwicz and Jordan establish for an algorithm that can iteratively convergene on a pareto optimality outcome -- only this time without the need for a trusted third-party to run the mechanism. Presuming one accepts the novel approach with multiple competing "auctioneers" as a valid auction design -- it is also an economically efficient combinatorial auction.

