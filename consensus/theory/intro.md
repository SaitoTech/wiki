---
title: Introduction to Saito for Theorists
description: 
published: true
date: 2026-08-08T03:33:14.821Z
tags: 
editor: markdown
dateCreated: 2025-11-24T09:35:00.976Z
---

# What is New

Saito makes **adversarial state transitions more expensive to propose than honest ones** in expectation. This change eliminates what kinds of profitable deviations are possible and allows the mechanism to implement at least one social choice rule that is not feasible under symmetric-cost models such as standard POW and POS mechanisms. 


## Impossibility Results

Existing impossibility results in distributed systems appear to assert that this property is not achievable, however these results are based on assumptions that do not apply to Saito Consensus:

- **Symmetric proposal costs:** most models treat the cost of proposing a block or state transition or publishing another equilibrium-affecting message as identical in expectation between adversarial and honest nodes.

- **Unobservable Contribution:** traditional models assume the mechanism cannot observe or verify which agents performed value-creating actions, and therefore cannot condition costs or rewards on those actions.

- **Exogenous Feasibility:** models assume that the feasibility and cost of proposing a state transition are fixed and independent of the topology or efficiency of the message-passing substrate.

In computer science these assumptions underlie all standard impossibility results in distributed systems and mechanism design. Bracha–Toueg (1985) use this assumption to assert maximum theoretical tolerance of distributed systems to adversraial actors, Dwork–Lynch–Stockmeyer (1988) uses it for partial synchrony assumptions in symmetric-cost models, while Babaioff et al. (2012) explicitly prohibit strategic routing in a topological impossibility claim on routing payouts.

In economics, a parallel assumption appears in the mechanism design literature. Beginning with Hurwicz (1972) and developed through Myerson, Maskin, and Holmström, the Revelation Principle is built on the premise that all messages are costless to send, and any mechanism that claims to implement an outcome must tolerate the existence of unverifiable and cost-free misreports. These results do not apply to mechanisms in which communication is itself strategic.

## Cryptographic Routing Signatures

The specifical technical innovation in Saito that allows it to skirt these impossibility results is the introduction of cryptographic routing signatures, which turn what would otherwise be "cheap talk" reports into verifiable evidence that can be conditioned on by mechanisms.

Three structural features stand out:

1. **Routing Signatures and Observable Forwarding:** every transaction carries a cryptographically-verifiable record of its forwarding path which makes the contribution of each node in the path observable in a way that is impossible in blockchains without such signatures.

2. **Diverging Routing-work Operators:** Each fee-bearing transaction is decomposed into position-weighted routing work. This allows a single routing path to be evaluated through two valuation operators which diverge as path-length grows, giving the mechanism a lever with which to impose higher costs on inefficient nodes in sybil-inflated routing paths.

3. **Topology Drives Feasibility.** Inefficient or sybil-inflated routing paths are strictly dominated because unnecessary message-passing raises costs faster than they raise expected rewards.

Taken together, these primitives produce the asymmetrically costly state transitions described in Section #1. Proposal cost is tied directly to routing efficiency, while the chain-selection process favors blocks whose routing paths minimize inefficiency.

As a result:

- A coalition attempting to orphan an honest block must mimic the honest block’s efficiency, which requires spending more of its own funds than the honest block producer had to spend.

- The attacker’s costs are certain, while his expected refunds are fractional and probabilistic.

- Orphaning also refunds the honest producer’s costs while leaving the attacker with sunk, unrecoverable expenses on their own proposed chain.

With appropriate design parameters, this inherent efficiency gap makes adversarial reorganization loss-making in expectation even when attackers control a large fraction of the network’s resources. This is the economic core of Saito-class consensus.

