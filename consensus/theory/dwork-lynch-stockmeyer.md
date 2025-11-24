---
title: Dwork-Lynch-Stockmeyer
description: 
published: true
date: 2025-11-24T23:57:35.675Z
tags: 
editor: markdown
dateCreated: 2025-11-24T23:40:21.395Z
---

# Dwork–Lynch–Stockmeyer (1988)

Dwork, Lynch, and Stockmeyer’s 1988 paper (“*Consensus in the Presence of Partial Synchrony*”) establishes one of the most influential impossibility results in distributed systems, showing that **deterministic consensus is impossible in a fully asynchronous setting** unless the system eventually behaves with a degree of synchrony — but with even one faulty process such synchrony cannot be guaranteed.

Saito Consensus does not evade this impossibility result so much as live outside the scope of its applicability completely as a non-deterministic mechanism. Since this is a point that is often overlooked by those working on distributed systems, this page provides a quick review of why exactly this result does not apply.

Critically, the DLS model assumes:

- a **fixed, finite set of processes**,  
- each running a **deterministic state machine**,  
- where every state transition and message output is **fully determined** by the protocol and prior inputs,  
- and no **exogenous, strategic, or utility-driven actions** enter the system.

Saito Consensus is not bound by these results as it is not a "deterministic" protocol in the DLS sense. It is an open, permissionless economic mechanism in which:

- anyone can introduce a new transaction at any time,  
- anyone can choose different routing strategies,  
- anyone can produce a block whenever they are willing to pay the burn fee,
- block production costs vary across actors,  
- and system evolution depends on **strategic, utility-driven behavior**, not fixed state transitions.

As a result of these changes, the next state of the chain is **not** a deterministic function of the previous state but depends on *exogenous economic actions* taken by unpredictable, heterogeneous participants, and participants who are continually motivated to use the mechanism and submit new transactions into it for settlement.

Because DLS applies **only to deterministic protocols** with no external actions, it cannot be used to evaluate or constrain Saito Consensus. The underlying model is simply not expressive enough to describe an open, strategy-driven mechanism like Saito in the first place.

## Conclusion

DLS is a foundational result for deterministic algorithms in adversarial asynchronous networks. Saito is **not** such a protocol. It is an open economic game with strategic participants and continuous external inputs. As such, **the DLS impossibility result does not apply** to Saito Consensus.
