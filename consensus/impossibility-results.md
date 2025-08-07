---
title: Impossibility Results
description: 
published: true
date: 2025-08-07T07:53:23.788Z
tags: 
editor: markdown
dateCreated: 2023-09-20T01:58:02.086Z
---

# Classic Impossibility Results

Saito Consensus sidesteps several impossibility results that affect other distributed consensus mechanisms. These allow the mechanism to achieve outcomes that are not possible with traditional approaches.

Please see our [technical explanation](/consensus) of consensus for a description of the mechanism itself. This page highlights how Saito avoids being bound by the classic impossibility results from economics and computer science which limit most other designs. It should be noted that this is not an argument that these papers are wrong **within the bounds of their assumptions** -- merely that these assumptions are not binding on routing mechanisms as routing mechanisms ellude their limitations.


<br>

### 1. On Bitcoin and Red Balloons (2011)

An influential [academic paper](https://arxiv.org/pdf/1111.2626) by Moshe Babaioff, Shahar Dobzinski, Sigal Oren and Aviv Zohar has claimed the impossibility of building distributed mechanisms which incentivize transaction propagation. Their paper specifically asserts that "there are no reward schemes in which information propagation and no self-cloning is a dominant strategy."

Saito Consensus solves this problem, offering a routing payout to P2P nodes that encourages nodes to share transactions with their peers, yet does not make self-cloning rational. The solution works because adding hops to transactions decreases the usefulness of those transactions for producing blocks, reducing the expected income of the attacker by more than the attacker can expect to earn through the expanded claim on payout from an additional routing hop. One assumption from this paper that Saito Consensus violates is the expectation that all nodes must have an equal probability and thus cost of producing the most efficient next block.

We have a [mathematical proof](https://github.com/SaitoTech/papers/blob/e32c51db6aae071a41b7e481d0f5ba6cd75ec12d/sybil/A_Simple_Proof_of_Sybil_Proof_Lancashire-Parris_2023.pdf) that routing work solves this problem in a three-hop routing path. To our knowledge the routing-decay and probabilistic payout solution offered by Saito Cosnensus remains the only known solution to this problem.

<br>

### 2. Roughgarden and Shi (2020)

A school of papers from Tim Roughgarden (Colombia) and Elaine Shi (Cornell) and others has emerged claiming the general impossibility of building incentive compatible blockchains. Saito Consensus offers a self-evident counter-proof to these claims as an indirect mechanism that implements a welfare-optimizing social choice rule.

These impossibility results assume all blockchains must be reducible to direct mechanisms in which incentive compatibility requires only the revelation by users of their private valuation for transaction inclusion. And yet Saito Consensus is a combinatorial auction that distributes at least three types of utility (transaction inclusion, speed-to-inclusion and collusion goods) in exchange for a single transaction fee that is non-scalar with regards to the private valuation of blockspace but scalar in combination over all three goods. The fact that users have private valuations for these co-mingled forms of utility is what frustrates the achievement of incentive compatibility in the academic models Saito breaks, and also the reason they fail to meet the requirements Hurwicz, Maskin and Myerson establish for proving the impossibility of achieving incentive compatibility across blockchain mechanisms generally.

A second problem with these results is that their authors require block producers to "faithfully implement" mechanisms, yet overlook that faithful implementation of any incentive compatible mechanism necessarily requires "faithful revelation" of all relevant private preferences. This pushes these papers into self-contradiction, as they also explicitly prohibit block producers from engaging in such forms of preference revelation through an additional and entirely arbitrary prohibition on their including self-generated transactions in blocks. As those familiar with Saito Consensus will know, the inclusion of such self-generated transactions is a form of preference revelation for block producers in our mechanism, and a form of competition for blockspace that forces users to act with greater strategic care: bid too lower and producers will switch from sellers to buyers because of their own time-preference! This limitation thus forces Saito Consensus out-of-model, as meeting the criteria for achieving impossibility becomes impossible.

Finally, we observe that these papers do not properly identify their social choice rule. While they implicitly adopt the social choice rule of the Vickrey auction ("efficient allocation") this social choice rule cannot be used in mechanisms where the supply of the good being distributed is subject to strategic manipulation. Switching to the more appropriate model for two-sided auctions ("efficient allocation and production") forces us into requiring higher-dimensional preference revelation as multidimensional forms of utility come into play and both supply and demand-side preferences must be disclosed for any direct mechanism to implement welfare-optimal outcomes.

Saito Consensus handles both forms of preference revelation indirectly: users reveal their bundled preference for three forms of utility through both the fee they choose and their transaction broadcast strategies (which indicate the existence of a welfare-increasing cooperative trade between the user and at least one block producer). Producers reveal their private cost structures through their willingness to include their own fee-bearing transactions in blocks, effectively redirecting surplus profits from the sale of collusion goods into a subsidy for either the welfare-improving forms of speed or collusion utility more highly valued by counterparties in the mechanism.


<br>

### 3. Bracha and Toueg (1985)

The paper *Asynchronous Consensus and Broadcast Protocols* by Bracha and Toueg shows that in an asynchronous system with **n** total processes, at most **(n−1)/2** processes can be adversarial. Their model assumes a network of processes that receive and respond to network messages automatically:

> In an atomic step of the system, a process can try to receive a message, perform an arbitrarily long local computation, and then send a finite set of messages. The computation and the messages sent are prescribed by the protocol, that is, a function of the message received and the local state.

In this model, nothing can stop malicious nodes from broadcasting messages that subvert consensus, and nothing can stop honest nodes from attempting to restore consensus. This creates the majoritarian vulnerability the paper argues is impossible to overcome: achieving consensus is a voting problem and whatever cohort can send the most messages wins.

In Saito Consensus the cost of proposing a block depends on the contents of its transaction set. Producers may be including and burning their own money at a loss depending on the strategy chosen. As a consequence, some messages cost more to propose in equilibrium than others. It is no longer possible to assume that messages which reduce the overall efficiency of fee-throughput are symmetrically costly to those which do not.

<br>

### 4. Roger B. Myerson and Mark A. Satterthwaite (1983)

The paper *Efficient Mechanisms for Bilateral Trading* by Roger B. Myerson and Mark A. Satterthwaite prove that it is impossible to achieve incentive compatibility in any bilateral trading (direct) mechanism, with results that are extensible through the Revelation Principle to any two-sided mechanism with multiple participants that can be reduced to a direct mechanism.

Saito Consensus is an indirect mechanism that is not reducible to a direct mechanism via the Revelation Principle. This impossibility emerges because conversion would require agents to reveal their supply and demand preferences at all prices levels for an effectively infinite combination of collusion and in-network goods on an infinitely granular time preference curve.

The informational problem that makes conversion impossible is not just the extreme multidimensionality of the types of utility available for trade in the mechanism. It also emerges from the fact that individual preference curves across this multidimensional space are jagged and discontinuous because of the potential to shift temporarily at arbitrary points between being producers and consumers of different goods, creating jagged spikes that cannot be assumed not to exist if agents have not fully revealed their preference. The fact that the "hinge" good that permits granular trade-offs to be made efficiently is infinitely granular (time preference) then blocks generalizing assumptions like curve monotonicity that could otherwise assist in reducing the preference space.


### 5. Leonid Hurwicz (1972)

Hurwicz's seminal paper *The Design of Mechanisms for Resource Allocation* pointed out that in informationally decentralized mechanisms where communication between agents is needed prior to resource allocation, only mechanisms that can induce participants to share private preferences truthfully can be considered *incentive compatible* (i.e. robust to strategic manipulation by rational agents in expectation).

> These results show that the difficulty is due not to our lack of inventiveness, but to a fundamental conflict among such mechanism attributes as the optimality of equilibria, incentive-compatibility of the rules, and the requirements of informa- tional decentralization. Concessions must be made in at least one of these directions.

In Saito Consensus, the "pre-exchange messaging step" that is needed for agents to form price expectations is mediated through the blockchain itself and can only be manipulated through the sending of fee-bearing messages. This act of publishing price-affecting signals is free for genuine consumers of those forms of utility, but -- due to the way consensus works -- expensive for those who have non-genuine purchase intent. We see that "false speech"  (spending your own money to manipulate price signals or supply) is more costly than speech which pushes the network towards an efficient price level where overall demand and supply is set only by genuine demand/supply preferences from other agents.

We can take a step further by conceptualizing Saito Consensus as a combinatorial auction for three goods (blockspace, time-to-settlement, ande collusion goods). As above, the mechanism can be seen to pull the price of the first two goods into equilibrium. The price of the third class of goods is then pulled into alignment through the mechanism because the mechanism itself forces it into an inverse relationship with the other two goods. Even those the mechanism cannot  a separate process known abstractly as Hurwicz' Greed Process, in which welfare-improving proposals (for collusion goods) 


Saito Consensus induces an emergens that the strategic information that users publishing of proposals necessarily involves a cost which is asymmetrically higher for false speech (state transitions which arbitrarily reduce efficiency) in equilibrium. In the process, Saito Consensus achieves incentive compatibility by fulfilling the requirements Hurwicz establishes for incentive compatibility with through its indirect and decomposable implementation of a decentralized optimization process he termed the "Greed Process".

<br> 

### Conclusion

The foundational impossibility results that computer scientists and economists developed in the 1970s and 1980s emerged out of the assumption that *processes* in computer systems were purely technical processes that could be costlessly manipulated by attackers. This resulted in the emergence of impossibility results based on the assumption that *malicious processes* could not be punished within consensus mechanisms as soon as they the same implicit "voting power" as honest nodes.

This assumption remains true in proof-of-work and proof-of-stake mechanisms, since those mechanisms lose the ability to punish attackers in majoritarian conditions. But there is no reason to consider this problem unsolvable. Subsequently impossibility results have not gone back to revisit the fundamentals examined in the 1980s, and have instead assumed that they must continue to hold, despite the shift to mechanisms that maintain their own unit-of-value and can punish participants without reference to external cost structures.



