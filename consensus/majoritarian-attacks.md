---
title: majoritarian-attacks
description: 
published: true
date: 2025-05-21T12:36:04.034Z
tags: 
editor: markdown
dateCreated: 2023-09-20T01:58:02.086Z
---

# Eliminating 51% Attacks

Many people believe that the 51% attack is fundamentally unsolvable. This belief stems from widely cited academic papers that claim it is mathematically impossible to build consensus systems that majoritarian attacks. Saito Consensus proves otherwise.

Given the [technical explanations](/consensus) of how Saito Consensus works elsewhere on this wiki, this page focuses on two of the most influential impossibility results in distributed systems: *Bracha and Toueg* (1985) and *Dwork, Lynch, and Stockmeyer* (1988). These papers form the intellectual foundation for claims that majority attacks are unsolvable. We'll show why these results do not apply to routing work mechanisms like Saito.

<br>

### 1. Bracha and Toueg (1985)

The paper *Asynchronous Consensus and Broadcast Protocols* by Bracha and Toueg claims that in an asynchronous system with **n** total processes, at most **(n−1)/2** processes can be Byzantine for the network to reach consensus.

The model they adopt assumes a network made up of processes that respond to messages:

> In an atomic step of the system, a process can try to receive a message, perform an arbitrarily long local computation, and then send a finite set of messages. The computation and the messages sent are prescribed by the protocol, that is, a function of the message received and the local state.

Critically, all messages cost all processes the same amount to broadcast in this model. If that assumption holds, Bracha and Toueg are correct: a malicious majority can indefinitely stalemate an honest minority. But what if it costs malicious nodes more to send messages than it costs honest nodes? And what if they received back less of the resources required to send further messages?

Unlike Bracha and Toueg's model, routing work mechanisms force attackers to burn tokens to produce blocks, and they get less refunded when those blocks are orphaning other blocks. Not only must attackers spend their own tokens to attack the chain, but they must transfer resources in aggregate to the honest nodes. Over time, the UTXO set shifts away from the attackers, eroding their ability to continue the attack.

As a result, the assumptions in Bracha and Toueg simply do not apply to Saito Consensus. Malicious nodes can extend the chain, but with every honest block they orphan they reduce their control of the resource that must be burned to propose blocks, pulling even a malicious majority back into minority status and rendering them -- eventually -- unable to continue the attack at all.

<br>

### 2. Dwork, Lynch, and Stockmeyer (1988)

A second and related impossibility result comes from *Consensus in the presence of Partial Synchrony* by Dwork, Lynch, and Stockmeyer (1988) which examines how delays in communication affect consensus protocols. One of their key insights is that consensus cannot be guaranteed to resolve when block production capacity is evenly split between two partitions of the network.

This argument is often used to claim that consensus systems cannot recover from "split-brain" situations or co-ordinated 50/50 attacks, yet these claims also fail to apply to Saito Consensus.

The most obvious reason is that splitting block production resources evenly in a routing work mechanism requires absolute control over how each participant and node in the network communicates. It is not reasonable to require control of 100% of network participants in order to pull off an attack that involves mere majority. Nor is imposing such a situation compatible with the theoretical requirements of informational decentralization.

We can try to salvage this attack by assuming our attacker already controls 50% of pre-attack fee-flow and is merely shifting their own resources to a private chain that they refuse to distribute to honest nodes in order to force them to extend a separate chain instead of happily extending the attacker's fork. This seems a more reasonable scenario since it requires the attacker to control a mere 50% of network fee-flow. Does this attack compromise Saito Consensus?

Unsurprisingly, while this attack may be theoretically possible in Saito Consensus, it is still economically irrational. Suddenly our attacker, who was previously spending 50% of their fee-flow producing golden tickets to unlock the remainder as routing payouts, is now spending 100% of their fee-flow to do the same. Not only has their cost-of-getting-paid doubled, it has consumed every penny of their potential profit, and that is without consideration for the economic costs of running the network infrastructure needed to collect the fees in the first palce.

Whereas other mechanisms make the DLS attack costless to attackers, who can move honest transactions into their private chain and attempt to collect them as payments, in Saito Consensus this is not possible. Attackers are forced to operate at a loss and the consensus mechanisms continues to do its job of ensuring byzantine nodes face a quantifiable economic loss for attacking the network and its users.

### Conclusion

Saito Consensus creates an asymmetrical cost of chain-extension. The most-efficient chain at including user-paid fees is the cheapest to produce and the most profitable for all participants to extend. This eliminates the majoritarian attack identified Bracha and Toueg (1985) which assumes that state transitions must be symmetrically costly for honest nodes and attackers to propose. 

The fact that forking halves fee-flow without halving the cost of fee-unlock then breaks the arguments of Dwork, Lynch, and Stockmeyer (1988). While it may be possible for attackers to force the network into a state of balanced stasis, it is not possible for attackers to do this without shifting the network into an equilibrium that does not punish them as the nodes who are producing the blocks that force the network into a lower efficiency equilibrium.


