---
title: majoritarian-attacks
description: 
published: true
date: 2025-05-21T11:29:47.849Z
tags: 
editor: markdown
dateCreated: 2023-09-20T01:58:02.086Z
---

# Eliminating 51% Attacks

The most common reason people consider the 51% attack impossible to solve is that well-known academic papers claim the problem is unsolvable. The most general way to see how Saito Consensus solves the problem is taking these papers seriously and realizing why they do not apply.

- See our [technical overview](/consensus) of Saito Consensus

- For a complete mathematical proof [see here](https://wiki.saito.io/consensus/math)

- Official Blog [post](https://saito.tech/eliminating-51-attacks-in-proof-of-work-blockchains/) on the same subject

As such, while the three links above explanation how the soluiton works, in this section we review the two major classes of impossibility proofs that are used to argue that the problems Saito Consensus solves are unsolvable. Our goal is to show you the informational limitations of these results and why they do not apply to routing work mechanisms.

<br>

### 1. Bracha and Toueg (1985)

The paper *Asynchronous Consensus and Broadcast Protocols* by Bracha and Toueg (1985) is the most widely-cited proof that probabilistic protocols with **n** total participants can tolerate at most **(n-1)/2** malicious participants.

Bracha and Toueg conceptualize consensus mechanisms as consisting of *processes* which behave honestly or maliciously. The foundation of their claim is that in permissionless mechanisms byzantine processes can do anything honest processes can do. If malicious nodes wish to prevent the network from achieving consensus, they need merely to propose the same number of "atomic steps" as the honest minority is proposing, stalemating consensus by preventing it from resolving on any particular outcome.

> In an atomic step of the system, a process can try to receive a message, perform an arbitrarily long local computation, and then send a finite set of messages. The computation and the messages sent are prescribed by the protocol, that is, a function of the message received and the local state.

The problem with Bracha and Toueg is that their model of the network consists of *processes*, which leads them into assuming that all nodes can perform the same actions for the same cost at all times. Missing from their view of the network is the need for resource expenditure in taking an atomic step. They assume malicious nodes can simulate the behavior of honest nodes without penalty. And they assume there is no economic or cryptographic mechanism to penalize processes sharing a malicious message over an honest one. 

This assumption -- symmetrically costless participation -- was reasonable in the 1980s when consensus mechanisms did not manage economic assets and could not force nodes to burn tokens for proposing malicious state transitions.  It remained reasonable in the face of proof-of-work and proof-of-stake mechanisms because those mechanisms cannot impose penalities on malicious majorities. The assumption collapses in the face of Saito Consensus, because routing work charges nodes more to propose economically-inefficient state transitions, and attackers are forced to propose economically-inefficient transitions in order to orphan honest blocks.

As a result, the assumption Bracha and Toueg make that all *processes* face the same cost structure does not apply to Saito Consensus. Honest nodes run the network using other people's money. Their costs of producing blocks are lower than those of attackers, and because they never include their own fees in blocks they never need reduce their share of the overall network. But attackers necessarily force themselves out majority control of network resources if they continue to orphan honest blocks. The network is capable of reducing 

<br>

### 2. Dwork, Lynch, and Stockmeyer (1988)

A second but related series of impossibility results come from *Consensus in the presence of Partial Synchrony* by Dwork, Lynch, and Stockmeyer (1988). These authors note that when a system is partitioned in ways where block production resources are distributed in an equally balanced fashion, deterministic consensus can't be achieved.

The first problem with this approach is its assumption that block production capacity can be split evenly — but in routing work systems, this would require total control over how ever participant in the network creates transactions and sends messages. Such coordination is at minimum incompatible with informational decentralization. Nor is it reasonably to assert control of 100% of network participants in order to pull off an attack that claims control over a mere majority.

To avoid this problem we can imagine a situation where an attacker privately controls 50% of pre-attack fee-flow and is merely moving their own resources to a private chain. In this case the attacker only controls the 50% of the resources needed to produce blocks and their attack is essentially denying those fees to the honest chain and spending them on a private fork. Does this attack compromise Saito Consensus?

Fortunately not, for while it is theoretically possible for an attacker who controls exactly 50% of first-hop fee-flow to move their fee-flow to a private network, doing so is economically irrational in Saito Consensus. For the attacker, who was previously spending 50% of their own fees on producing golden tickets to unlocking routing payouts, is now spending 100% of their  fees-in-block to do the same. Even if an attacker could pull off such an attack they would not increase their revenue but merely raise their cost of getting paid.

The consensus mechanism continues to work exactly as promised -- imposing a quantifiable cost-of-attack on nodes which engage in the byzantine behavior of censoring honest transactions or orphaning honest blocks from the collective chain.


## How Saito Eliminates 51% Attacks

The essence of eliminating 51% attacks is a technique for increasing the cost of orphaning a block above the cost of .

In the inner auction

Saito Consensus achieves this as honest nodes make blocks entirely with fees collected from other users. Attackers are forced to spend their own money.

In equilibrium, spending their own money to produce blocks results in attackers . 


### Golden Ticket

### Conclusion

The preservation of work, work which is independent of blocks, is not possible in PoW or PoS, and is how Saito eliminates 51% attacks.

Since the amount of work the honest network accumulates can only grow the longer they are censored, the amount of work the attacker must produce to keep censoring them also grows without bound, no matter if the attacker has 51% of inbound fees or 99%.

Even if the attacker owns 100% of inbound fees, as soon as they begin abusing users, new routing nodes are free to enter the network and begin taking market share and interrupting the majority fork. The ability for recovery from 100% attacks is not possible in any other blockchain.


