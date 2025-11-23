---
title: What is Saito
description: An ELI5 description of what Saito Consensus is and why it matters...
published: true
date: 2025-11-23T10:51:54.600Z
tags: 
editor: markdown
dateCreated: 2025-11-23T10:51:54.600Z
---

### What Problem does Saito Solve?

Blockchains are distributed networks that need to pay for their own infrastructure. This means they need to collect fees from users, and somehow get those fees to the nodes that are running the network. In principle this sounds simple enough.

In practice this is one of the hardest problems in distributed systems. To pay the right nodes the right amount of money, a blockchain must be able to observe who is contributing actual value. But in a permissionless network where we only see the blocks contributed by "winners" participants have many ways to lie about the wrk they are doing, and hide (orphan) the work that others are doing. And there is no easy way to measure value creation.

Unable to solve this problem, the Bitcoin and Ethereum developers chose a workaround: they created an activity that was both expensive and objectively measureable (mining or staking) and decided to pay the nodes that did it. Although most developers were vaguely aware that mining and staking are extractive activities, they hoped that the people earning the rewards would voluntarily spend some portion on servicing the users that paid network fees. And when this didn't happen? By then developers had switched to arguing that infrastructure provision was the responsibility of the private sector not the consensus mechanism.

### The Underlying Problem is Extractive Economics

The inability of other consensus mechanisms to solve this problem is why they all converge into an economically-centralized state as they scale. The people responsible for running infrastructure monetize by controlling the transaction fees that flow into the network, and finding ways to leverage those flows into an outsized ability to collect the fees themselves. What started as a decentralized mechanism now coalesces into something that is centralized in practice by the economic need to pay for things that the consensus layer needs to survive but cannot pay for itself.

If you are interested in learning more about these economic problems, we have separate pages which describe the two major collective action problems in economics which lead to the kind of centralization we are observing in blockchains today. You can find discussions of these problems (and how Saito solves them) in our pages on the Tragedy of the Commons and the Free-Rider Problem. For now let's continue to describe how Saito fixes this problem.

### How Saito Fixes this Problem

Instead of paying for *extractive* forms of work like mining or staking, Saito makes the *contributive* work of "collecting fees" objectively observable in a decentralized environment by adding cryptographic routing signatures to transactions. Instead of hashing or staking for the right to produce blocks, we play a game where nodes that collect more money from users have an advantage producing blocks.

As a result of this change, the nodes that contribute the most value to the network now produce the most blocks. And whenever a block is distributed, all of the nodes that receive the block can see who did the work of collecting the fees. Consensus can distribute the block reward to one of those nodes. Problem solved, right?

Except it isn't -- because all we have done is replace our earlier problem with a much harder one. As long as the node that produces any block has a chance of collecting the fees it contributes, it suddenly has an incentive to add "fake transactions" to blocks to improve its chance of producing the next block. And it is suddenly rational for routing ndoes to add fake "routing hops" to the transactions they forward so that they have a greater chance of collecting any payment that is sent to routing nodes.

Both forms of cheating make the solution unworkable. They seem to throw us back to a situation in which the solution -- paying nodes for contributing money -- is fundamentally impossible because in a decentralized mechanism we can't tell who owns the money or whether multiple routing nodes are owned by the same person.

And this is the real problem that Saito fixes.

### How Saito Fixes this Problem



But the 


  whoever produces the block gets the right to collect the fees from how do we know that the transactions and fees that nodes are claiming to have collected didn't come from them?


pays a transaction fee, pays the nodes that actually deliver transactions into the network. When earnings depend on contributing to the network rather than extracting from it, incentives shift in a healthier direction. (If you want more background, we have pages on the **Free-Rider Problem** and the **Tragedy of the Commons**.)

---

## How Saito Fixes This Problem

The key change is simple: **Saito pays for the work the network actually needs.**

Nodes earn income by delivering transactions and bringing in the fees users are paying. This means:

- earnings come from serving users  
- the network’s incentives point outward, toward value creation  
- nodes have reason to route and relay rather than extract  

This fixes the core mispricing that causes extraction in other blockchains.

---

## But This Creates a Secondary Problem

If nodes earn money for helping the network, nothing stops them from trying to **use that money to buy block production**. A successful node could try to dominate consensus by outspending others, or a group of nodes could pool fees to seize control of block creation.

In other words:  
solving extraction by paying for routing work introduces a new incentive to attack consensus.

---

## How Saito Fixes *Those* Problems

Saito prevents earnings from being used to attack the chain by making harmful deviations **more expensive than honest behavior**.

This asymmetry is the foundation of Saito consensus:

- **It costs more to orphan a block than to build on it.**  
- **This remains true even if you control a majority of network resources.**  
- **So cooperating with the longest chain is always the cheapest option.**

Because deviation is privately costly, coalitions can’t profit by reorganizing the chain or spending their earnings to dominate production. The system favors cooperation by design.

---

## What This Gives Us

With aligned incentives and cost-asymmetric transitions, Saito exhibits properties that are difficult or impossible for traditional blockchains:

- **51% attacks become unprofitable** — majority coalitions lose money by deviating.  
- **Spam and state-bloat attacks are costly** — harmful state is expensive to add.  
- **Sybil identities don’t help attackers** — extra nodes don’t earn extra reward.  
- **Routing incentives are sustainable** — nodes earn for delivering data.  
- **On-chain applications become practical** — social networks, marketplaces, games, chat, and video all run smoothly.  
- **Blockspace supply adjusts naturally** — the network expands or contracts with demand.

Saito is what a blockchain looks like when the core incentives are aligned with the work required to operate the network.
