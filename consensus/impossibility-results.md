---
title: Impossibility Results
description: 
published: true
date: 2025-09-13T12:15:30.329Z
tags: 
editor: markdown
dateCreated: 2023-09-20T01:58:02.086Z
---

# Impossibility Results

Saito Consensus sidesteps several impossibility results that affect other consensus mechanisms and are often treated as theoretical limits on all distributed consensus mechanisms. 

The solution suggests general strategies exist for achieving incentive compatibility in informationally decentralized mechanisms, and offers a rebuttal to the following frequently-cited impossibility results from economics and computer science, showing that while these papers may be correct **within the bounds of their assumptions** -- those assumptions are not universally binding on distributed consensus mechanisms.

<br>

### 1. On Bitcoin and Red Balloons (2011)

An influential [academic paper](https://arxiv.org/pdf/1111.2626) by Moshe Babaioff, Shahar Dobzinski, Sigal Oren and Aviv Zohar has claimed the impossibility of building distributed mechanisms which incentivize transaction propagation. Their paper specifically asserts that "there are no reward schemes in which information propagation and no self-cloning is a dominant strategy."

Saito Consensus solves this problem, offering a routing payout to P2P nodes that encourages nodes to share transactions with their peers, yet does not make self-cloning rational. The solution works because adding hops to transactions decreases the usefulness of those transactions for producing blocks, reducing the expected income of the attacker by more than the attacker can expect to earn through the expanded claim on payout from an additional routing hop. One assumption from this paper that Saito Consensus violates is the expectation that all nodes must have an equal probability and thus cost of producing the most efficient next block.

We have a [mathematical proof](https://github.com/SaitoTech/papers/blob/e32c51db6aae071a41b7e481d0f5ba6cd75ec12d/sybil/A_Simple_Proof_of_Sybil_Proof_Lancashire-Parris_2023.pdf) that routing work solves this problem in a three-hop routing path. To our knowledge the routing-decay and probabilistic payout solution offered by Saito Cosnensus remains the only known solution to this problem.

<br>

### 2. Roughgarden and Shi (2020)

A school of academics led by Tim Roughgarden (Columbia) and Elaine Shi (Cornell) argue it is impossible to build incentive-compatible blockchains. Saito Consensus provides a direct counterexample, exposing several fundamental problems with the assumptions underlying these papers.

The first major problem involves the assumption that the transaction fee is a scalar value that reflects only the bidder’s private valuation for blockspace. This is clearly incorrect. Transaction fees are non-scalar values that express a joint preference over a multi-dimensional bundle of utility: they can be adjusted to buy more or less blockspace, to affect inclusion times, and/or to secure off-chain benefits (“collusion goods”) that peers may provide in return for the exclusive access to the transaction.

Because fees are non-scalar, they lack the monotonicity required to invoke implementation theory in the way these papers attempt. Worse, the models attempt to hide this problem by acknowledging the fact that collusion is possible, yet never asking users or producers to reveal their valuations for these forms of available utility to the mechanism. The presence of undisclosed but relevant preferences is the underlying source of the impossibility results found by these papers. They are the product of the internal contradictions in the models themselves, since -- as Maksin observes -- incentive compatibility is impossible in direct mechanisms without adequate and truthful preference revelation.

A second and deeper flaw is the assumption that block producers can faithfully implement incentive-compatible mechanisms without revealing their own private preferences. This contradiction ("faithful implementation" without "faithful revelation") is worsened by these models prohibiting producers from inserting their own transactions in blocks -- expressly preventing them from communicating with the consensus mechanism.

Saito Consensus shows how combinatorial auctions can fix this problem and implement incentive compatible fee mechanisms: users are motivated to bid honestly exactly because competition to purchase blockspace exists from producers: bid too low and producers will switch from being sellers to buyers of blockspace and out-bid them in their own demand-side auction. Fascinatingly, this solution is only possible because the transaction fee is non-scalar and the blockchain is a combinatorial auction -- producers must have a rational reason to purchase blockspace that is different from that motivating users.

On a closing note, we observe that all of the TFM papers to date also fail to meet the requirements of implementation theory in their failure to properly specify the social choice rule with which they desire incentive compatibility. While the authors of most papers implicitly adopt the rule of the Vickrey auction ("efficient allocation") none seem aware this rule cannot be implemented by any mechanisms in which the supply of utility changes based on the strategies used by agents in the mechanism. The fact that the supply of utility floats based on the strategic engagement of agents with the mechanism creates the known problem of "interdependent valuations" that breaks the models and thus their conclusions.

Switching to the appropriate social choice rule for two-sided auctions ("efficient allocation and production") allows mechanisms to handle a variable supply of utility but forces us into requiring higher-dimensional preference revelation as both supply and demand-side preferences must be disclosed for any direct mechanism to implement welfare-optimal outcomes.  The papers cannot mathematically model this using the techniques they attempt to use, which makes them methodologically incapable of drawing the conclusions they do.

We close by observing that in Saito Consensus we do see proper -- if indirect -- preference revelation. users reveal their preferences through both the fee they choose and the broadcast strategies they use to share their transactions with peers in the network. Producers reveal their own preferences through their willingness to add their own fee-flow to blocks, effectively redirecting surplus profits from the sale of collusion goods into a subsidy that drives the faster inclusion valued more highly by other agents in equilibrium.

<br>

### 3. Bracha and Toueg (1985)

The paper *Asynchronous Consensus and Broadcast Protocols* by Bracha and Toueg shows that in an asynchronous system with **n** total processes, at most **(n−1)/2** processes can be adversarial. Their model assumes a network of processes that receive and respond to network messages automatically:

> In an atomic step of the system, a process can try to receive a message, perform an arbitrarily long local computation, and then send a finite set of messages. The computation and the messages sent are prescribed by the protocol, that is, a function of the message received and the local state.

In Saito Consensus the cost of proposing a block varies for different nodes in the network. And the probabiliy of winning the routing payment also varies based on the efficiency with which all nodes participated in sourcing the transactions included in the block. These two costs do not move in unison for all nodes in the network. It is less expensive for nodes to propose blocks that contain more welfare-optimal set of transactions.

This breaks the assumption in this paper that all messages are symmetrically costly to propose. The most efficient block that it is possible to propose is cheaper than all others.

<br>

### 4. Roger B. Myerson and Mark A. Satterthwaite (1983)

The paper *Efficient Mechanisms for Bilateral Trading* by Roger B. Myerson and Mark A. Satterthwaite prove that it is impossible to achieve incentive compatibility in any bilateral trading (direct) mechanism, with results that are extensible through the Revelation Principle to any two-sided mechanism with multiple participants that can be reduced to a direct mechanism.

Saito Consensus is an indirect mechanism that is not reducible to a direct mechanism via the Revelation Principle. This impossibility emerges because conversion would require agents to reveal their supply and demand preferences at all prices levels for an effectively infinite combination of collusion and in-network goods and along an infinitely granular time preference curve.

The informational problem that makes conversion impossible is not just the extreme multi-dimensionality of the preferences which must be revealed to the mechanism. It also emerges from the way the jagged and discontinuous indifferent curves created by multidimensional forms of utility combine with the possibility of regime shift on each (buyers becoming sellers and vice-versa) to create the potential for jagged spikes that cannot be assumed not to exist if agents have not fully revealed their preferences. The fact that the "hinge" good that permits all trade-offs to be made efficiently is infinitely granular (time preference) consequently blocks generalizing assumptions that could assist in compressing the preference space into a finite representation that could be theoretically revealed to a direct mechanism.


### 5. Leonid Hurwicz (1972)

Hurwicz's seminal paper *The Design of Mechanisms for Resource Allocation* pointed out that in informationally decentralized mechanisms where communication between agents is needed prior to resource allocation, only mechanisms that can induce participants to share private preferences truthfully can be considered *incentive compatible* (i.e. robust to strategic manipulation by rational agents in expectation).

> These results show that the difficulty is due not to our lack of inventiveness, but to a fundamental conflict among such mechanism attributes as the optimality of equilibria, incentive-compatibility of the rules, and the requirements of informa- tional decentralization. Concessions must be made in at least one of these directions.

In Saito Consensus, the "pre-exchange messaging step" that is needed for agents to form price expectations and thus strategies is mediated through the blockchain itself and can only be manipulated through the sending of fee-bearing messages. And the cost that the publisher of this message must pay increases if it pushes the network into a less efficient equilibrium.

The cost of speech now depends on the content of the message. An asymmetrically higher cost is charged for false speech (state transitions which push us away from welfare-optimal outcomes), undermining the impossibility of implementing those equilibria in informationally decentralized conditions. Saito Consensus achieves incentive compatibility by fulfilling the requirements Hurwicz establishes through the indirect and decomposable optimization process he referred to generally as the "Greed Process".

<br> 

### Conclusion

The foundational impossibility results that computer scientists and economists developed in the 1970s and 1980s emerged out of the assumption that *processes* in computer systems were purely technical processes that could be costlessly manipulated by attackers. This resulted in the emergence of impossibility results based on the assumption that *malicious processes* could not be punished within consensus mechanisms as soon as they the same implicit "voting power" as honest nodes.

This assumption remains true in proof-of-work and proof-of-stake mechanisms, since those mechanisms lose the ability to punish attackers in majoritarian conditions. But there is no reason to consider this problem unsolvable. Subsequently impossibility results have not gone back to revisit the fundamentals examined in the 1980s, and have instead assumed that they must continue to hold, despite the shift to mechanisms that maintain their own unit-of-value and can punish participants without reference to external cost structures.



