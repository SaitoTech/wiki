---
title: Untitled Page
description: 
published: true
date: 2024-11-30T08:31:29.591Z
tags: 
editor: markdown
dateCreated: 2024-11-30T08:31:29.591Z
---

# Tolerating Malicious Majorities – Advances in Distributed Consensus

*Written by David Lancashire on April 24, 2023*

For the last four decades, computer scientists have believed that consensus mechanisms can tolerate a theoretical maximum of (n-1)/2 dishonest participants. This limit has recently increased to (n-1)/2+x, permitting tolerance of even a majority of dishonest actors.

The advance is possible in mechanisms where attackers must expend a costly resource (“work”) to participate in consensus. Under these conditions, a malicious majority can be tolerated if the consensus mechanism can asymmetrically strip attackers of “work” over time and restore honest participants to majority status.

Asymmetrically punishing attackers is accomplished by taxing the only activity attackers perform which honest nodes do not: the orphaning of work from other participants. There is a precedent for this type of tax in Bitcoin, but the penalty fails under majoritarian assault. Securing a consensus mechanism beyond that requires making work-orphaning expensive even in situations where attackers produce all of the blocks on the longest-chain.

Framing the problem this way makes it clear why proof-of-work and proof-of-stake blockchains cannot solve it. In those mechanisms, the cost of orphaning work is identical to the cost of proposing blocks once attackers can propose a majority of blocks. When attackers spend resources to push the chain into stasis, the honest network is forced to spend an equivalent amount to resolve the deadlock. Honest nodes face symmetrical losses which prevents their recovering majority status.

The theoretical solution that improves security involves migrating the “work” used to produce blocks into the transactions that constitute them. Attackers may still produce blocks that route around those proposed by honest nodes, but the newly-orphaned transactions can be shifted costlessly into a new block and deposited at the tip of the attacker’s chain to resolve the deadlock.

Preventing this requires a more aggressive form of work-orphaning: attackers must move the work-bearing transactions into their own chain. This form of orphaning-by-inclusion is profitable in proof-of-work and proof-of-stake designs but can be made quantifiably costly in others.

Routing work — the addition of cryptographic routing signatures to transactions — is the first known strategy that accomplishes it, modulating down the value of transactions for producing blocks as well as the expected payout from their inclusion. With a sufficiently high per-hop decay (50% or greater) attackers who orphan-by-inclusion face an expected loss from doing so, even if they produce all of the blocks in the blockchain.

A properly designed mechanism not only exposes attackers to this cost, but forces them to pay it in a way that reduces their ability to generate work and participate in consensus.

The somewhat alien nature of asymmetrical taxation may be one reason the first wave of blockchains like Saito which use routing work are still outside the mainstream. The concepts that power the network and create guaranteed economic losses for attackers are simple enough once understood.

Routing signatures create a different cost structure that allows different nodes to produce blocks more and less cheaply at different times. As long as it remains cheaper for the honest network to produce at least a subset of blocks than attackers, the network will always be able to imposes losses on those attempting to commandeer the longest-chain.

Those interested in a practical description of how to implement such a mechanism are invited to review our one-page summary of Saito Consensus or read our more academic whitepaper describing how this approach works. It is worth noting that the innovations here are generally applicable across the space.

As the leading blockchain team focused on routing work – we look forward to broader awareness within academia of the fundamental advances that cryptographically-secured routing makes possible in distributed consensus. It is encouraging to see the blockchain space continue to make headway on problems that have been previously considered unsolvable. In this case, achieving quantifiable security guarantees against malicious majority coalitions is no longer an insurmountable task.
