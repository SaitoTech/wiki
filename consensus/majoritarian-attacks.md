---
title: majoritarian-attacks
description: 
published: true
date: 2025-05-22T09:55:40.295Z
tags: 
editor: markdown
dateCreated: 2023-09-20T01:58:02.086Z
---

# Eliminating 51% Attacks

Many people believe that the 51% attack is fundamentally unsolvable. This belief stems from widely cited academic papers that claim it is mathematically impossible to build consensus systems that majoritarian attacks. Saito Consensus establishes it is possible to work around these.

Given the [technical explanations](/consensus) of routing mechanisms elsewhere on this wiki, this page focuses on explaining how Saito skirts the academic impossibility results which form the intellectual foundation for claims that majority attacks are unsolvable: *Bracha and Toueg* (1985) and *Dwork, Lynch, and Stockmeyer* (1988).

<br>

### 1. Bracha and Toueg (1985)

The paper *Asynchronous Consensus and Broadcast Protocols* by Bracha and Toueg claims that in an asynchronous system with **n** total processes, at most **(n−1)/2** processes can be Byzantine. Their proof assumes a network of processes that respond to inbound messages:

> In an atomic step of the system, a process can try to receive a message, perform an arbitrarily long local computation, and then send a finite set of messages. The computation and the messages sent are prescribed by the protocol, that is, a function of the message received and the local state.

In this model, all messages cost the same amount to broadcast. Honest nodes respond with messages that promote consensus while Byzantine nodes respond in ways that prevent consensus. Nothing can stop malicious nodes from broadcasting messages that subvert consensus, allowing any malicious majority to indefinitely stalemate any honest minority.

But what if it costs malicious nodes more to send Byzantine messages than it costs honest nodes to broadcast honest messages? And what if the cost paid is the loss of resources required to send further messages?

Saito Consensus breaks the assumption Bracha and Toueg make that the cost of sending messages must be the same for honest and Byzantine nodes. It forces attackers to burn more tokens to propose their blocks, and refunds them less in network payouts when they do. Over time, this shifts control of the resources needed to extend the chain away from attackers, eroding their ability to continue the attack.

The proof Bracha and Toueg offer is based on axiomatic assumptions that do not apply to Saito Consensus. Malicious nodes can extend the chain, but the punishment imposed for orphaning honest blocks will eventually pull even a malicious majority back into minority status and render them able to continue the attack.

<br>

### 2. Dwork, Lynch, and Stockmeyer (1988)

A second impossibility result is from *Consensus in the Presence of Partial Synchrony* by Dwork, Lynch, and Stockmeyer (1988). This paper examines how communication delays affect consensus protocols. One of its key insights is that consensus cannot be guaranteed when block production capacity is evenly split into two partitions.

This argument is often used to claim that consensus mechanisms cannot prevent "split-brain" situations or 50/50 splits, because attackers who control 50% of network resources can always force a chain split.

There are two reasons this does not apply to Saito Consensus. The first is that splitting block production this way in a routing mechanisms requires dictating how every participant in the network communicates. This is not possible in informationally decentralized mechanisms, and requires giving the attacker control over 100% of network resources. Calling this a majoritarian attack is misleading.

But what if we give the attacker control of exactly half of network fee-flow and simply have them force a partiction by building a private chain they refuse to disclose to honest nodes. This forces a split without requiring the attacker to control the behavior of honest nodes. Can this attack succeed?

To understand why not, remember that when attackers partition the network, they reduce the fee-throughput on their fork. The drop in fees reduces the income available to pay for golden tickets, but does not reduce the difficulty of finding those tickets. Any downward adjustment in the cost of getting paid is only possible if multiple blocks are produced whose burned fees are not paid-out at all. And those costs are concentrated on the attacker, who is producing the blocks whose fees must go uncaptured.

So partitioning the network is not costless in the way that Dwork, Lynch, and Stockmeyer assume it must be. Any attacker who shifts to a private chain increases their cost of getting paid so much that the entire block reward must now be spent simply to recover any funds at all. In the production design, this cost actually rises above 100% of the block reward and results in direct losses.

In contrast to other consensus mechanisms — where attackers can shift work to private forks without direct penalty — Saito Consensus succeeds in making network partitioning attacks irrational. 

### Conclusion

The foundational impossibility results in the 1980s developed out of the assumption that *processes* in computer systems do not face any internal cost for messaging, and thus *malicious processes* cannot be punished if they choose to send malicious messages or partition their communications in ways that cripples the ability for honest nodes to reach consensus.

This assumption remains true in proof-of-work and proof-of-stake mechanisms, since once those mechanisms are under majoritarian attack they lose the ability to asymmetrically punish attackers. But there is no theoretical reason to believe that these limitations are universal limitations.

Saito Consensus creates an asymmetrical cost for sending messages. The most-efficient chain at including user-paid fees is the cheapest to produce and the most profitable for all participants to extend. This eliminates the majoritarian attack identified Bracha and Toueg (1985) which assumes that state transitions must be symmetrically costly for honest nodes and attackers to propose. 

Partitioning the network into equal halves is also irrational and pushes attackers into loss. While it may be possible for attackers to force the network into a state of balanced stasis, it is not possible to do this without accepting losses. This breaks the arguments of Dwork, Lynch, and Stockmeyer (1988).

