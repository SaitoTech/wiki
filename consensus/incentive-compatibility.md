---
title: Saito Consensus and Incentive Compatibility
description: 
published: true
date: 2025-04-07T20:52:14.989Z
tags: 
editor: markdown
dateCreated: 2025-04-07T19:21:22.502Z
---

# Incentive Compatibility

Saito Consensus is the first distributed consensus mechanism believed to be incentive compatible with pareto optimality. It does this by creating a combinatorial auction over the three forms of competing utility that can be delivered through a blockchain:

1. **Blockspace**
2. **Speed-of-Inclusion** 
3. **Collusion Goods** (bribes for private payment)

Users express their preferences for all three by manipulating two levers:

1. **Bid Distribution:** how the bid is broadcast into the network affects the degree of competition that exists to collect it, which affects the marginal profitability for producers of servicing the transaction and thus providing #2 and #3.

2. **Bid Amount:** the value of the fee paid affects the speed of transaction inclusion regardless of the distribution strategy selected, as higher fees trigger faster block production.

Manipulating these levers allow users to reveal their ordinal preferences across multiple dimensions. Distribution strategies can be used to increase provision of collusion goods, and fee-levels can then be micro-optimized to purchase faster/slower inclusion.

The mechanism works because users who dictate any two forms of utility must let the third be set by the most efficient producer at aggregating inbound fee-flow, and less efficient producers can only out-compete this producer by emulating their efficiency at delivering value to users, which requires spending their own money to subsidize production of the forms of utility favoured by honest users.

User preferences (setting the demand curve) are revealed by the trade-offs users accept across the three dimensions, while producer preferences (cost-of-supply which controls the supply curve) are revealed by their willingness to spend their own money to outcompete their peers.

The mechanism qualifies as an indirect mechanism with truthful preference revelation in the tradition of Hurwicz and Maskin. It meets the criteria Hurwicz and Jordan establish for iterative convergence on pareto optimality. And -- presuming one accepts the existence of multiple competing auctioneers as a valid auction design -- it is an economically efficient combinatorial auction.

