---
title: Impossibility Results
description: 
published: true
date: 2025-09-13T13:48:12.211Z
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

A school of academics led by Tim Roughgarden (Columbia) and Elaine Shi (Cornell) argue it is impossible to build incentive-compatible blockchains. Saito Consensus provides a direct counter-example, exposing several fundamental problems with the assumptions underlying these papers in the process.

The first major problem involves the assumption that the transaction fee is a scalar value that reflects only the bidder’s private valuation for blockspace. This is clearly incorrect. Transaction fees are non-scalar values that express a joint preference over a multi-dimensional bundle of utility: they can be adjusted to buy more or less blockspace, faster or slower inclusion, and/or to secure off-chain benefits (“collusion goods”) that peers may provide in return for exclusive access to the transaction.

Because transaction fees are non-scalar in practice, they lack the property of monotonicity these models assert they must have as a pre-requisite for proving it is impossible to achieve incentive compatibility generally. The impossibility results therefore fail on straightforward grounds of model misspecification: they do not accurately capture the properties of the mechanisms they claim to analyze.

Worse, while these papers explicitly acknowledge that other types of utility exist (such as incentives to collude) their models never ask agents to reveal their valuations for these additional forms of utility as required by implementation theory. This pushes the models beyond misspecification and into open contradiction: they invoke the framework for incentive compatibility provided by Maskin (2002) without following its most basic requirements for truthful preference revelation.

Even if we overlook this problem and agree to treat the transaction fee as a scalar value that can at least theoretically reflect the truthful valuation that users have for blockspace, the security-levels and amount of blockspace provided by any TFM clearly change based on the strategies chosen by agents within the mechanism. This means the amount of utility available for purchase through the mechanism cannot be known in advance, and we have the classic problem of "interdependent valuations" under which it is not possible to make any assumptions about the truthfulness of even a scalar fee.

A second and more subtle flaw is the assumption that block producers can faithfully implement incentive-compatible protocols without needing to reveal their own private preferences to those protocols. This contradiction ("faithful implementation" without "faithful revelation") is overlooked by these models, which then make matters worse by explicitly forbidding producers from including self-generated transaction in blocks. This restriction violates the requirement that we do not prohibit agents from revealing preferences to the mechanism.

On a closing note, we observe that all of the TFM papers to date also fail to properly specify the social choice rule with which they desire incentive compatibility. While the authors of most papers implicitly adopt the rule of the Vickrey auction ("efficient allocation") none seem aware that this social choice rule cannot be implemented in a two-sided mechanism where supply as well as demand-side pressures must come into equilibrium.

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



