---
title: Saito Consensus and Incentive Compatibility
description: 
published: true
date: 2025-04-07T21:42:38.246Z
tags: 
editor: markdown
dateCreated: 2025-04-07T19:21:22.502Z
---

# Incentive Compatibility

Saito Consensus is the first distributed consensus mechanism believed to be incentive compatible with the social choice rule of pareto optimality. It works by create a combinatorial auction that forces trade-offs in the consumption and production of the various forms of utility that can be mediated through a blockchain:

1. **Blockspace**
2. **Speed-of-Inclusion** 
3. **Collusion Goods** (off-chain bribes)

Users reveal their private valuations for all three goods by manipulating two strategic levers: bid distribution (how the bid is broadcast into the network) and bid amount (the fee that is paid).

Producers reveal their cost structure in producing collusion goods through the decision to include their own fees to speed-up block production, an act which increases efficiency by subsidizing production of the forms of utility favoured by honest users.

Manipulating these levers allow users and producers to reveal their ordinal preferences across multiple dimensions. The mechanism works because users who dictate any two forms of utility must let the third be set at market rates by the most efficient producer, and rational producers will drive the network towards the point at which fees are used to generate utiilty with optimal efficiency.

The mechanism qualifies as an indirect mechanism with truthful preference revelation in the tradition of Hurwicz and Maskin. It also meets the criteria Hurwicz and Jordan establish for iterative convergence on pareto optimality. Presuming one accepts the existence of multiple competing "auctioneers" as a valid auction design -- it is an economically efficient combinatorial auction.

