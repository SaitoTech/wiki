---
title: Bracha and Toueg
description: 
published: true
date: 2025-11-24T23:31:21.068Z
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

The underlying reason that costless equivocation is so damaging is simple. Because bad actors can send different, conflicting messages to different recipients without penalty, honest processes cannot distinguish delay from deception and cannot coordinate to punish deceivers.

## 2. Why the Bracha–Toueg Assumptions Fail in Saito

Routing-work mechanisms like Saito Consensus break the core symmetry that Bracha–Toueg rely on:

### **A. Messages are not free.**

Proposing different blocks create **different economic costs** which must be borne by the proposer, depending on:

- the set of transactions included in the block
- the way in which they were routed into the network
- if any fees involved were contributed by the proposer

### **B. Equivocation is economically asymmetric.**  

Sending different “views of the chain” to different peers is *not free*:

- it requires burning money to propose fraudulent blocks, or
- it destroys the sender’s expected routing payout, or
- it provokes competitive block production that lowers profit, or 
- it changes the price of block creation or fee unlock in a way that is harmful to the equivocator.

### **C. The environment creates real, observable consequences.**  

Because Saito uses **costly, behavior-generated signals**, the act of producing, forwarding, or withholding transactions:

- changes the actor’s economic payoff,  
- changes the payoffs of others,  
- and is **verifiable** through cryptographic signatures and chain state.

This breaks the “all deviations are free” assumption which drives the impossibility proof.


## 3. Conclusion

In Saito Consensus a Byzantine actor can still misbehave — but they cannot do so *for free*, since every deviation consumes real resources. And that means they cannot do it in perpetuity.

Bracha–Toueg proves a powerful impossibility — but only for systems where:

- all deviations are costless,  
- messages carry no economic meaning,  
- Byzantine actors face no penalty,  
- and honest actors cannot distinguish malice from delay.

Routing-work mechanisms like Saito eliminate these assumptions.  
They operate in an **action-based economic environment** where:

- equivocation is expensive,  
- honest behavior is rewarded,  
- the network conditions outcomes on real, verifiable work,  
- and the symmetry needed for classical impossibility results is absent.

Therefore, **Bracha–Toueg does not apply to Saito Consensus**, just as [Myerson–Satterthwaite and Green–Laffont](/consensus/theory/welfare-efficiency) do not apply in the economic domain.

