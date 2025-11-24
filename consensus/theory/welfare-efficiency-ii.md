---
title: Implementing Welfare Efficiency via Saito Consensus
description: 
published: true
date: 2025-11-24T22:07:46.619Z
tags: 
editor: markdown
dateCreated: 2025-11-24T21:04:59.989Z
---

# Welfare-Increasing Costly Signals in Saito Consensus

### Relevant Papers
- Hurwicz (1972, 1979), *On Informational Decentralization*  
- Jackson (2001), *A Crash Course in Implementation Theory*  
- Milgrom & Weber (1982), *A Theory of Auctions and Competitive Bidding*  
- Parkes (2001, 2006), *Iterative Combinatorial Auctions*  

---

Saito Consensus is built around a simple insight taken directly from classical implementation theory: **actions with observable consequences can serve as messages in a mechanism**. 

The purpose of this page is twofold. We first show that achieving welfare optimality requires an expansion of the message space beyond costless type reports. We then show that how Saito implements this permits the mechanism to naturally filter out welfare-reducing deviations. 

This provides a conceptual way to understand how Saito can implement a welfare efficient outcome as a decentralized mechanism. We start by conceptualizing a version of the mechanism with the smallest possible message space.


## 1. The Baseline Mechanism

Without the ability to cryptographically sign transactions, Saito regresses to a baseline mechanism with:

- no coordination or joint bids,  
- no manipulation of propagation topology,  
- no side-benefits exchanged between users and producers.

Under this much simpler mechanism, users cannot secure faster inclusion at a lower price by bundling low-fee transactions into portfolio bids. This makes welfare-increasing trades which affect time and blockspace impossible.

Likewise, without the ability to take joint action in the assembling of portfolio blocks, it becomes irrational for agents to provide each other with collusion goods. Welfare increasing trades for complementary forms of collusion utility are thus also irrational in this simplified mechanism.

## 2. Expanding the Message Space

Implementing a welfare-efficient equilibrium requires our mechanism to offer a way for agents to make welfare-increasing trade-offs. This requires an expansion in the message space in which actions can carry welfare-relevant information. But in order for welfare-increasing proposals to dominate in equilibrium, the actions within this expanded part of the message space must impose real opportunity costs.

Saito accomplishes this by adding cryptographic routing signatures to transactions. As Hurwicz emphasized, and as we discuss in our page on [direct and indirect mechanisms](/consensus/theory/indirect-mechanisms), this mechanistic expansion fits the strict requirements of implementation theory for messages within decentralized mechanisms:

- they may be observable consequences of actions,
- they may encode costs or opportunity costs,  
- they may reflect strategic choices within the mechanism

Cryptographic routing signatures create environmental traces that are verifiable within the mechanism. And because the mechanism conditions rewards based on these signals (such as issuing routing payouts to particular nodes) these signals become part of the **message space**.

More importantly, routing signatures impose a real cost on agents within the mechanism, one that allows them to offer welfare-increasing trades that the counterparty can and will only settle if the gain is mutually beneficial.

## 3. Routing is Costly?

In our baseline mechanism, the only participant eligible for the routing payout is the creator of the single transaction in the block. Users can treat the routing payout as a refund in expectation.

But once we have the ability to generate portfolio bids, signing a transaction to a peer provides them with a probabilistic chance of collecting the routing payout. This dilutes the sender's claim on the routing payout: the refund that would otherwise accrue exclusively to them is now shared probabilistically with that peer, which means that routing creates a real opportunity cost and is only rational when the expected gain from joint action exceeds the refund value surrendered. Since nothing in the mechanism compensates a sender for a lost share of the refund, any routing choice that reduces joint welfare produces a strictly worse payoff for the sender.

Nonetheless, while benefits can be communally negotiated, offering cooperation can never force a loss on participants, as the original sender can always submit their shared transaction directly to the mechanism to bid directly for a block.

This creates a dynamic where the only situation in which participants will route transactions to other peers is if the cost of doing so (reduced claim on the probabilistic refund) is exceeded by the welfare-increasing gain enabled through joint action within the mechanism.

And powerfully, the mechanism allows each form of utility it offers to be traded off against the others through these mechanisms. The trilemma it creates gives agents a continuous space of costly actions through which they can express high-dimensional private preferences. Optimization is possible because expressing richer preferences always involves a sacrifice in at least one utility dimension, preserving the principle that welfare-increasing signals are cheap, but welfare-decreasing ones are expensive.


## Conclusion: Welfare-Increasing Deviations Are the Only Profitable Ones

In equilibrium, every profitable deviation corresponds to a welfare-improving trade, because routing is only rational when the sender and receiver jointly benefit, Saito fulfills Hurwicz’s requirement that decentralized mechanisms identify and implement precisely the proposals that increase welfare.

Attempts to exploit the expanded message space in ways that reduce welfare fail endogenously. Any routing choice that does not generate compensating gains through cooperative action simply destroys refund value and increases cost, or forces participants to fallback on non-cooperative strategies to prevent loss.

As a result, the mechanism never enables new profitable deviations that reduce welfare. The opportunity cost created by expanded competition over the routing payout ensures that any harmful deviation results in a strictly worse payoff. As a result, Saito enlarges the set of possible improvements without enlarging the set of profitable harmful actions.

## Final Synthesis

Saito’s welfare-efficiency rests on four core insights:

- message-space expansion allows welfare-increasing proposals

- costliness ensures only such proposals survive equilibrium.

- routing signatures provide verifiable signals needed to distinguish genuine proposals from empty reports.

- the chain aggregates these proposals into Pareto-efficient outcomes.

This lets Saito implement decentralized welfare efficiency without violating classical impossibility results. The solution emerges precisely because it operates in an indirect, action-based domain outside the limits of direct mechanisms and their limitations.