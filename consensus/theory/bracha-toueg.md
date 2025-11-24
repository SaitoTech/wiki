---
title: Bracha and Toueg
description: 
published: true
date: 2025-11-24T23:35:37.595Z
tags: 
editor: markdown
dateCreated: 2025-11-24T23:31:21.068Z
---

# Bracha–Toueg (1985)

Bracha and Toueg’s 1985 paper is one of the foundational results in distributed computing, showing that in an **asynchronous network with Byzantine faults**, no reliable broadcast protocol can guarantee both safety and liveness once the number of adversarial processes reaches a critical threshold. The intuition behind their proof is simple: in a world where **messages are free**, **equivocation is free**, and **no process can distinguish delay from malice**, correctness cannot be enforced.

Routing-work mechanisms such as Saito fall **outside this model** because they remove the symmetry that Bracha–Toueg assume must exist. In Saito, sending conflicting messages is not free and actually imposes *asymmetric, actor-specific economic cost*. This shifts the system from the “pure message-passing model” assumed by Bracha and Toueg into a hybrid economic–computational regime where the impossibility results no longer apply.

The remainder of this page explains this in more depth, covering (1) what Bracha–Toueg actually proves, and (2) why the assumptions of their impossibility theorem do not hold in any mechanism — such as Saito — that uses **costly, behavior-generated signals** to drive incentive compatible outcomes.

## 1. What Bracha–Toueg Actually Show (1985)

Bracha and Toueg consider an asynchronous distributed system with:

- **n processes**
- **up to f Byzantine processes**
- **arbitrary network delay**
- **messages that are delivered reliably but at unbounded delays**
- **local computation that is free**
- **message transmission that is free**
- **no source of asymmetry other than process IDs**

Their model assumes that every process behaves as a deterministic state machine, responding automatically and without cost to any message received over the network:

> “In an atomic step a process may receive a message, perform an arbitrarily long local computation, and then send a finite set of messages. The computation and the messages are prescribed by the protocol as a function of the message received and the local state.”  
> — *Bracha–Toueg (1985)*

Under these constraints they prove:

**reliable broadcast is impossible if f ≥ (n−1)/2**

This impossibility result is driven by one factor:

**Byzantine processes can equivocate freely without penalty**


## 2. Why the Bracha–Toueg Assumptions Fail in Saito

The underlying reason that costless equivocation is so damaging in this model is simple. Because bad actors can send different, conflicting messages to different recipients without penalty, honest processes cannot distinguish delay from deception and coordinate to punish deceivers.

And this is why routing-work mechanisms like Saito Consensus break the core symmetry that Bracha–Toueg, since proposing different blocks creates **different economic costs** which must be borne by the proposer, depending on:

- the set of transactions included in the block
- the way in which they were routed into the network
- if any fees involved were contributed by the proposer

Sending different “views of the chain” to different peers is also *not free*:

- it requires burning money to propose fraudulent blocks, or
- it destroys the sender’s expected routing payout, or
- it provokes competitive block production that lowers profit, or 
- it changes the price of block creation or fee unlock in a way that is harmful to the equivocator.

These changes fundamentally break the “all deviations are free” assumption which drives the impossibility proof, and make the proof non-binding on Saito Consensus.


## 3. Conclusion

Bracha–Toueg proves a powerful impossibility result — but only for systems where:

- all deviations are costless,  
- messages carry no economic meaning,  
- Byzantine actors face no penalty,  
- and honest actors cannot distinguish malice from delay.

Routing-work mechanisms like Saito eliminate these assumptions by switching to an **action-based economic environment** where:

- equivocation is expensive,  
- honest behavior is rewarded,  
- the network conditions outcomes on real, verifiable work,  
- and the symmetry needed for classical impossibility results is absent.

As such, **Bracha–Toueg does not apply to Saito Consensus** in the computer science domain, just as [Myerson–Satterthwaite and Green–Laffont](/consensus/theory/welfare-efficiency) do not apply in the economic domain.

