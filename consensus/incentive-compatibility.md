---
title: Saito Consensus and Incentive Compatibility
description: 
published: true
date: 2025-04-07T19:21:22.503Z
tags: 
editor: markdown
dateCreated: 2025-04-07T19:21:22.502Z
---

# Incentive Compatibility

Saito Consensus appears to be the first known distributed consensus mechanism that is incentive compatible with the social choice rule of pareto optimality. It does this by creating a combinatorial auction in which users bid for three forms of utility:

1. blockspace
2. speed-of-inclusion
3. collusion goods

Users express their preferences for these goods by manipulating two levers:

1. Distribution Strategy: affects what percent of the bid induces competitive provision
2. Fee Strategy: determines the total amount of utility purchased
Thse two levers allow users to reveal their ordinal preferences across three dimensions, as competition between producers pushes price levels into optimality. For example:

* Users who maximally value fast inclusion can purchase next-block inclusion, but get zero collusion goods.
* Users who maximally value collusion goods get slowest transaction inclusion ceteris paribus
* Users target fractional combinations through the strategic distribution of fractional bids

User preferences are revealed by the trade-offs users accept across the three dimensions. This qualifies the system as an indirect mechanism in the tradition of Hurwicz and Maskin. It meeets the criteria for truthful preference revelation and incentive compatibility. And also the criteria Hurwicz and Jordan establish for iterative algorithms which converge on pareto optimal outcomes.

Your content here