---
title: Sybil Attacks
description: 
published: true
date: 2025-11-25T03:38:06.190Z
tags: 
editor: markdown
dateCreated: 2023-09-12T04:54:16.592Z
---

# Sybil Attacks

Sybil attacks are one of the core economic challenges in decentralized systems. In 2011, Babaioff, Dobzinski, Oren, and Zohar formalized this in their paper "On Bitcoin and Red Balloons", which claimed to prove that no reward scheme can simultaneously incentivize information propagation while also detering self-cloning. This result has since been widely interpreted as offering a fundamental limitation on incentive design.

Saito Consensus breaks this limitation. It is the first known consensus mechanism that is provably sybil-proof, with these properties formally established in the paper [*A Simple Proof of Sybil Proof.*](https://github.com/SaitoTech/papers/blob/main/sybil/A_Simple_Proof_of_Sybil_Proof_Lancashire-Parris_2023.pdf).

The purpose of this page is to explain -- in non-technical terms -- what the Red Balloons impossibility result is and why it does not apply to Saito-class routing mechanisms. Following that, we explain why the solution Saito offers to this specific routing problem generalizes to provide protection against other attacks associated with cheap identity creation in permissionless mechanisms.


## An Impossible Problem? 

> Many large decentralized systems rely on information propagation to ensure their proper function... [we show] that there are no reward schemes in which information propagation and no self-cloning is a dominant strategy.
<br>-*Moshe Babaioff, Microsoft Research*

A major economic problem in blockchains is that nodes in possession of fee-bearing transactions do not have an incentive to share these transactions with their peers. Why share transactions with potential competitors? Increasing the number of people with the ability to put a transaction into a block is irrational for those with access if it lowers their own chance of collecting the fee.

This problem is solvable if we pay nodes to share. But adding any such a payout creates a separate problem: once routing nodes are paid for forwarding transactions to others, what is stopping them from adding "fake" routing hops to increase their share of the routing path and increase their chance of winning any routing payout?

This is the problem Moshe Babaioff and his colleagues examine in their paper *[On Bitcoin and Red Ballons](https://arxiv.org/abs/1111.2626)*. And not surprisingly, the authors conclude that no reward scheme exists that can make “honestly forwarding” transactions a dominant strategy while simultaneously discouraging "self-cloning". Once you pay nodes to share, Moshe reasons, you must also incentivize them to use fake identities. The incentive to propagate must create an incentive to sybil.

## A Groundbreaking Solution

While the Red Balloons paper is frequently cited in blockchain circles as demonstrating the infeasibility of creating a fair routing payment, what typically goes unnoticed is that the claims of these authors only hold under the specific assumptions they make when framing the problem. Specifically, the authors assume:

- all nodes have equal probability of proposing the next block**
- all nodes have the same cost of proposing the next block**
- routing decisions do not affect leader selection or cost
- all routing payouts induce zero-sum conflict over a routing path**

Under these assumptions it is true that forwarding a transaction can only ever decrease the income of the node that shares, but it is not true that these assumptions hold for all distributed consensus mechanisms capable of issuing routing payments.

## How Saito Addresses Sybilling

Saito Consensus is the first consensus mechanism that solves the Red Balloons problem from first principles in a permissionless setting. It achieves this by penalizing the economic inefficiency associated with the addition of sybil hops to routing paths. Specficially, nodes that add unnecessary hops to transactions increase their cost of producing blocks faster than they increase their expected income from the expanded claims that they create on the routing payout. Sybilling remains technically possible, but becomes strictly irrational.

The [mathematical paper](https://github.com/SaitoTech/papers/blob/main/sybil/A_Simple_Proof_of_Sybil_Proof_Lancashire-Parris_2023.pdf) linked above provides a rigorous proof of this. It demonstrates that the expected income from the payout lottery *falls* for all nodes that add an unnecessary hop to a routing path. The solution is possible because Saito Consensus does not work the way *Babaioff* and his colleagues assume blockchains must work.

Specifically, Saito breaks the assumption that all nodes have the same probability of producing the next block. This assumption is true in proof-of-work and proof-of-stake mechanisms. But it does not hold in Saito Consensus as cost of producing a block depends on the efficiency of the routing paths the block producer is leveraging to produce the block. If two competing nodes have access to the same set of transactions the one with the more efficiently-routed set will produce a block faster and more cheaply than its competitor.

The assumption that nodes on a routing path face zero-sum conflict for collection of the fee also does not apply in Saito Consensus, where conflict over fee-collection is between *competing* routing paths rather than nodes on the same path. Within a routing path, the efficient sharing of transactions is mutually beneficial for all nodes in a routing path as it increases their chance of producing blocks and receiving payment relative to other nodes elsewhere in the network.

These two assumptions: (1) all nodes face the same probability and cost of producing blocks, (2) nodes on a routing path face zero-sum conflict over fee collection, are the ultimately source of its impossibility claims. Yet neither of these assumptions apply to routing work mechanisms, and Saito Consensus in particular shows that solutions exist which are not trapped by their impossibility results.

## A General Solution

While Saito Consensus solves the very specific problem in the Babaioff paper. It also offers a more general solution to sybil attack generally. To understand how, consider [Wikipedia](https://en.wikipedia.org/wiki/Sybil_attack)'s definition of a sybil attack as "a type of attack on a computer network in which an attacker subverts the service's reputation system by creating a large number of pseudonymous identities and uses them to gain a disproportionately large influence."

Understood properly, this points to Saito offering a general solution to sybil-attacks that manifest in other domains as well. And the reason for this is that, in Saito, identity inflation also results in an increase in the measured inefficiency of the network and forces an inefficient money-burn on the nodes responsible for the inefficiency.

The key innovation in Saito Consensus is that **block-production cost depends on routing-path efficiency**. Routing paths embedded into transactions encode how efficiently the network is collecting tokens, and submits those tokens into a payout lottery that requires burning a substantial amount of the fees collected. As such, adding fake identities to those paths:

- increases the length of the path,  
- slows block production,  
- raises the cost of producing a block, and  
- raises the cost of collecting other people's money

Crucially, if the attacker controls *all* the sybil identities, the harm falls entirely on the attacker themselves. This is why the formal proof in *A Simple Proof of Sybil Proof* (Lancashire & Parris, 2023) shows:

> **The expected routing payout strictly decreases for any node that inserts an unnecessary hop.**


### Why this generalizes far beyond routing

Saito’s protection against sybilling does not depend on the specific structure of the routing payout, but emerges from the structural economics of how the network quantifies the value contributed by nodes and encourages only economically-productive forms of cooperation.

And this general principle holds across attack surfaces:

- **Operating many block-producers**  
  - Splits access to transaction flow and forces unncessary cross-node transfers, making each identity less competitive at block production.

- **Creating many routing identities**  
  - Lengthens routing paths and increases burn cost faster than it increases expected reward.

- **Adding "fake transactions" to blocks**
  - Imitates a real user, but subjects the imitator to the costs a real user would face in the mechanism, namely the unrecoveralb eburning of a portion of their fee.

Essentially, Saito offers a generalizable solution to sybil-attacks because **income-earning power is tied to efficient economic behavior** not identity count. And the requirement for distinct identities to communicate to cooperate/collude subjects those nodes to the implicit tax the network assigns to work-transfers across routing networks.

### Sybilling becomes a strictly dominated strategy

In Saito, every sybil attacks shares a common property:

> **It makes the attacker strictly worse off than following the protocol.**

This is stronger than merely preventing one particular routing-path attack. It ensures that:

- honest participation is always profit-maximizing,  
- sybilling is always profit-decreasing,  
- and cooperative sharing of transactions is strategically stable.

This positions Saito as the first consensus mechanism in which **sybilling is irrational in the general mechanism-design sense**, not just prohibited by ad-hoc rules.
