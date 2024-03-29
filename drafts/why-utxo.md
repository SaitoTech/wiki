---
title: Why UTXO
description: A quick introduction to why Saito uses a UTXO structure
published: true
date: 2024-02-15T06:14:15.344Z
tags: 
editor: markdown
dateCreated: 2024-02-12T00:53:34.021Z
---

# Why UTXO?

This explanation derives from this [thread](https://twitter.com/dlancashi/status/1756705883029934464) written by David Lancashire.

UTXO chains can add, verify, and revert transactions quickly and independently of one another, while Account Model chains must compute complex, interconnected outputs which cannot be checked in parallel and cannot be verified without doing so for every other transaction in the block.

## Overview

Why does Saito employ a UTXO model rather than an account based ledger?

Much has been written on The *Account* versus *UTXO* Model for ledger designs. The Account Model makes programmability easier while restricting the optimizations around transaction verification. Smart contracts are simple to implement out of the box but verifying individual transactions becomes necessarily complex since all account balances may depend on any single transaction within a block.

The Account Model also allow developers use pre-written database software. This, again, speeds up development, but leaves scaling limited by database throughput. Unless a chain's number one priority is arbitrary computation, the overhead associated with verifying individual account balances (equal to verifying the state of entire blocks) rapidly degrades the ability for smaller nodes to meaningfully participate in the blockchain.

Contrast to UTXO, where the only data required to verify a new transaction are the specific coins which it is spending; this grants transactions the property of being "atomic," i.e independent of one another. No matter how many transactions are processed into a block, individual users can have their receipts verified quickly and cheaply, and full nodes can revert blocks in the case of a fork without re-verifying every transaction.

Perhaps the greatest benefit of the atomic property of The UTXO Model is that all transactions can be processed in parallel, meaning scaling performance is as easy as adding more computers. This is unlike the Account Model, where the computation of the state-transition of a new block has arbitrary inter-dependencies between all its transactions making such parallelization impossible.

Even Ethereum, the chain which popularized The Account Model, has adjusted its roadmap to push as much computation off-chain as possible via layer-2 scaling. Saito sees the choice of UTXO over accounts as a natural technical path to allow massive scaling; readers should note that it is also well-proven that smart contracts can exist and thrive on UTXO chains.

## In Practice

In Saito, each UTXO is associated with an entry into an in—memory hashmap specific to that UTXO. When a transaction arrives the hashmap allows the UTXO inputs it must consume to be conjured with the minimal possible overhead. The fastest data structure is thus used to store the most critical most frequently checked data, and quickly answer: do these tokens exist and can they be spent? This directs the greatest optimizations towards the most fundamental and prolific operation:

![Hashmap Speeds](https://pbs.twimg.com/media/GGETcXlX0AAD6I2?format=jpg&name=small)
[source](https://tessil.github.10/2616/68/29/benchmark-hopscotch-map.html)

As demonstrated above, current technologies allow millions of new entries into a hashmap per second; the simple nature of the UTXO verification scheme is key to opening the door to the benefits of such data structures, which are widely applied and innovated upon independent of the cryptocurrency sector.

<!--
Nodes can delete the massive block data from rapid-memory access, as the critical information is now contained in this incredibly-compact and rapid-access data structure.

When you want to spend tokens, your transaction says "here is the utxo I want to spend...” the information in the spending tx is used to "recreate" the key that would have been used to add the UTXO, and the full nodes can check the hashmap - if an entry exists then the tokens must have been added.


This is now possible to do in parallel and doesn't require a database re-orging the chain is also much faster and doesn't run into the problems that smart contract—style chains do, because all the blockchain is really doing on the base layer is flipping entries in this hashmap.
-->

Consensus on a UTXO chain can be completely managed by flipping entries in a hashmap. Processing transactions, verifying if they have already been spent or not and checking their inputs, then adopts the technical scalability of such hashmaps. This is especially important in the *open*, distributed context, where agreement on the most recent blocks is expected to sometimes differ:

When consensus on the longest chain ends up differing from one node's perspective, that node is not required to recompute expensive state transitions from scratch; instead they simply correct their hashmap for only the transactions which are affected. This greatly reduces the cost associated with chain re-organizations - the situation where nodes must revert and rebuild blocks on the end of their chains after discovering their fork is invalid or out of agreement with the network.

## Re-Orgs

<!--
Entry A becomes unspendable and entries B and C become spendable.

If the chain rolls back in the other direction (such as during a re-org) B and C become unspendable and A becomes spendable.
-->

The re-organization (re-org) of blocks is one of the most fundamental issues all blockchains must grapple with. Given that blockchains eschew any central coordinator, nodes de-synchronizing and then resolving their differences through re-orgs is unavoidable. Most attacks on blockchain consensus exploit and exacerbate the fact that re-orgs will happen, and thus handling them generally is a sensitive and crucial topic.

The great difficulty Account Model chains have around re-orgs is the *cost* associated with reverting and recomputing state transitions (new blocks). Such database-models cannot elegantly perform reverse-direction transformations, and is one reason *closure* must be introduced. Open versus closed systems is out of scope, but simply put: closure sacrifices the ability for anyone to participate in an attempt to make re-orgs less likely.

In many designs, the developers basically *must* add closure because state-transitions under Account Model data-structures may only progress in a forward-moving direction. If the chain gets reversed an older version must be dug up and rolled forward until it reaches consensus. This requires recomputing the blocks from scratch even if the input transaction list differs only by a tiny amount. 

UTXO and hashmaps only need recompute each differing transaction. The difference in the re-orged blocks is closely associated to the cost of re-org, whereas the cost of re-org under Account-based chains is associated with the size of the block.

This is one reason POS developers typically push ”finality" so hard as a feature. Finality itself isn't what it is literally sold as - it really just seeks to impart grave penalties on nodes who end up on forks past a certain length, ideally allowing all nodes to assume they will never need to reorg more than $N$ blocks.

Debates on the sacrifices made to achieve those penalties are out of scope, but suffice to say that discouraging forks doesn't solve the fundamental issue of expensive reorgs, and requires tradeoffs against other consensus-level design choices which fundamentally tarnish many desirable properties of blockchain.

UTXO reorgs are fundamentally simpler and faster because verification can be reduced down to flipping bits in a hashmap with no concern that one entry will have an unexpected relationship to any other. State-transitions moving backwards through the chain history happen almost as quickly as moving forwards.

Under a UTXO system, re-orgs are so much less expensive and thus much less threatening. Sacrificing of openness properties which Account-based chains must make are not at all necessary with UTXO. The Layer-1 is simpler because "account cruft" gets pushed to wallet or apps and the blockchain itself can be optimized for consensus.

<!--
From this [thread](https://twitter.com/dlancashi/status/1756705883029934464)  
-->