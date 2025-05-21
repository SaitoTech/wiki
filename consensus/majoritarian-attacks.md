---
title: majoritarian-attacks
description: 
published: true
date: 2025-05-21T12:06:10.589Z
tags: 
editor: markdown
dateCreated: 2023-09-20T01:58:02.086Z
---

# Eliminating 51% Attacks

Many people believe that the 51% attack is fundamentally unsolvable. This belief stems from widely cited academic papers that claim it is mathematically impossible to build consensus systems that majoritarian attacks. Saito Consensus proves otherwise.

- See our [technical overview](/consensus) of Saito Consensus

- For a complete mathematical proof [see here](https://wiki.saito.io/consensus/math)

Given the technical explanations of how Saito Consensus works available at the links above, this page focuses on two of the most influential impossibility results in distributed systems: *Bracha and Toueg* (1985) and *Dwork, Lynch, and Stockmeyer* (1988). These papers form the intellectual foundation for claims that majority attacks are unsolvable. We'll show why these results do not apply to routing work mechanisms like Saito.

<br>

### 1. Bracha and Toueg (1985)

The paper *Asynchronous Consensus and Broadcast Protocols* by Bracha and Toueg is one of the most influential results in distributed consensus. It shows that in an asynchronous system with **n** total processes, at most **(n−1)/2** can be byzantine for honest nodes to be able to eventually reach consensus.

Notably, the model Bracha and Toueg adopt assume that the network is made up of processes that can be either honest or byzantine, and that byzantine processes can do anything honest processes can, including responding to inbound messages by broadcasting outbound ones:

> In an atomic step of the system, a process can try to receive a message, perform an arbitrarily long local computation, and then send a finite set of messages. The computation and the messages sent are prescribed by the protocol, that is, a function of the message received and the local state.

This leads to the critical error: the assumption that all messages must cost all processes the same amount to broadcast. If this assumption is true Bracha and Toueg are correct -- a malicious majority can indefinitely stalemate an honest minority by proposing blocks or state transitions which block them arriving at consensus.

That assumption was appropriate in the 1980s, before consensus systems managed valuable in-network tokens and could charge participants money for proposing state transitions. It remains appropriate for proof-of-work and proof-of-stake systems, because those mechanisms cannot penalize malicious majorities. But Saito Consensus breaks this symmetry.

Whereas Bracha and Toueg assume all nodes are *processes* which can perform the same actions for the same cost, routing work mechanisms requires nodes to burn different amounts in fees to propose blocks, and refunds them a different amount of the fees-collected based on their efficiency in collecting those fees.

As a result, the assumption Bracha and Toueg make simply does not apply to Saito Consensus. Malicious nodes can extend the chain, but because they are less efficient than an honest node by definition for whatever subset of blocks they are orphaning, they must contribute and burn their own money in any attack on those nodes. This reduces their share of the in-network resource over time, pulling even a malicious majority back into minority status.

<br>

### 2. Dwork, Lynch, and Stockmeyer (1988)

A second but related series of impossibility results come from *Consensus in the presence of Partial Synchrony* by Dwork, Lynch, and Stockmeyer (1988). These authors note that when a system is partitioned in ways where block production resources are distributed in an equally balanced fashion, deterministic consensus can't be achieved.

The first problem with this approach is its assumption that block production capacity can be split evenly — but in routing work systems, this would require total control over how ever participant in the network creates transactions and sends messages. Such coordination is at minimum incompatible with informational decentralization. Nor is it reasonably to assert control of 100% of network participants in order to pull off an attack that claims control over a mere majority.

To avoid this problem we can imagine a situation where an attacker privately controls 50% of pre-attack fee-flow and is merely moving their own resources to a private chain. In this case the attacker only controls the 50% of the resources needed to produce blocks and their attack is essentially denying those fees to the honest chain and spending them on a private fork. Does this attack compromise Saito Consensus?

Fortunately not, for while it is theoretically possible for an attacker who controls exactly 50% of first-hop fee-flow to move their fee-flow to a private network, doing so is economically irrational in Saito Consensus. For the attacker, who was previously spending 50% of their own fees on producing golden tickets to unlocking routing payouts, is now spending 100% of their  fees-in-block to do the same. Even if an attacker could pull off such an attack they would not increase their revenue but merely raise their cost of getting paid.

The consensus mechanism continues to work exactly as promised -- imposing a quantifiable cost-of-attack on nodes which engage in the byzantine behavior of censoring honest transactions or orphaning honest blocks from the collective chain.


### Conclusion

Saito Consensus creates an asymmetrical cost of chain-extension. The most-efficient chain at including user-paid fees is the cheapest to produce and the most profitable for all participants to extend. This eliminates the majoritarian attack identified Bracha and Toueg (1985) which assumes that state transitions must be symmetrically costly for honest nodes and attackers to propose. 

The fact that forking halves fee-flow without halving the cost of fee-unlock then breaks the arguments of Dwork, Lynch, and Stockmeyer (1988). While it may be possible for attackers to force the network into a state of balanced stasis, it is not possible for attackers to do this without shifting the network into an equilibrium that does not punish them as the nodes who are producing the blocks that force the network into a lower efficiency equilibrium.


