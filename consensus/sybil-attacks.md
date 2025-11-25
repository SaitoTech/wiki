---
title: Sybil Attacks
description: 
published: true
date: 2025-11-25T02:53:59.773Z
tags: 
editor: markdown
dateCreated: 2023-09-12T04:54:16.592Z
---

# Sybil Attacks

Sybil attacks are one of the core economic challenges in decentralized systems. In 2011, Babaioff, Dobzinski, Oren, and Zohar formalized this in their paper "On Bitcoin and Red Balloons", which claimed to prove that no reward scheme can simultaneously incentivize information propagation while also detering self-cloning. This result has since been widely interpreted as offering a fundamental limitation on incentive design.

Saito Consensus breaks this limitation. It is the first known consensus mechanism that is provably sybil-proof, with these properties formally established in the paper [*A Simple Proof of Sybil Proof.*](https://github.com/SaitoTech/papers/blob/main/sybil/A_Simple_Proof_of_Sybil_Proof_Lancashire-Parris_2023.pdf).

The purpose of this page is to explain -- in non-technical terms -- what the Red Balloons impossibility result is and why it does not apply to Saito-class routing mechanisms. Following that, we explain why the solution Saito offers to this specific routing problem generalizes to provide protection against other attacks associated with cheap identity creation in permissionless mechanisms.



## An Impossible Problem?

> Many large decentralized systems rely on information propagation to ensure their
proper function... [we show] that there are no reward schemes in which information
propagation and no self-cloning is a dominant strategy.
<br>-Moshe Babaioff, Microsoft Research

A major economic problem in blockchains is that nodes in possession of fee-bearing transactions do not have an incentive to share these transactions with their peers. Why share transactions with potential competitors? Increasing the number of people with the ability to put a transaction into a block is irrational if it lowers your own chance of collecting the fee.

This problem is solvable if we pay nodes to share. But adding such a payout creates a separate problem: once routing nodes get paid for sending transactions to block producers, what is stopping these nodes from adding fake routing hops to transactions to increase their share of the routing path and increase their chance of winning the routing payout?

This is the problem Moshe Babaioff and his colleagues examined in their paper *[On Bitcoin and Red Ballons](https://arxiv.org/abs/1111.2626)* and concluded was impossible to solve, arguing that there are no reward schemes that can incentivize *information propagation* that do not also incentivize *self-cloning*. If you pay nodes to share, Moshe reasons, you must also incentivize them to route their transactions through fake identities to maximize their chance of winning any routing payout.

## A Groundbreaking Solution

Saito Consensus is the first consensus mechanism that solves this problem. It achieves this by penalizing the economic inefficiency associated with sybil hops. Nodes that add unnecessary routing hops to transactions increase their cost of producing blocks faster than they increase their expected income from the expanded claims on the routing payout. Sybilling remains technically possible, but becomes strictly irrational.

The [mathematical paper](https://github.com/SaitoTech/papers/blob/main/sybil/A_Simple_Proof_of_Sybil_Proof_Lancashire-Parris_2023.pdf) linked above provides a rigorous proof of this. It demonstrates that the expected income from the payout lottery *falls* for all nodes that add an unnecessary hop to a routing path. The solution is possible because Saito Consensus does not work the way *Babaioff* and his colleagues assume blockchains must work. Specifically, *Babaioff* makes two critical assumptions about how blockchains work that do not apply to Saito Consensus.

The first assumption *On Bitcoin and Red Balloons* makes is that consensus mechanisms must afford all nodes the same cost for proposing blocks. This assumption is true in proof-of-work and proof-of-stake mechanisms. But it breaks in Saito Consensus as cost of producing a block depends on the efficiency of the routing paths the block producer is proposing to include in the block. If two competing nodes have the same set of transactions the one with the more efficiently-routed set will produce a block faster and more cheaply than its competitor.

*On Bitcoin and Red Balloons* also assumes that nodes on a routing path face a zero-sum conflict for collection of the fee. But in Saito Consensus the nodes on any routing path do not face a zero-sum conflict to collect the fee. They are engaged in a zero-sum conflict with nodes on competing routing paths. The cooperative and efficient sharing of transaction flows is mutually beneficial as it benefits nodes which share while penalizing those which hoard. This reverses the collective action problem which makes the .

These two assumptions: (1) all nodes face the same cost of producing blocks, (2) nodes on a routing path face zero-sum conflict over fee collection are buried in the *On Bitcoin and Red Balloons* paper but are the source of its impossibility claims. They are accepted uncritically in part because they describe how the Bitcoin network functions. Yet neither of these assumptions apply to routing work mechanisms, and the trade-offs they force on other networks vanish in informationally decentralized payment mechanisms that are not subject to this specific problem.

## A General Solution

While Saito Consensus solves the very specific problem in the Babaioff paper. It also offers a more general solution to sybil attack generally. To understand how, consider [Wikipedia](https://en.wikipedia.org/wiki/Sybil_attack)'s definition of a sybil attack as "a type of attack on a computer network in which an attacker subverts the service's reputation system by creating a large number of pseudonymous identities and uses them to gain a disproportionately large influence."

All sybil attacks involve attackers who use pseudoanonymous identities to increase their expected incomes. In Saito Consensus this becomes generally irrational because the routing paths that are embedded within transactions are a measure of the efficiency with which the network is burning money. Faking this metric using pseudoanonymous identities is only possible those identities are willing to burn money. But since both identities are controlled by the attacker this implies that the attacker must be irrational.

Put most plainly, with Saito Consensus nodes can *try* to sybil, but doing so increases the costs of producing blocks and lowers the expected profitability of doing so in ways that make sybilling far more costly than following protocol rules and sharing unconfirmed transactions efficiently with other nodes on the network. Sybilling becomes a strictly dominated strategy.

## Conclusion

Saito Consensus offers a significant advance in distributed consensus. But you don't need to take our word for it -- we encourage all readers to dig into the mathematical paper above and see for yourself how cryptographic routing signatures can be used to universally punish the inefficiencies created by the presence of sybils in transaction routing paths.
