---
title: Saito Consensus and Incentive Compatibility
description: 
published: true
date: 2025-04-07T20:41:43.289Z
tags: 
editor: markdown
dateCreated: 2025-04-07T19:21:22.502Z
---

# Incentive Compatibility

Saito Consensus is the first distributed consensus mechanism known to be incentive compatible with pareto optimality. It does this by creating a combinatorial auction with three forms of competing utility:

1. **Blockspace**
2. **Speed-of-Inclusion** 
3. **Collusion Goods**

Users express their preferences for all three by manipulating two levers:

1. **Bid Distribution:** how the bid is broadcast into the network affects the degree of competition to collect it, which affects the marginal profitability of servicing the transaction and the forms of utility delivered in exchange.

2. **Bid Amount:** increasing the fee increases the speed of transaction inclusion regardless of the distribution strategy selected, as higher fees trigger faster block production.

Manipulating these levers allow users to reveal their ordinal preferences across multiple dimensions. 

The mechanism works because users who dictate any two forms of utility must let the third be set by the most efficient producer. Less efficient producers can only out-compete this producer by emulating their efficiency at delivering value to users, which requires spending their own money to subsidize production of the forms of utility favoured by honest users.

User preferences (amount demanded) are revealed by the trade-offs users accept across the three dimensions, while producer preferences (cost-of-supply) are revealed by their willingness to spend their own money to outcompete their peers.

The mechanism qualifies as an indirect mechanism with truthful preference revelation in the tradition of Hurwicz and Maskin. It meets the criteria Hurwicz and Jordan established for iterative convergence on pareto optimality. And -- presuming one accepts the existence of multiple competing auctioneers as a valid auction design -- it is an economically efficient combinatorial auction.

