---
title: Sybil Attacks
description: 
published: true
date: 2025-05-21T07:56:19.294Z
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

A major economic problem in blockchains is that nodes in possession of fee-bearing transactions do not have an incentive to share those transactions with their peers. Why share transactions with potential competitors? Increasing the number of people with the ability to put a transaction into a block only lowers your own chance of collecting the fee.

This problem is solvable if we have a way of paying nodes to share. But adding such a payout seems to create a different problem: how can we reward nodes for sharing transactions without encouraging them to add fake routing hops and increase their chance of payout? And if you can sybil a routing path and increase your chance of getting paid, my rational response flips again into not sharing.

This is the problem Moshe Babaioff and his colleagues examined in their paper *[On Bitcoin and Red Ballons](https://arxiv.org/abs/1111.2626)* and concluded was impossible to solve, arguing that there are no reward schemes that can incentivize *information propagation* that do not also incentivize *self-cloning*. If you incentivize nodes to share, Moshe argues, you must also incentivize them to route their transactions through fake identities in order to maximize their chance of winning any routing payout.

## A Groundbreaking Solution

Saito Consensus is the first consensus mechanism that solves this problem. It achieves this by penalizing the economic inefficiency associated with sybil attacks. Nodes that add fake sybil hops increase their cost of producing blocks much faster than they increase their expected gains from doing so. Sybilling remains theoretically possible, but becomes strictly irrational.

The [mathematical paper](https://github.com/SaitoTech/papers/blob/main/sybil/A_Simple_Proof_of_Sybil_Proof_Lancashire-Parris_2023.pdf) linked above provides a rigorous proof of this. It demonstrates that the expected income from the payout lottery actually *falls* for all nodes that add a sybil path (route a transaction to themselves). Because the proof is self-evident at the first-hop position (a first-hop node that sybils itself doubles its the cost of block production without increasing expected income in the lottery), the proof examines the incentives facing a second-hop node.

With this in mind, it's often worth just pointing out exactly what *Babaioff* and his colleagues missed: what two critical assumptions they make about how blockchains must work that do not apply to Saito Consensus and thus permit routing mechanisms to skirt their impossibility claims.

The first assumption *On Bitcoin and Red Balloons* makes is that all nodes must face the same cost of producing blocks. This assumption is true in proof-of-work mechanisms. And it is true in proof-of-stake mechanisms. It has been accepted in computer science research since the 1980s. But it is not true in Saito Consensus, where the cost of producing blocks differs for different nodes based on the value of the transactions in their mempools and the compactness of the routing paths inside those transactions.

Routing work mechanisms make it less expensive for nodes to produce blocks if they propose to do so with transactions with compact routing paths. What the math in the paper shows is that adding fake routing hops to a transaction decreases the efficiency of the routing paths inside the proposed block and thus makes it more expensive to produce a block. The maths in this paper demonstrate unambiguously that these costs imposed by adding superfluous routing hops always increase faster than the benefits they offer. Sybilling gets nodes a greater chance of getting paid, but requires them to spend more to increase their odds than those extra odds are worth.

But can we also incentivize propagation? *On Bitcoin and Red Balloons* assumes this is impossible because sharing transactions in other mechanisms make it less likely for the sharer to produce a block and get paid. But in Saito Consensus sharing increases the chance of the recipient producing a block. And because the sender is eligible to collect payment from that block, it is beneficial to share as long as sharing increases rather than decreases your expected income. Routing work accomplishes this because sharing shifts income away from the nodes on routing paths that hoard and towards nodes on routing paths that share.

Sharing becomes the default equilibrium because not sharing makes nodes much more likely to be outcompeted by their competitors on routing paths that share. The mechanism essentially creates a reversed collective action problem where sharing is the most profitable strategy.

These two assumptions (all nodes face the same cost of producing blocks, sharing cannot speed up block production) are buried in the *On Bitcoin and Red Balloons* paper where they are accepted uncritically in part because they describe how the Bitcoin network functions. Yet neither of these assumptions apply to routing work mechanisms, and the difference allows the creation of an informationally decentralized payment mechanism that is not subject to this sybil attack.

## A General Solution

While Saito Consensus solves the very specific problem in the Babaioff piece. It also offers a more general solution to sybil attack generally, defined as per [Wikipedia](https://en.wikipedia.org/wiki/Sybil_attack) as "a type of attack on a computer network in which an attacker subverts the service's reputation system by creating a large number of pseudonymous identities and uses them to gain a disproportionately large influence."

The reason for this is that all sybil attacks involve an attacker exploiting a pseudoanonymous identity to increase their expected claims-on-payout. In Saito Consensus this is generally irrational because the routing paths that are embedded within transactions are a measure of the efficiency of the network itself. Using additional identities requires producers to add additional routing hops when transferring work between them, which reduces the efficiency of the mechanism. If one is going to attack the mechanism it is much better to do it directly! And that is punished through a different mechanism.

Put most plainly, with Saito Consensus nodes can *try* to sybil, but since the mechanism is only profitable for nodes that use other people's money, all sybilling does is reduce their competitiveness and increases costs faster than income. Sybilling becomes a strictly dominated strategy.

## Conclusion

Saito Consensus offers a significant advance in distributed consensus. But don't take our word for it -- we encourage all readers to dig into the informational problems described on this page and work through how to address them using routing signatures.

