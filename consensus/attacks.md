---
title: Technical Attacks
description: How Saito Consensus improves defense against common technical attacks
published: true
date: 2025-11-23T15:13:05.725Z
tags: 
editor: markdown
dateCreated: 2025-11-23T14:08:23.537Z
---

# Attacks on Permissionless Consensus

Permissionless blockchains must defend against a number of attack vectors. These attacks exploit the ability of agents in such mechanisms to participate under many identities and collude with other agents. This page reviews these attack vectors and describes, technically, how Saito addresses them.

Readers interested in a more academic treatment of these problems should note that multiple academic papers exist which assert that some of these problems are unsolvable. For a discussion of these results with an academic explanation of why they do not bind Saito, please see our page on [academic introduction](/consensus/theory).


## 1. Majoritarian Attacks

The **51% attack** is often described as the ability to re-organize the blockchain. This definition is misleading: the property that disappears at the 51% control point in Bitcoin is not whether the blockchain can be reorgnized but whether the mechanism provides an economic deterrent against such attempts.

Saito eliminates majoritarian attacks in this sense -- it guarantees that any attempt by even a majoritarian coalition to increase their share of blocks on the longest chain (a share that must increase when honest blocks are orphaned, as at least one honest block must be replaced by an attacker block) requires the orphaning party or adversarial coalition to bear losses in expectation.

The underlying problem thus appears when reorganizing the chain is *not more expensive than extending it* or *the cost of producing all blocks are identical in expectation*, such that it costs the same amount for an attacker to orphan a block that it took the honest node to produce it originally. This symmetry of chain-extension costs is what makes majoritarian attacks feasible in Proof-of-Work and Proof-of-Stake systems:

- orphaning honest blocks costs no more than building on them  
- majority coalitions can cheaply create competing chains  
- double-spends and deep reorganizations become economically rational 

Saito removes this attack by ensuring it is also costly (in expectation) to produce blocks that push more efficiently-produced blocks off what would otherwise be the honest chain.

The solution is easiest to see by considering what happens when an attacker simply ignores blocks produced by other nodes, and extends a fork without accepting any contributions from other participants.

In this case, the fee-throughput of the network drops (there must be at least one transaction in the honest block that was not available to the attacker if their block was produced second). While this lowers the fee throughput of the attacker's fork, the cost of hashing golden tickets (unlocking payouts) remains at the pre-attack equilibrium level.

In short, attackers are able to burn a smaller amount of fees to continue extending the chain. But the relative cost of capturing those fees (hashing costs as a percentage of total fees available for payout) spikes significantly, as the overall hashing burden is spread over fewer transaction fees that do not belong to the attacker or attacking coalition.

Attackers are strictly better not orphaning blocks, and maximize their profitability when they permit other honest nodes to contribute fees to the chain. This inequality holds up to the point the attacker holds 100% of the first-hop fee throughput flowing into the network, i.e. in any situation characterized by informational decentralization.

As a result:

- costless reorganizations are impossible  
- majoritarian attacks lose money in expectation  
- controlling 51% (or even 99%) does not permit a profitable attack  

Fixing this restores the economic security that POW and POS lose when a single coalition gains majority control: the ability of users to increase cost-of-attack on their own transactions by waiting for more confirmations.

---

# 2. Sybil Attacks

A sybil attack occurs when an adversary creates multiple identities in a permissionless network. In Saito, sybilling is economically irrational because the consensus mechanism imposes an implicit tax on every extra routing hop:

- each hop halves the routing work available to all later hops

- deeper paths pay the same burn cost while providing less routing work in equilibrium

- and including high-hop transactions is strictly more expensive for block producers

Any dilution of routing-work increases the share of the block reward that is distributed to non-routers for the block containing the sybilled transaction. This creates an implicit tax on routers who pad their transactions with unnecessary hops. Any sybil that clones itself in the routing path makes that path worse for itself.

This produces two immediate consequences:

 - Sybils that collude must pass messages between identities, forcing them to burn more tokens to produce blocks than a single efficient identity would need to burn ceteris paribus.

 - Sybils that do not collude compile fees inefficiently, since they cannot benefit from inbound transaction flow that would be available to "both" nodes if they produced blocks under a shared public key.

In short: it is always more profitable for agents to participate in routing mechanisms under one identity as the mechanism has a bias towards informational efficiency and compact routing paths. This bias is expressed as an indirect tax on both non-cooperative behavior as well as deliberately inefficient routing strategies.

For a formal economic proof of sybil-resistance and a more academic treatment of the underlying economics, see  
**→ [A Simple Proof of Sybil-Proofness](/consensus/theory/sybil-proof)**.

---

# 3. Censorship Attacks

Censorship attacks occur when a node or coalition selectively drops, delays, or refuses to include user transactions. They can also be used to describe situations in which block producers refuse to accept valid blocks proposed by competitors.

In Saito, censorship is **self-punishing** due to the structure of routing work. We briefly review the two technical mechanisms that punish censorship of user-transactions and producer-blocks respectively.

### Transaction Censorship

1. **Censorship lowers block-producer profitability.**  
   Block producers earn routing work and payouts by including user-sourced transactions. Dropping fee-competitive transactions makes them less efficient at producing blocks and less profitable in the payout lottery.

2. **Censored transactions accumulate ATR payouts.**  
   If a user’s UTXO cannot be moved because a transaction containing it is censored, this transaction will eventually receive ATR payouts. These payouts come from the fees collected by the attackers, meaning **censorship transfers money from the attacker to the censored user** while reducing the attacker's own share of ATR payouts.

3. **Competitive routing dominates censoring routes.**  
   Routing nodes earn by forwarding traffic. Withholding or delaying transactions destroys the competitiveness of the routing path. Honest routing paths emergently outcompete censoring paths because forwarding increases revenue, while dropping transactions reduces it.

### Block Censorship

Routing signatures prohibit attackers from moving transactions sourced by other routing nodes into their own blocks. This means that attackers who refuse to permit honest nodes to contribute blocks lower the honest fee-throughput of the network.

While the cost in routing-work to produce blocks quickly recovers from the fall in fee-throughput, the difficulty of unlocking payouts cannot fall until multiple blocks go unsolved and unpaid.

The attacker who deliberately censors an honest block transfers to himself a higher cost of collecting the fees he is already collecting in payment, in perpetuity, unless he is willing to let the blocks he is proposing go unpaid, in which case he loses money that way.

In short, censorship in Saito is not merely discouraged — it is structurally **unprofitable** for attackers, whose act of censorship increases their costs and reduces their income available to pay.

---

# Summary

Saito’s defense against attacks is grounded in protocol-level economics:

- **Majoritarian attacks** fail because orphaning honest blocks is more expensive than extending the longest chain.
- **Sybil attacks** fail because redundant identities decrease profitability and routing signatures expose inefficiency.  
- **Censorship attacks** fail because they reduce the attacker’s competitiveness at making blocks (transaction censorship) or getting paid (block orphaning).

All three solutions arise directly from Saito’s use of cryptographically signed routing paths, independent of any need for external social coordination or benefits/penalities.

-----

For deeper theoretical discussion of these three topics as relates to the existing distributed systems literature, see our [academic introduction](/consensus/theory).
