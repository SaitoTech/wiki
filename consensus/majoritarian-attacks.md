---
title: majoritarian-attacks
description: 
published: true
date: 2025-05-22T03:08:51.212Z
tags: 
editor: markdown
dateCreated: 2023-09-20T01:58:02.086Z
---

# Eliminating 51% Attacks

Many people believe that the 51% attack is fundamentally unsolvable. This belief stems from widely cited academic papers that claim it is mathematically impossible to build consensus systems that majoritarian attacks. Saito Consensus establishes it is possible to work around these.

Given the [technical explanations](/consensus) of routing mechanisms elsewhere on this wiki, this page focuses on explaining how Saito skirts the academic impossibility results which form the intellectual foundation for claims that majority attacks are unsolvable: *Bracha and Toueg* (1985) and *Dwork, Lynch, and Stockmeyer* (1988).

<br>

### 1. Bracha and Toueg (1985)

The paper *Asynchronous Consensus and Broadcast Protocols* by Bracha and Toueg claims that in an asynchronous system with **n** total processes, at most **(n−1)/2** processes can be Byzantine. Their proof is based on a network made up of processes that respond to inbound messages:

> In an atomic step of the system, a process can try to receive a message, perform an arbitrarily long local computation, and then send a finite set of messages. The computation and the messages sent are prescribed by the protocol, that is, a function of the message received and the local state.

In this model, all messages cost the same amount to broadcast, thus allowing any malicious majority to indefinitely stalemate any honest minority. But what if it costs malicious nodes more to send Byzantine messages than it costs honest nodes to follow the protocol? And what if the cost paid is the loss of resources required to send further messages?

Unlike Bracha and Toueg's model, routing work mechanisms force attackers to burn their own tokens to produce blocks, and refund them less back when those blocks orphan honest blocks. Not only must attackers spend their own tokens to attack the chain, but they must transfer tokens to honest nodes in proportion to the amount of honest blocks they orphan. Over time, this tax shifts control of the resources needed to propose further state transitions away from attackers, eroding their ability to continue the attack.

As a result, the assumptions in Bracha and Toueg simply do not apply to Saito Consensus. Malicious nodes can extend the chain, but with every honest block they orphan they reduce their control of the resource that must be burned to propose blocks, pulling even a malicious majority back into minority status and rendering them -- eventually -- unable to continue the attack at all.

<br>

### 2. Dwork, Lynch, and Stockmeyer (1988)

A related impossibility result is from *Consensus in the Presence of Partial Synchrony* by Dwork, Lynch, and Stockmeyer (1988). This paper examines how communication delays affect consensus protocols. One of its key insights is that consensus cannot be guaranteed when block production capacity is evenly split into two partitions.

This argument is often used to claim that consensus mechanisms cannot deter attackers from "split-brain" situations or 50/50 attacks. However these claims do not apply to Saito Consensus.

The first reason is that splitting block production this way in Saito Consensus requires dictating how every participant in the network connects and communicates with others. This requires controlling 100% of network resources not a mere majority. Nor is the assumption this situation can persist compatible with the requirements of informational decentralization.

We can salvage the attack by giving an attacker only 50% of network fee-flow and having them extend a private chain they refuse to disclose to honest nodes. This version of the attack sounds more plausible — it forces a split while requiring only half the network’s economic activity. But does it succeed?

As consideration will show, the attacker who previously spent half of their income mining golden tickets to unlock the routing payout is now spending the entire block reward to mine golden tickets. Their cost of getting paid has doubled, and that is before any need to pay actual network costs. Consensus has succeeded in making this attack economically irrational.

In contrast to other consensus mechanisms — where attackers can shift their work to private forks without direct penalty and even profit by moving transactions from the honest chain onto their fork — Saito punishes such behavior. Nodes that cooperate reduce their own cost of getting paid. Attacks that terminate this cooperation through partitioning or isolating nodes become self-defeating, and impose increasing economic losses on attackers.

### Conclusion

Saito Consensus creates an asymmetrical cost of chain-extension. The most-efficient chain at including user-paid fees is the cheapest to produce and the most profitable for all participants to extend. This eliminates the majoritarian attack identified Bracha and Toueg (1985) which assumes that state transitions must be symmetrically costly for honest nodes and attackers to propose. 

The fact that forking halves fee-flow without halving the cost of fee-unlock then breaks the arguments of Dwork, Lynch, and Stockmeyer (1988). While it may be possible for attackers to force the network into a state of balanced stasis, it is not possible for attackers to do this without shifting the network into an equilibrium that does not punish them as the nodes who are producing the blocks that force the network into a lower efficiency equilibrium.


