---
title: Impossibility Results
description: 
published: true
date: 2025-08-26T08:00:05.179Z
tags: 
editor: markdown
dateCreated: 2023-09-20T01:58:02.086Z
---

# Impossibility Results

Saito Consensus sidesteps several impossibility results that affect other consensus mechanisms. These allow the mechanism to achieve outcomes that are not possible with traditional approaches.

Please see our [technical explanation](/consensus) of consensus for a description of the mechanism itself. This page highlights how Saito avoids being bound by the classic impossibility results from economics and computer science which limit most other designs. It should be noted that this is not an argument that these papers are wrong **within the bounds of their assumptions** -- merely that these assumptions are not binding on routing mechanisms as routing mechanisms ellude their limitations or avoid the informational problems which throw the models into internal contradiction and thus impossibility.


<br>

### 1. On Bitcoin and Red Balloons (2011)

An influential [academic paper](https://arxiv.org/pdf/1111.2626) by Moshe Babaioff, Shahar Dobzinski, Sigal Oren and Aviv Zohar has claimed the impossibility of building distributed mechanisms which incentivize transaction propagation. Their paper specifically asserts that "there are no reward schemes in which information propagation and no self-cloning is a dominant strategy."

Saito Consensus solves this problem, offering a routing payout to P2P nodes that encourages nodes to share transactions with their peers, yet does not make self-cloning rational. The solution works because adding hops to transactions decreases the usefulness of those transactions for producing blocks, reducing the expected income of the attacker by more than the attacker can expect to earn through the expanded claim on payout from an additional routing hop. One assumption from this paper that Saito Consensus violates is the expectation that all nodes must have an equal probability and thus cost of producing the most efficient next block.

We have a [mathematical proof](https://github.com/SaitoTech/papers/blob/e32c51db6aae071a41b7e481d0f5ba6cd75ec12d/sybil/A_Simple_Proof_of_Sybil_Proof_Lancashire-Parris_2023.pdf) that routing work solves this problem in a three-hop routing path. To our knowledge the routing-decay and probabilistic payout solution offered by Saito Cosnensus remains the only known solution to this problem.

<br>

### 2. Roughgarden and Shi (2020)

A number of papers from Tim Roughgarden (Colombia) and Elaine Shi (Cornell) claim the general impossibility of building incentive compatible blockchains. The very first paper from Shi is technically corrct as it limits its analysis to direct mechanisms in which the transaction fee pays for only a single (non-combinatorial) form of value. This same focus invalidates it as a model for blockchains where fees express a joint valuation over a combinatorial bundle of utility (on-chain blockspace and security, speed-of-confirmation, off-chain collusion goods).

In subsequent papers both authors dropped the requirement for "single-paramater" fees and expanded their scope of analysis to mechanisms with multiple forms of utility. It is these secondary claims that are explicitly invalidated by Saito Consensus, whose structure also points to fundamental theoretical problems with these papers.

Specifically, Saito Consensus shows it is possible to design consensus mechanisms that are are not reducible to direct mechanisms in which incentive compatibility requires users to reveal their private valuation for only a single form of utility: blockspace. In routing work mechanisms, the fee continues to provide a joint valuation across three types of utility: the valuation of transaction inclusion, its speed-of-confirmation, and any utility available to the user through collusion with block producers.

The fact that users have private valuations for at least three co-mingled forms of utility is why the Roughgarden and Shi papers find incentive compatibility impossible to achieve in theory. What they fail to see is that -- mathematically -- the existence of non-scalar valuations that cannot be informationally reduced to single-dimensional monotonic bids makes their models inconsistent with the requirements of implementation theory. Their results therefore do not hold; they arise from applying single-parameter conditions outside their domain of validity.

Saito Consensus eliminates this problem by shifting to a indirect combinatorial auction in which the non-scalar bid *combines* with broadcast strategy to encode user preferences over multidimensional outcomes obliquely through action-in-mechanism.

A second problem with this school of papers exists because they require block producers to "faithfully implement" incentive compatible mechanisms while overlooking that faithful implementation of any incentive compatible mechanism necessarily requires "faithful revelation" of all relevant private preferences by all relevant actors. This oversight pushes these papers into internal-contradiction, as they explicitly prohibit block producers from revealing preferences through the strategy in which it occurs in Saito Consensus (the inclusion of self-generated transactions in blocks).

This oversight pushes the solution out-of-model and invites failures. Incentive compatibility requires users to face competition for blockspace from producers: bid too low and producers will switch from being sellers to buyers of blockspace because of their desire to purchase faster transaction inclusion! And this is only possible in a combinatorial auction, since producers must be bidding for a form of utility that is different from the one they are selling when they produce a block.

Finally, we observe that many papers skip properly identifying their social choice rule. While they implicitly adopt the rule of the Vickrey auction ("efficient allocation") this rule cannot be used in mechanisms where the supply of the good being distributed is subject to strategic manipulation, as this introduces problems with interdependent valuations that thwart the theoretical possibility of incentive compatibility.

Switching to the more appropriate rule for two-sided auctions ("efficient allocation and production") forces us into requiring higher-dimensional preference revelation as both supply and demand-side preferences must be disclosed for any direct mechanism to implement welfare-optimal outcomes.

Saito Consensus handles both forms of preference revelation indirectly: users reveal their bundled preference for three forms of utility through both the fee they choose and their transaction broadcast strategies (which indicate the existence of a welfare-increasing cooperative trade between the user and at least one block producer). Producers reveal their private cost structures through their willingness to include their own fee-bearing transactions in blocks, effectively redirecting surplus profits from the sale of collusion goods into a subsidy for either the welfare-improving forms of speed or collusion utility more highly valued by counterparties in the mechanism.


<br>

### 3. Bracha and Toueg (1985)

The paper *Asynchronous Consensus and Broadcast Protocols* by Bracha and Toueg shows that in an asynchronous system with **n** total processes, at most **(n−1)/2** processes can be adversarial. Their model assumes a network of processes that receive and respond to network messages automatically:

> In an atomic step of the system, a process can try to receive a message, perform an arbitrarily long local computation, and then send a finite set of messages. The computation and the messages sent are prescribed by the protocol, that is, a function of the message received and the local state.

In Saito Consensus the cost of proposing a block depends on the contents of its transaction set. The refund available for proposal also depends on the contents of the transaction set. And these two variables move in ways that make it faster and less expensive to propose blocks that contain more welfare efficient set of transactions.

As a consequence, biasing block production towards economic efficiency forces all attacks which orphan or exclude competitive work to shift the network into a lower state of a form of efficiency measurable within the network. With this adjustment used as an input to regulate (reduce) payouts, it is no longer true that messages which reduce the overall efficiency of fee-throughput are symmetrically costly to those which are not.

<br>

### 4. Roger B. Myerson and Mark A. Satterthwaite (1983)

The paper *Efficient Mechanisms for Bilateral Trading* by Roger B. Myerson and Mark A. Satterthwaite prove that it is impossible to achieve incentive compatibility in any bilateral trading (direct) mechanism, with results that are extensible through the Revelation Principle to any two-sided mechanism with multiple participants that can be reduced to a direct mechanism.

Saito Consensus is an indirect mechanism that is not reducible to a direct mechanism via the Revelation Principle. This impossibility emerges because conversion would require agents to reveal their supply and demand preferences at all prices levels for an effectively infinite combination of collusion and in-network goods and on an infinitely granular time preference curve.

The informational problem that makes conversion impossible is not just the extreme multi-dimensionality of utility available for trade in the mechanism. It also emerges from the way the individual preference curves end up jagged and discontinuous because of the potential for participants to shift temporarily at arbitrary points between being producers and consumers of different combinations of goods, creating jagged spikes that cannot be assumed not to exist if agents have not fully revealed their preference. The fact that the "hinge" good that permits granular trade-offs to be made efficiently is infinitely granular (time preference) then blocks generalizing assumptions that could otherwise assist in compressing the preference space.


### 5. Leonid Hurwicz (1972)

Hurwicz's seminal paper *The Design of Mechanisms for Resource Allocation* pointed out that in informationally decentralized mechanisms where communication between agents is needed prior to resource allocation, only mechanisms that can induce participants to share private preferences truthfully can be considered *incentive compatible* (i.e. robust to strategic manipulation by rational agents in expectation).

> These results show that the difficulty is due not to our lack of inventiveness, but to a fundamental conflict among such mechanism attributes as the optimality of equilibria, incentive-compatibility of the rules, and the requirements of informa- tional decentralization. Concessions must be made in at least one of these directions.

In Saito Consensus, the "pre-exchange messaging step" that is needed for agents to form price expectations and thus strategies is mediated through the blockchain itself and can only be manipulated through the sending of fee-bearing messages. And the cost that the publisher of this message must pay increases if it pushes the network into a less efficient equilibrium.

The cost of speech now depends on the content of the message. An asymmetrically higher cost is charged for false speech (state transitions which push us away from welfare-optimal outcomes), undermining the impossibility of implementing those equilibria in informationally decentralized conditions. Saito Consensus achieves incentive compatibility by fulfilling the requirements Hurwicz establishes through the indirect and decomposable optimization process he referred to generally as the "Greed Process".

<br> 

### Conclusion

The foundational impossibility results that computer scientists and economists developed in the 1970s and 1980s emerged out of the assumption that *processes* in computer systems were purely technical processes that could be costlessly manipulated by attackers. This resulted in the emergence of impossibility results based on the assumption that *malicious processes* could not be punished within consensus mechanisms as soon as they the same implicit "voting power" as honest nodes.

This assumption remains true in proof-of-work and proof-of-stake mechanisms, since those mechanisms lose the ability to punish attackers in majoritarian conditions. But there is no reason to consider this problem unsolvable. Subsequently impossibility results have not gone back to revisit the fundamentals examined in the 1980s, and have instead assumed that they must continue to hold, despite the shift to mechanisms that maintain their own unit-of-value and can punish participants without reference to external cost structures.



