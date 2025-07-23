---
title: majoritarian-attacks
description: 
published: true
date: 2025-07-23T10:30:15.318Z
tags: 
editor: markdown
dateCreated: 2023-09-20T01:58:02.086Z
---

# Eliminating Impossibility Results

Saito Consensus sidesteps several impossibility results that affect almost all other distributed consensus mechanisms. These allow the mechanism to achieve outcomes that are not possible with traditional approaches.

Given the [technical explanations](/consensus) of routing mechanisms elsewhere on this wiki, this page focuses on explaining how Saito skirts the academic impossibility results which form the intellectual foundation for claims that problems like majority attacks and incentive compatibility are unsolvable.

<br>

### 1. Bracha and Toueg (1985)

The paper *Asynchronous Consensus and Broadcast Protocols* by Bracha and Toueg shows that in an asynchronous system with **n** total processes, at most **(n−1)/2** processes can be adversarial. Their model assumes a network of processes that receive and respond to network messages automatically:

> In an atomic step of the system, a process can try to receive a message, perform an arbitrarily long local computation, and then send a finite set of messages. The computation and the messages sent are prescribed by the protocol, that is, a function of the message received and the local state.

In this model, nothing can stop malicious nodes from broadcasting messages that subvert consensus, and nothing can stop honest nodes from attempting to restore consensus. This creates tbe majoritarian vulnerability the paper arguesis impossible: whatever cohort can send the most messages wins.

Saito Consensus avoids this problem because the cost of proposing a message depends on its content: adversarial messages cost more to propose and refund less in equilibrium than honest messages. Over time, this shifts control of the resources needed to broadcast messages extend the chain away from attackers and towards honest nodes.

<br>

### 2. Dwork, Lynch, and Stockmeyer (1988)

The paper *Consensus in the Presence of Partial Synchrony* by Dwork, Lynch, and Stockmeyer (1988) examines how communication delays affect consensus protocols. One of its key insights is that consensus cannot be guaranteed when block production capacity is evenly split into two factions.

This is often used to claim that consensus mechanisms cannot prevent majoritarian attacks, as attackers who control 50% of network resources can always force a chain split by extending the shorter rather than longer of two competing network forks.

This is not possible in Saito Consensus for several reasons. The first is that splitting block production in such a way in a routing mechanisms requires controlling how every participant in the network communicates, which is not possible in informationally decentralized mechanisms and requires giving the attacker control over 100% rather than a mere 50% of network resources.

It is also not possible for attackers to trigger this by extending a private chain. To see why, remember that when attackers partition the network, they reduce the fee-throughput on their fork. The drop in fees reduces the income available to pay for hashing without reducing the difficulty of the mining puzzle. Any downward adjustment in the cost of getting paid is only possible if multiple blocks are left unsolved and their fees uncollected, imposing costs on the stealth fork.

So partitioning the network is not costless in the way that Dwork, Lynch, and Stockmeyer assume it must be. In contrast to other consensus mechanisms — where attackers can "balance" competing chains without dictating peer connections and extend stealth chains at the same cost of public chains, Saito Consensus succeeds in making both types of network partitioning attacks irrational. 


### 4. On Bitcoin and Red Balloons (2011)

An influential [academic paper](https://arxiv.org/pdf/1111.2626) by Moshe Babaioff, Shahar Dobzinski, Sigal Oren and Aviv Zohar has claimed the impossibility of building distributed mechanisms which incentivize transaction propagation. Their paper specifically asserts "that there are no reward schemes in which information propagation and no self-cloning is a dominant strategy."

Saito Consensus solves this problem, offering a routing payout to P2P nodes that encourages nodes to share transactions with their peers, yet without make self-cloning rational. The solution works because adding hops to transactions decreases the value of those transactions for producing blocks, forcing the attacker to contribute and burn more of their own money in equilibrium than the attacker can expect to earn through an expanded claim on payout in the payment lottery.

A [mathematical proof](https://github.com/SaitoTech/papers/blob/e32c51db6aae071a41b7e481d0f5ba6cd75ec12d/sybil/A_Simple_Proof_of_Sybil_Proof_Lancashire-Parris_2023.pdf) that routing work solves this problem in a three-hop routing path. To date the routing-decay and probabilistic payout solution offered by Saito Cosnensus remains the only known solution to this problem.


### 4. Roughgarden and Shi (2020)

A school of papers from Tim Roughgarden (Colombia) and Elaine Shi (Cornell) and others has emerged claiming the impossibility of building incentive compatible blockchains. Saito Consensus offers a self-evident counter-proof to these claims as an indirect mechanism that implements a welfare-optimizing social choice rule.

The fundamental problem with these papers involve the existence of private preferences which affect transactions fees but are never revealed to the mechanism as required by implementation theory. Undisclosed preferences prevent these authors from meeting the requirements that Hurwicz, Maskin and Myerson establish as a prerequisite for proving the possibility or impossibility of incentive compatibility, rendering their impossibility claims tautological and non-binding.

A second problem involves these authors forgetting that the "faithful implementation" of any incentive compatible mechanism by definition requires the "faithful revelation" of relevant preferences. This problems applies to the treatment of block producers in these papers, who are explicitly forbidden from sharing information with the mechanism through the inclusion of self-generated transactions, thus blocking a form of competition (between users and producers) that the solution uses to induce users to pay the optimal fee. Prohibiting preference revelation violates the fundamental tenets of implementation theory.

Saito Consensus handles both kinds of preference revelation indirectly: users reveal their willingness to collude through the fee they choose and their transaction distribution strategies, while producers reveal their own preferences through their willingness to include their own fee-bearing transactions in blocks and bundle privately-distributed transactions into blocks.

### Conclusion

The foundational impossibility results that computer scientists and economists developed in the 1970s and 1980s emerged out of the assumption that *processes* in computer systems were purely technical processes that could be costlessly manipulated by attackers. This resulted in the emergence of impossibility results based on the assumption that *malicious processes* could not be punished within consensus mechanisms as soon as they the same implicit "voting power" as honest nodes.

This assumption remains true in proof-of-work and proof-of-stake mechanisms, since those mechanisms lose the ability to punish attackers in majoritarian conditions. But there is no reason to consider this problem unsolvable. Subsequently impossibility results have not gone back to revisit the fundamentals examined in the 1980s, and have instead assumed that they must continue to hold, despite the shift to mechanisms that maintain their own unit-of-value and can punish participants without reference to external cost structures.



