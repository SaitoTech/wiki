---
title: Implementing Welfare Efficiency via Saito Consensus
description: 
published: true
date: 2025-11-24T21:04:59.989Z
tags: 
editor: markdown
dateCreated: 2025-11-24T21:04:59.989Z
---

# Message Space Expansion and Costly Signals in Saito Consensus

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

Implementing a welfare-efficient equilibrium requires our mechanism to offer a way for agents to make welfare-increasing trade-offs different forms of utility provisioned through the mechanism. This requires an expansion in the message space.

Saito accomplishes this by adding cryptographic routing signatures to transactions. As Hurwicz emphasized, and as we discuss in our page on [direct and indirect mechanisms](/consensus/theory/indirect-mechanisms), messages need not be costless type reports:  

- they may be observable consequences of actions,
- they may encode costs or opportunity costs,  
- they may reflect strategic choices within the mechanism

The cryptographic routing signatures Saito adds create  environmental traces that are verifiable within the mechanism. And because the mechanism conditions rewards based on these signals (such as issuing routing payouts to particular nodes) these signals become part of the **message space**.

This expansion of the message space is not like the expansion of the message space in a direct mechanism, however, as exploiting it requires agents to bear a known cost. The existence of this cost is what penalizes welfare-reducing trades.

# 3. Routing is Costly?

In our baseline mechanism, the only participant eligible for the routing payout is the creator of the single transaction in the block. Users can treat the routing payout as a refund in expectation.

Once we have the ability to generate portfolio bids, sharing a transaction with a peer provides them with a probabilistic chance of collecting the routing payout, which is a potential cost for the transaction originator and a potential benefit for the recipient. It is the fact that this cost can never be welfare-reducing (the original user can still use the same UTXO to produce a block)


expectation of payout to other nodes. 
The addition of cryptographic routing signatures and the ability of producers to create portfolio bids expands the message space. We move from a mechanism that collects a simple fee report to one with a multi-dimensional message space:

- fee
- broadcast scope
- timing, self-routing, collusion structure, portfolio formation)


This expanded space is what allows Saito to capture high-dimensional preferences.

---

# 4. Why Expressing These Messages Requires Costly Actions

It is essential to distinguish between:

- **the expanded message space**, which is just a set of possible signals, and  
- **actions taken within that space**, which may be costly.

The message space itself is not costly to define.  
What is costly are the actions that generate messages inside it.

Examples:

- Strong broadcast incurs greater opportunity cost in routing.  
- Private broadcast reduces competition but increases time risk.  
- Routing signatures require work and forgo alternative refunds.  
- Coordinating a portfolio bid redistributes surplus and requires joint action.  
- Producing a block privately forfeits routing income.  

Thus:

> **High-dimensional preferences can only be expressed by sacrificing one form of utility to obtain another.**

This is made possible by the mechanism’s inherent **trilemma**:

- blockspace vs. time  
- time vs. collusion utility  
- collusion utility vs. blockspace  

The trilemma ensures that richer signals cannot appear unless a user has preferences strong enough to justify the cost.

---

# 5. Welfare-Relevant Features of the Expanded Message Space

Because expression of a high-dimensional preference requires real expenditure or opportunity cost, Saito naturally filters messages:

- If expressing a preference **increases the user’s welfare**, the user will bear the cost.  
- If expressing it **reduces welfare**, the user will not take the action.  
- If expressing it is **welfare-neutral**, the mechanism’s dynamics often drive such signals out of equilibrium.

This implements a form of **welfare-improving revealed preference**:

- costly signals appear only when they correspond to welfare-improving deviations,  
- welfare-reducing deviations are automatically suppressed,  
- the chain aggregates the surviving actions into efficient combinations.

This structure is why routing-work mechanisms can implement efficient combinatorial allocation in decentralized environments where full type revelation is infeasible.

---

# 6. Summary

- A *message space* is the set of signals the mechanism can condition outcomes on.  
- In Saito, many messages are produced by **actions** with **verifiable consequences**.  
- Expanding the message space allows users to express preferences over blockspace, time, and collusion goods.  
- But expressing these higher-dimensional messages requires **real economic cost**.  
- This ensures that only **welfare-improving** deviations are expressed in equilibrium.  
- The mechanism therefore implements **Pareto-efficient allocations relative to the informational topology of the network**.

This forms the conceptual basis for Saito’s welfare-efficiency claims.

---
