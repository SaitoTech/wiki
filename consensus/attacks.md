---
title: Technical Attacks
description: How Saito Consensus improves defense against common technical attacks
published: true
date: 2025-11-23T14:08:23.537Z
tags: 
editor: markdown
dateCreated: 2025-11-23T14:08:23.537Z
---

# Attacks on Permissionless Consensus

Permissionless blockchains must defend against a number of new attack vectors. These attacks exploit the ability of participants to participate under many identities, collude with other participants in the network, or arbitrarily censor other users. This page reviews these attack vectors and describes, technically, how Saito addresses them.

Readers interested in the underlying economic and theoretical foundations of these attacks should notice that several academic papers exist which argue that some of these problems are unsolvable. For a discussion of these results with a more academic explanation of why they do not bind Saito, please see our page on [academic introduction](/consensus/theory).


## 1. Majoritarian Attacks

The **51% attack** is often described as the ability to re-organize the blockchain. This definition is misleading: the property that disappears at the 51% control point in Bitcoin is the fact that such attacks are economically costly to attackers in expectation.

Saito eliminates majoritarian attacks in this sense -- it cannot prohibit participants from burning money to attack the network, but it guarantees that any attempt to increase their share of blocks on the longest chain (a variable that must increase when honest blocks are orphaned) requires the orphaning party to bear losses in expectation.

The real problem appears when reorganizing the chain is *not more expensive than extending it*. This is what makes majority attacks feasible in Proof-of-Work and Proof-of-Stake systems:

- orphaning honest blocks costs no more than building on them  
- majority coalitions can cheaply create competing chains  
- double-spends and deep reorganizations become economically rational  

Saito removes this property.

### Saito’s Guarantee: orphaning is always more expensive than extending.

Because block production requires burning the routing work embodied in the transactions included in the blockchain:

- an honest node extending the chain pays the **equilibrium cost** (the burn fee)  
- an attacker trying to orphan a block must burn **all the routing work suppressed by the attack**, which is **strictly greater**  

This inequality holds even when the attacker controls a majority of network resources.

As a result:

- reorganizations are possible but **always costly**  
- costless reorganizations are impossible  
- majoritarian attacks lose money in expectation  
- controlling 51% (or even 99%) does not permit a profitable attack  

This property restores the economic security that PoW and PoS lose when a single coalition gains majority control.

---

# 2. Sybil Attacks

A sybil attack occurs when an adversary creates multiple identities to manipulate reward distribution or distort network structure. In permissionless networks, sybil resistance requires that creating extra identities provides no economic advantage.

Saito addresses sybil attacks at two layers:

## (a) Routing-Layer Sybils

Attackers may attempt to insert unnecessary hops into the routing path to appear as additional contributors of work.

Saito prevents this because:

- every hop in a routing path **dilutes the value** available to all hops following it  
- routing signatures reveal the full forwarding path  
- unnecessary hops reduce total profitability for the entire path  
- nodes therefore **purge parasitic peers**, since keeping them lowers their own yield  

A routing-layer sybil is not invisible and is not profitable. Nodes have straightforward economic incentives to route around and exclude such identities.

## (b) Identity Splitting by Block Producers

Block producers may attempt to split into multiple identities to bias payout selection or increase expected revenue.

This provides no benefit because:

- only **observed routing work** determines the share of rewards  
- routing work is tied to transaction fees collected from users, not to identity count  
- splitting identities does not increase routing work and therefore does not increase expected payout  

Sybil strategies fail because Saito pays only for **real, observable contribution**, not for the number of identities presenting it.

For a formal economic proof of sybil resistance, see  
**→ [A Simple Proof of Sybil-Proofness](/consensus/theory/sybil-proof)**.

---

# 3. Censorship Attacks

Censorship attacks occur when a node or coalition selectively drops, delays, or refuses to include user transactions. In many blockchains this can be profitable for block producers seeking MEV, fee extraction, or strategic advantage.

In Saito, censorship is **self-punishing** due to the structure of routing work and the ATR (Automatic Transaction Rebroadcast) mechanism.

### Why Censorship Fails in Saito

1. **Censorship lowers block-producer profitability.**  
   Block producers earn routing work by including user-sourced transactions.  
   Dropping transactions directly reduces the routing work they can burn to create blocks, making them less competitive.

2. **Censored transactions accumulate ATR payouts.**  
   If a user’s UTXO cannot be moved because it is censored, it will eventually receive ATR payouts.  
   These payouts come from the fees collected by block producers — meaning **censorship transfers money to the censored user**.

3. **Competitive routing dominates censoring routes.**  
   Routing nodes earn by forwarding traffic.  
   Withholding or delaying transactions destroys the value of their routing work.  
   Honest routing paths outcompete censoring paths because forwarding increases revenue, while dropping transactions reduces it.

4. **Coalitions cannot sustain censorship without sustained losses.**  
   A coalition attempting to starve a user must forgo block revenue, increase ATR liabilities, and reduce its own routing income.

Censorship in Saito is therefore not merely discouraged — it is structurally **unprofitable**.

---

# Summary

Saito’s defense against attacks is grounded in protocol-level economics:

- **Majoritarian attacks** fail because orphaning is more expensive than extending.  
- **Sybil attacks** fail because unnecessary identities decrease profitability and routing signatures expose contribution.  
- **Censorship attacks** fail because they reduce the attacker’s own block-production competitiveness and transfer value to the victim.

These properties arise directly from Saito’s routing-work consensus, independent of any social coordination or external assumptions.

For deeper theoretical discussion, see the  
**→ [Academic Introduction](/consensus/theory)**.
