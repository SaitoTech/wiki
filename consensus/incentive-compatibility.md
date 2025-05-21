---
title: Saito Consensus and Incentive Compatibility
description: 
published: true
date: 2025-05-21T12:56:28.752Z
tags: 
editor: markdown
dateCreated: 2025-04-07T19:21:22.502Z
---

# Incentive Compatibility

Saito Consensus is the first distributed consensus mechanism believed to be incentive compatible with the social choice rule of pareto optimality in conditions of informational decentralization. It does this by creating a combinatorial auction that forces trade-offs to hit the production and consumption of contending forms of utility simultaneously:

1. **Blockspace**
2. **Speed-of-Inclusion** 
3. **Collusion Goods** (off-chain utility)

Rational users truthfully reveal their private valuations for the utility of all three goods by manipulating two strategic levers: the value of the bid (the transaction fee paid), and distribution strategy (how the bid is broadcast into the network).

Rational producers truthfully reveal their competitive advantage at collecting transaction fees and selling collusion goods through the strategy of including their own fees in blocks, an act which -- uniquely in Saito Consensus mechanism -- increases the efficiency of the overall economic system.

The mechanism achieves incentive compatibility because users who dictate any two forms of utility must let the third be set at market rates by the most efficient provider of that form of value. This process iterates towards optimality over time as the mechanism incentivizes producers to drive the network into a state of maximal fee-throughput by advantaging those who are most efficient at proposing such transitions in both the production of blocks and collection of payments.

In the language of implementatino theory, routing work mechanisms are indirect mechanism with truthful preference revelation in the tradition of Hurwicz and Maskin. They meet the criteria Hurwicz and Jordan establish for iteratively converging on pareto optimality equilibria -- only uniquely as they lack the need for a trusted third-party to run the mechanism.

