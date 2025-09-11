---
title: Impossibility Results
description: 
published: true
date: 2025-09-11T04:26:28.238Z
tags: 
editor: markdown
dateCreated: 2023-09-20T01:58:02.086Z
---

# Impossibility Results

Saito Consensus sidesteps several impossibility results that affect other consensus mechanisms and are often treated as defining general limitation on all distributed consensus mechanisms. 

The solution suggests general strategies exist for achieving incentive compatibility in informationally decentralized mechanisms, and offers a rebuttal to the following frequently-cited impossibility results from economics and computer science, showing that while these papers may be correct **within the bounds of their assumptions** -- those assumptions are not universally binding on distributed consensus mechanisms.

<br>

### 1. On Bitcoin and Red Balloons (2011)

An influential [academic paper](https://arxiv.org/pdf/1111.2626) by Moshe Babaioff, Shahar Dobzinski, Sigal Oren and Aviv Zohar has claimed the impossibility of building distributed mechanisms which incentivize transaction propagation. Their paper specifically asserts that "there are no reward schemes in which information propagation and no self-cloning is a dominant strategy."

Saito Consensus solves this problem, offering a routing payout to P2P nodes that encourages nodes to share transactions with their peers, yet does not make self-cloning rational. The solution works because adding hops to transactions decreases the usefulness of those transactions for producing blocks, reducing the expected income of the attacker by more than the attacker can expect to earn through the expanded claim on payout from an additional routing hop. One assumption from this paper that Saito Consensus violates is the expectation that all nodes must have an equal probability and thus cost of producing the most efficient next block.

We have a [mathematical proof](https://github.com/SaitoTech/papers/blob/e32c51db6aae071a41b7e481d0f5ba6cd75ec12d/sybil/A_Simple_Proof_of_Sybil_Proof_Lancashire-Parris_2023.pdf) that routing work solves this problem in a three-hop routing path. To our knowledge the routing-decay and probabilistic payout solution offered by Saito Cosnensus remains the only known solution to this problem.

<br>

### 2. Roughgarden and Shi (2020)

A number of papers from Tim Roughgarden (Colombia) and Elaine Shi (Cornell) claim the impossibility of building incentive compatible blockchains. While the very first paper from Shi is technically correct, it limits its analysis to direct mechanisms in which the transaction fee pays for a single (non-combinatorial) form of value, invalidating it as a model for blockchains where the fee is a non-scalar value that expresses joint preferences over a combinatorial bundle of utility (on-chain blockspace and security, speed-of-confirmation, availability of off-chain collusion goods).

In subsequent papers authors dropped their requirement for "single-parameter" fees and applied their model to mechanisms with "collusion goods" (possibility of off-chain payments), declaring the impossibility of achieving incentive compatibility in more general mechanisms. These claims are explicitly invalidated by Saito Consensus, whose solution points directly to fundamental theoretical problems which make the conclusions of these papers unsupportable in theory or practice.

Specifically, Saito Consensus shows the existence of consensus mechanisms that are are not reducible to direct mechanisms at all, and in which incentive compatibility does not require users to reveal their private valuation for only a single form of utility. In routing work mechanisms, the fee is a non-scalar value that expresses a joint valuation across multiple types of utility. The true valuation the user has for any particular kind of good is never revealed directly to the mechanism, as is common in other indirect mechanisms of its class.

A second more fundamental problem is the assumption of these models that block producers can "faithfully implement" incentive compatible mechanisms without also revealing their own relevant preferences to the mechanism. This is inconsistent with the requirements of implementation theory since "faithful implementation" requires "truthful preference revelation" in any incentive compatible mechanism. This oversight pushes these papers into internal-contradiction, as they explicitly prohibit block producers from revealing preferences through the strategy in which it occurs in Saito Consensus (the inclusion of self-generated transactions in blocks).

This oversight pushes the solution out-of-model. In Saito Consensus users are motivated to bid honestly by competition from producers: bid too low and producers will switch from being sellers to buyers of blockspace because of their desire to purchase faster transaction inclusion! This solution is only possible in a combinatorial auction -- another reason for the observed failure of single-parameter models -- as producers must be bidding for a form of utility that is different from the one they are selling when they produce a block.

On a closing note, we observe that most papers in this area fail to properly identify their social choice rule. While they implicitly adopt the rule of the Vickrey auction ("efficient allocation") this rule cannot be implemented in any mechanisms where the supply of the good being distributed is subject to strategic manipulation, as this introduces problems with "interdependent valuations" that block incentive compatibility with that specific social choice rule.

Switching to the appropriate social choice rule for two-sided auctions ("efficient allocation and production") with variable supply of utility forces us into requiring higher-dimensional preference revelation as both supply and demand-side preferences must be disclosed for any direct mechanism to implement welfare-optimal outcomes. We are once again reminded that the form of preference revelation forbidden from block producers in these models is required to achieve incentive compatibility.

We observe that Saito Consensus handles both forms of preference revelation indirectly: users reveal their preferences through both the fee they choose and their transaction broadcast strategies (private strategies indicate the existence of a welfare-increasing trade between the user and at least one block producer). Producers reveal their own preferences through their willingness to include their own fee-bearing transactions in blocks, effectively redirecting surplus profits from the sale of collusion goods into a subsidy for welfare-improving forms of speed valued more highly by other agents in the mechanism in equilibrium.


<br>

### 3. Bracha and Toueg (1985)

The paper *Asynchronous Consensus and Broadcast Protocols* by Bracha and Toueg shows that in an asynchronous system with **n** total processes, at most **(n−1)/2** processes can be adversarial. Their model assumes a network of processes that receive and respond to network messages automatically:

> In an atomic step of the system, a process can try to receive a message, perform an arbitrarily long local computation, and then send a finite set of messages. The computation and the messages sent are prescribed by the protocol, that is, a function of the message received and the local state.

In Saito Consensus the cost of proposing a block varies for different node in the network. And the probabiliy of winning the payment available to routing nodes also varies for block producers based on the efficiency with which they have sourced the transactions included in the block. These two costs do not move in unison for all nodes in the network, and making it faster and less expensive for nodes to propose blocks that contain more welfare efficient set of transactions.

It stops being that messages which reduce the overall efficiency of fee-throughput are symmetrically costly to those which do not.

<br>

### 4. Roger B. Myerson and Mark A. Satterthwaite (1983)

The paper *Efficient Mechanisms for Bilateral Trading* by Roger B. Myerson and Mark A. Satterthwaite prove that it is impossible to achieve incentive compatibility in any bilateral trading (direct) mechanism, with results that are extensible through the Revelation Principle to any two-sided mechanism with multiple participants that can be reduced to a direct mechanism.

Saito Consensus is an indirect mechanism that is not reducible to a direct mechanism via the Revelation Principle. This impossibility emerges because conversion would require agents to reveal their supply and demand preferences at all prices levels for an effectively infinite combination of collusion and in-network goods and on an infinitely granular time preference curve.

The informational problem that makes conversion impossible is not just the extreme multi-dimensionality of the preferences which must be revealed to the mechanism. It also emerges from the way the individual preference curves end up jagged and discontinuous because of the potential for participants to shift temporarily at arbitrary points between being producers and consumers of different combinations of goods, creating jagged spikes that cannot be assumed not to exist if agents have not fully revealed their preference. The fact that the "hinge" good that permits the trade-offs to be made efficiently is infinitely granular (time preference) then blocks generalizing assumptions that could otherwise assist in compressing the preference space into a finite representation.


### 5. Leonid Hurwicz (1972)

Hurwicz's seminal paper *The Design of Mechanisms for Resource Allocation* pointed out that in informationally decentralized mechanisms where communication between agents is needed prior to resource allocation, only mechanisms that can induce participants to share private preferences truthfully can be considered *incentive compatible* (i.e. robust to strategic manipulation by rational agents in expectation).

> These results show that the difficulty is due not to our lack of inventiveness, but to a fundamental conflict among such mechanism attributes as the optimality of equilibria, incentive-compatibility of the rules, and the requirements of informa- tional decentralization. Concessions must be made in at least one of these directions.

In Saito Consensus, the "pre-exchange messaging step" that is needed for agents to form price expectations and thus strategies is mediated through the blockchain itself and can only be manipulated through the sending of fee-bearing messages. And the cost that the publisher of this message must pay increases if it pushes the network into a less efficient equilibrium.

The cost of speech now depends on the content of the message. An asymmetrically higher cost is charged for false speech (state transitions which push us away from welfare-optimal outcomes), undermining the impossibility of implementing those equilibria in informationally decentralized conditions. Saito Consensus achieves incentive compatibility by fulfilling the requirements Hurwicz establishes through the indirect and decomposable optimization process he referred to generally as the "Greed Process".

<br> 

### Conclusion

The foundational impossibility results that computer scientists and economists developed in the 1970s and 1980s emerged out of the assumption that *processes* in computer systems were purely technical processes that could be costlessly manipulated by attackers. This resulted in the emergence of impossibility results based on the assumption that *malicious processes* could not be punished within consensus mechanisms as soon as they the same implicit "voting power" as honest nodes.

This assumption remains true in proof-of-work and proof-of-stake mechanisms, since those mechanisms lose the ability to punish attackers in majoritarian conditions. But there is no reason to consider this problem unsolvable. Subsequently impossibility results have not gone back to revisit the fundamentals examined in the 1980s, and have instead assumed that they must continue to hold, despite the shift to mechanisms that maintain their own unit-of-value and can punish participants without reference to external cost structures.



