---
title: What is Saito
description: An ELI5 description of what Saito Consensus is and why it matters...
published: true
date: 2025-11-23T11:51:41.344Z
tags: 
editor: markdown
dateCreated: 2025-11-23T10:51:54.600Z
---

### What Problem Does Saito Solve?

Blockchains are distributed networks that need to pay for their own infrastructure. They must collect fees from users and somehow get those fees to the nodes that are actually running the network. In principle this sounds simple enough.

In practice it is one of the hardest problems in distributed systems. To pay the right nodes the right amount of money, a network must be able to observe who is contributing real value. But in a decentralized blockchain where participants can lie and orphan blocks contributed by others, there is no reliable way to measure contribution. Consensus only ever sees the blocks that “win” and not the honest contributions that contributed value but got buried.

Unable to solve this, Bitcoin and Ethereum developers declared the problem impossible and retreated to using pay-to-pay activities (mining and staking) that are expensive but objectively measurable in distributed systems. Instead of trying to get the money to the nodes producing real value, they limited which nodes could produce blocks and collect payments based on how much extractive work they performed. While Satoshi knew this was problematic and hoped that the people earning the rewards would spend money to fund network infrastructure, the developers that followed him forgot that fees were supposed to incentive the provision of the network, and shifted to make infrastructure provision the responsibility of the private sector not the consensus mechanism.

### The Underlying Problem Is Extractive Economics

Without the ability to provision their own infrastructure, other networks drift toward economic centralization:

- nodes that run infrastructure lose money  
- nodes that only stake / hash accumulate money  
- extractors reinvest to dominate block production  

Consensus changes from a protocol that supports the network to a that cripples it, by transferring wealth from economic productive nodes (paying for infrastructure, collecting fees) to extractive nodes.

As we explain in our separate pages on the **Tragedy of the Commons** and the **Free-Rider Problem**, the only rational response for infrastructure providers is to restrict access to the transactions they are collecting for the network, and create business models which monetize the willingness of users to pay fees before their transactions ever hit the consensus layer of the blockchain.

What started as an open and permissionless network degrades into a closed and centralized mechanism because economic pressures induce centralization by forcing a need for the private sector to provision infrastructure at scale, and find business models that are capable of bearing those costs.

### But Saito Fixes This Problem... How?

The solution Saito introduces is paying for the contributive work of **sharing transaction fees** with other nodes in the network.  Saito does this by adding cryptographic routing signatures to transactions which store information on how they flow into the network. This makes routing paths objectively observable once those transactions are put into blocks. Instead of hashing or staking for the right to extract value, nodes earn influence by bringing real fees into the chain.

As a result:

- nodes that serve users collect more fees  
- nodes that collect more fees produce more blocks  
- honest contributive work gets rewarded in a verifiable way  

Problem solved? 

Not quite. And the reason for this is that money flows are circular in blockchains. As soon as nodes can make blocks by spending money, and earn money by producing blocks, nodes suddenly have an incentive to cheat by adding **fake transactions** to their own blocks in order to produce more blocks and collect more of other people's money. Routing nodes face the same temptation for routing payouts: why not add **fake hops** that make them seem to have done more work collecting the fee?

Both forms of cheating kill the solution if unsolved, because switching to use "fee collection" as our objective measure of value-contribution requires it to be impossible for attackers to game the payout mechanism by pretending to be honest users and spending their own money to attack the blockchain.

This is the real problem that Saito solves.

### And the Solution is Revolutionary

Saito inhibits attackers by making it more expensive for nodes to add their money into blocks or add fake routing hops to transactions. Those forms of deviation remains possible, but in every case where they are undesirable, more profitable strategies exist that encourage cooperation with other participants.

The cost asymmetry this creates forms the heart of the mechanism. And the problem that makes it impossible to measure value contribution disappears because attacking the metric the network uses to issue payouts becomes quantifiably costly in equilibrium. Cooperation becomes the dominant and most profitable way to participate in the network.

In Saito-class mechanisms:

- **It costs more to orphan a block than to build on it.**  
- **This remains true even if you control a majority of network resources.**  
- **So cooperating with the longest chain is always the cheapest option.**

The solution is subtle and genuinely original: Saito aligns private cost with social cost in a way no previous consensus mechanism manages to do. And because attacking the longest-chain is less profitable than building atop it, coalitions cannot even benefit from reorganizing the chain or pushing other people's blocks off it. Cooperation replaces competition as the winning network strategy.


### What This Gives Us

With aligned incentives and cost-asymmetric state transitions, Saito exhibits properties that are difficult or impossible for traditional blockchains:

- **51% attacks become unprofitable**  
- **spam and state-bloat attacks carry real cost**  
- **sybil identities offer no advantage**  
- **routing and bandwidth infrastructure become sustainable**  
- **on-chain applications are profitable to operate**
- **and the network scales emergently**

Saito is what a blockchain looks like when its core incentives are aligned with the work required to operate the network. For more information on how Saito Consensus works and is able to impose this asymmetrical cost of attack, please see our ELI5 page describing [Saito Consensus](/consensus).