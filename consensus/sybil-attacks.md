---
title: Sybil Attacks
description: 
published: true
date: 2025-05-21T09:06:14.176Z
tags: 
editor: markdown
dateCreated: 2023-09-12T04:54:16.592Z
---

# Sybil Attacks

Saito Consensus is the first consensus mechanism that is known to be sybil-proof. A mathematical proof of this claim is available in the paper [*A Simple Proof of Sybil Proof.*](https://github.com/SaitoTech/papers/blob/main/sybil/A_Simple_Proof_of_Sybil_Proof_Lancashire-Parris_2023.pdf). Since the economic problem this solves is non-obvious, this page provides a non-technical introduction to what the sybil problem is and how Saito Consensus solves it.

## An Impossible Problem?

> Many large decentralized systems rely on information propagation to ensure their
proper function... [we show] that there are no reward schemes in which information
propagation and no self-cloning is a dominant strategy.
<br>-Moshe Babaioff, Microsoft Research

A major economic problem in blockchains is that nodes in possession of fee-bearing transactions do not have an incentive to share these transactions with their peers. Why share transactions with potential competitors? Increasing the number of people with the ability to put a transaction into a block is irrational if it lowers your own chance of collecting the fee.

This problem is solvable if we pay nodes to share. But adding such a payout creates a separate problem: once routing nodes get paid for sending transactions to block producers, what is stopping these nodes from adding fake routing hops to transactions to increase their share of the routing path and increase their chance of winning the routing payout?

This is the problem Moshe Babaioff and his colleagues examined in their paper *[On Bitcoin and Red Ballons](https://arxiv.org/abs/1111.2626)* and concluded was impossible to solve, arguing that there are no reward schemes that can incentivize *information propagation* that do not also incentivize *self-cloning*. If you pay nodes to share, Moshe reasons, you must also incentivize them to route their transactions through fake identities to maximize their chance of winning any routing payout.

## A Groundbreaking Solution

Saito Consensus is the first consensus mechanism that solves this problem. It achieves this by penalizing the economic inefficiency associated with sybil hops. Nodes that add unnecessary routing hops to transactions increase their cost of producing blocks much faster than they increase their expected income from the routing payout. Sybilling remains theoretically possible, but becomes strictly irrational.

The [mathematical paper](https://github.com/SaitoTech/papers/blob/main/sybil/A_Simple_Proof_of_Sybil_Proof_Lancashire-Parris_2023.pdf) linked above provides a rigorous proof of this. It demonstrates that the expected income from the payout lottery *falls* for all nodes that add an unnecessary hop to a routing path. The solution is possible because Saito Consensus does not work the way *Babaioff* and his colleagues assume blockchains must work. Specifically, *Babaioff* makes two critical assumptions about how blockchains work that do not apply to Saito Consensus.

The first assumption *On Bitcoin and Red Balloons* makes is that all consensus mechanisms must allow all nodes the same cost for proposing blocks. This assumption is true in proof-of-work and proof-of-stake mechanisms. It breaks in Saito Consensus as cost of producing a block depends on the efficiency of the routing paths the block producer is proposing to include in the block. If two competing nodes have the same set of transactions the one with the more efficiently-routed set will produce a block faster and more cheaply than its competitor.

*On Bitcoin and Red Balloons* also assumes that incentivizing propagation is impossible because sharing transactions makes it less likely for the sharer to collect payment at all. But in Saito Consensus the block producer is not the only node eligible for payout. It is possible to induce sharing between node as long as the nodes on the routing path do not face a zero-sum conflict over collection of the fee. And routing work accomplishes this because sharing shifts income to the sharing nodes from the nodes on competing routing paths that hoard.

These two assumptions: (1) all nodes face the same cost of producing blocks, (2) nodes on a routing path face zero-sum conflict over fee collection are buried in the *On Bitcoin and Red Balloons* paper where they are accepted uncritically in part because they describe how the Bitcoin network functions. Yet neither of these assumptions apply to routing work mechanisms, and the difference allows the creation of an informationally decentralized payment mechanism that is not subject to this sybil attack.

## A General Solution

While Saito Consensus solves the very specific problem in the Babaioff piece. It also offers a more general solution to sybil attack generally, defined as per [Wikipedia](https://en.wikipedia.org/wiki/Sybil_attack) as "a type of attack on a computer network in which an attacker subverts the service's reputation system by creating a large number of pseudonymous identities and uses them to gain a disproportionately large influence."

The reason for this is that all sybil attacks involve an attacker exploiting a pseudoanonymous identity to increase their expected claims-on-payout. In Saito Consensus this is generally irrational because the routing paths that are embedded within transactions are a measure of the efficiency of the network itself. Using additional identities requires producers to add additional routing hops when transferring work between them, which reduces the efficiency of the mechanism. If one is going to attack the mechanism it is much better to do it directly! And that is punished through a different mechanism.

Put most plainly, with Saito Consensus nodes can *try* to sybil, but since the mechanism is only profitable for nodes that use other people's money, all sybilling does is reduce their competitiveness and increases costs faster than income. Sybilling becomes a strictly dominated strategy.

## Conclusion

Saito Consensus offers a significant advance in distributed consensus. But you don't need to take our word for it -- we encourage all readers to dig into the mathematical paper above and see for yourself how cryptographic routing signatures can be used to universally punish the inefficiencies created by the presence of sybils in transaction routing paths.
