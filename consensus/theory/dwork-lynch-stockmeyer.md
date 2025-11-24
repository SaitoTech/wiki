---
title: Dwork-Lynch-Stockmeyer
description: 
published: true
date: 2025-11-24T23:40:21.395Z
tags: 
editor: markdown
dateCreated: 2025-11-24T23:40:21.395Z
---

# Dwork–Lynch–Stockmeyer (1988)

Dwork, Lynch, and Stockmeyer’s 1988 paper (“DLS”) is the canonical impossibility result for consensus in **partially synchronous** networks. They show that when the system alternates unpredictably between synchronous and asynchronous periods, no deterministic protocol can guarantee both safety and liveness in the presence of Byzantine faults.

The force of the DLS result comes from its **message–passing model**, in which:

- communication is free,  
- equivocation is free,  
- adversaries face no economic constraints,  
- processes are symmetric automata, and  
- local computation is costless.  

Routing-work mechanisms like Saito lie **outside this model**. Saito adds *persistent economic asymmetries* to the message-passing environment: proposing different blocks has different costs, misbehavior alters the burn fee, routing incentives break structural symmetry, and equivocation is economically punished even when it cannot be cryptographically detected.

This page explains (1) what DLS actually proves, and (2) why its assumptions do not hold for Saito Consensus.

---

## 1. What DLS Prove (1988)

Dwork, Lynch, and Stockmeyer investigate consensus in a **partially synchronous network**, where:

- message delays may be arbitrarily long during “asynchronous periods,”  
- but eventually the network satisfies timing bounds during “synchronous periods,”  
- and processes do not know when synchrony begins.  

Processes are modeled exactly as in Bracha–Toueg:

- identical deterministic state machines,  
- free local computation,  
- free messaging,  
- free equivocation,  
- no asymmetry except process identity.

Under these assumptions they prove:

> **No deterministic protocol can achieve both safety and liveness in the presence of Byzantine faults in a partially synchronous system.**

The proof relies critically on two structural facts:

1. **Byzantine nodes can produce arbitrary, costless, conflicting behavior.**  
2. **Honest nodes cannot distinguish a slowly functioning system from a malicious one.**

When equivocation is free and indistinguishable from delay, consensus is impossible.

---

## 2. Why DLS Does Not Apply to Saito Consensus

The DLS impossibility result rests entirely on *symmetry* and *costless deviation*.  
Routing-work mechanisms break both.

### **A. Not all messages are symmetric**

In Saito, proposing a block is not a uniform operation:

- Proposing a block containing well-routed transactions is **cheaper**.  
- Proposing a block containing poorly-routed or self-created (“fake”) transactions is **more expensive**.  
- The burn fee adjusts dynamically and reflects the economic cost of congestion and competition.

Thus:

> **Sending different block proposals has different economic costs for different actors.**

This violates the core assumption of the DLS model, where *all processes incur identical cost for identical actions*.

---

### **B. Equivocation is economically costly**

In DLS, a Byzantine actor can send inconsistent messages “for free.”

In Saito:

- Proposing two blocks simultaneously destroys expected routing payouts.  
- Proposing bad blocks increases burn fees that harm the equivocator.  
- Equivocation attracts competition: honest nodes can outbid and replace malicious blocks.  
- The routing-payment mechanism routes surplus away from malicious strategies.

Thus:

> **Equivocation is not free — it is self-punishing.**

DLS explicitly assumes the opposite.

---

### **C. Safety/liveness tradeoffs depend on economic incentives, not timing**

DLS impossibility stems from delay ambiguity: no node can tell if the network is slow or Byzantine.

Saito decouples safety and liveness from timing by grounding them in **incentive gradients**, not message timing:

- Routing signatures provide proof of work-like forward progress.  
- Block proposals reveal real economic preferences.  
- Misbehavior decreases attacker profit in expectation, regardless of timing.

This moves the mechanism from a “pure timing” domain to an “economic+timing” hybrid domain that DLS does not analyze.

---

### **D. Saito’s consensus rule is not deterministic-state-machine consensus**

DLS assumes a deterministic transition system:

**(state, message) → new state + new messages**


Saito’s block-production game is **not** such a protocol:

- It is a *market*, not an automaton.  
- Nodes choose actions based on private valuations, not deterministic transitions.  
- Outcomes depend on equilibrium behavior, not state-machine execution.  
- Deviations incur real costs.

This violates the syntactic definition of a DLS-style protocol.

---

## 3. Conclusion

Dwork–Lynch–Stockmeyer prove an impossibility theorem for a world in which:

- messages are free,  
- equivocation is free,  
- actors are indistinguishable,  
- timing is the only source of uncertainty,  
- and consensus is defined as deterministic state evolution.

Routing-work mechanisms break all of these assumptions.  
Saito introduces:

- economic asymmetry,  
- costly deviations,  
- incentive-based filtering of malicious behavior,  
- and behavioral messages that carry welfare information.

Thus, **DLS does not apply to Saito Consensus**, just as [Bracha–Toueg (1985)](/consensus/theory/bracha-toueg) does not, and just as classical economic impossibility results (e.g. [Myerson–Satterthwaite & Green–Laffont](/consensus/theory/welfare-efficiency)) do not in the economic domain.

Routing-work consensus is simply **not in the domain of models that DLS — or any message-only impossibility theorem — was designed to rule out**.

