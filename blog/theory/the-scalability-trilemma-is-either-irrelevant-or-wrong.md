---
title: The Scalability Trilemma is Either Irrelevant or Wrong: Here is Why
description: 
published: true
date: 2024-11-30T09:14:35.615Z
tags: 
editor: markdown
dateCreated: 2024-11-30T09:14:35.615Z
---

# The Scalability Trilemma is Either Irrelevant or Wrong: Here is Why

![the-scalability-trilemma.webp](/blog/the-scalability-trilemma.webp)

*Written by David Lancashire on May 10, 2021*

As proposed by Vitalik Buterin, the scalability trilemma asserts that it is impossible to increase decentralization, scale, or security in a blockchain without decreasing at least one of the other two.

Vitalik’s proposition is self-evident in the sense that increasing scale requires concentrating expenditure and increasing decentralization requires spreading it out. So the only way you can increase both simultaneously is by finding an external source of funds—defunding your security mechanism. But does this actually say anything meaningful about blockchain security?

Saito shows that it does not, as in a Saito-class blockchain, the network gets security from the division of funds across the routing network. So the routing network can reconfigure into topologies that don’t affect scalability but simultaneously increase both the cost-of-attack on the network as well as its decentralization.

For a very trivial example, picture a Saito network with two nodes. Node-A collects 80 percent of fees and produces 80 percent of blocks. Node-B collects 20 percent of fees and produces 20 percent of blocks. These nodes have a cost-of-attack on the network inverse to their share of fee-flow.

It is trivial to see that users in this network could shift 20 percent of their transaction flow away from Node-A and to a new node: Node-C. The distribution of block production is now 60-20-20. The cost-of-attack on the network has increased. The network is more decentralized. But scalability is unaffected.

Or is it? And while there may be some objections that I suppose someone might make, note that they require removing “security” from the discussion and retreating to a “scale-vs-decentralization” dilemma that has nothing to do with security and thus nothing particularly interesting or meaningful to say about it.

*Written by David Lancashire*
