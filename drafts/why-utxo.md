---
title: Why UTXO
description: A quick introduction to why Saito uses a UTXO structure
published: true
date: 2024-02-13T02:24:04.167Z
tags: 
editor: markdown
dateCreated: 2024-02-12T00:53:34.021Z
---

# Why UTXO?

Why does Saito employ a UTXO model rather than an account based ledger?

Much has been written on The *Account* versus *UTXO* Model for ledger designs. The Account Model makes programmability easier while restricting the optimizations around transaction verification. Smart contracts are simple to implement out of the box but verifying individual transactions becomes necessarily complex since all account balances may depend on any single transaction within a block.

The Account Model also allow developers use pre-written database software. This, again, speeds up development, but leaves scaling limited by database throughput. Unless a chain's number one priority is arbitrary computation, the overhead associated with verifying individual account balances (equal to verifying the state of entire blocks) rapidly degrades the ability for smaller nodes to meaningfully participate in the blockchain.

Contrast to UTXO, where the only data required to verify a new transaction are the specific coins which it is spending; this grants transactions the property of being "atomic," i.e independent of one another. No matter how many transactions are processed into a block, individual users can have their reciepts verified quickly and cheaply, and full nodes can revert blocks in the case of a fork without reverifying every transaction.

Perhaps the greatest benefit of the atomic property of The UTXO Model is that all transactions can be processed in parrelell, meaning scaling performance is as easy as adding more computers. This is unlike the Account Model, where the computation of the state-transition of a new block has arbitrary interdependencies between all its transactions making such parrellization impossible.

Even Ethereum, the chain which popularized The Account Model, has adjusted its roadmap to push as much computation off-chain as possible via layer-2 scaling. Saito sees the choice of UTXO over accounts as a natural technical path to allow massive scaling; readers should note that it is also well-proven that smart contracts can exist and thrive on UTXO chains.

## Saito Implementation

In Saito, each UTXO is associated with an entry into an in—memory hashmap specific to that UTXO. When a transaction arrives the hashmap allows the UTXO inputs it must consume to be conjured with the minimal possible overhead. The fastest data structure is thus used to store the most critical most frequently checked data, and quickly answer: do these tokens exist and can they be spent? This directs the greatest optimizations towards the most fundamental and prolific operation:

![Hashmap Speeds](https://pbs.twimg.com/media/GGETcXlX0AAD6I2?format=jpg&name=small)
[source](https://tessil.github.10/2616/68/29/benchmark-hopscotch-map.html)

As demonstrated above, current technologies allow millions of new entries into a hashmap per second; the simple nature of the UTXO verification scheme is key to opening the door to the benefits of such data structures, which are widely applied and innovated upon independent of the cryptocurrency sector.

Nodes can delete the massive block data from rapid-memory access, as the critical information is now contained in this incredibly-compact and rapid-acoess data structure.

When you want to spend tokens, your transaction says "here is the utxo I want to spend...” the information in the spending tx is used to "recreate" the key that would have been used to add the UTXO, and the full nodes can check the hashmap - if an entry exists then the tokens must have been added.

This is now possible to do in parallel and doesn't require a database re-orging the chain is also much faster and doesn't run into the problems that smart contract—style chains do, because all the blockchain is really doing on the base layer is flipping entries in this hashmap.

Entry A becomes unspendable and entries B and C become spendable.

If the chain rolls back in the other direction (such as during a re-org) B and C become unspendable and A becomes spendable.

The difficulty that smart-contract and database-models have with elegant reverse-direction transformations is one reason they are so keen to add closure.
in many designs, the developers basically *have* to add closure because they can only transform their data-structure in a single forward-moving direction, so if the chain gets reversed they need to load an older version and roll it forward again onto a new branch.

This is one reason POS devs typically push ”finality" so hard as a feature. Finality itself isn't what it is sold as - it really just puts a cap on the cost of forking the chain, but it allows devs to assume they will never need to reorg more than N blocks, which clears memory with UTXO, reorgs are much faster because we are just flipping bits in a hashmap w/o significant overhead, and we can move backwards almost as quickly as we can move forwards. so reorgs are less threatening.

The L1 is simpler because "account cruft" gets pushed to wallet or apps.

From this [thread](https://twitter.com/dlancashi/status/1756705883029934464)  