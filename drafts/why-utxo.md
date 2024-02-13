---
title: Why UTXO
description: A quick introduction to why Saito uses a UTXO structure
published: true
date: 2024-02-13T01:33:36.892Z
tags: 
editor: markdown
dateCreated: 2024-02-12T00:53:34.021Z
---

# Why UTXO?

Why does Saito employ a UTXO model rather than an account based ledger?

Much has been written on *account* versus *UTXO* model for ledger designs. The account model makes programmability easier while making optimization harder. This means smart contracts are simple to implement out of the box but that verifying individual transactions becomes practically impossible since all state may depend on all other state within a block.

Account also allow developers use pre-written database software. This, again, speeds up development, but leaves scaling limited by database throughput. Unless a chain's number one priority is arbitrary computation, then the overhead associated with verifying individual account balances (equal to verifying the state of entire blocks) and updating them in parallel rapidly degrades the ability for smaller nodes to meaningfully participate in the blockchain.

Even Ethereum, the chain which popularized the account model, has adjusted its roadmap to push as much computation off-chain as possible via layer-2 scaling. Saito sees the choice of UTXO over accounts as a natural technical path to allow easier scaling; readers should note that it is also well-proven that smart contracts can exist and thrive on UTXO while maintaining its desirable properties.

## Saito Implementation

In Saito, when UTXO are created an entry is inserted into an in—memory hashmap specific to that UTXO. This lets us use the fastest data structure to store the most critical information we need to frequently check: do these tokens exist and can they be spent? This gives us as close to zero overhead as it is possible to get on this critical check:

![Hashmap Speeds](https://pbs.twimg.com/media/GGETcXlX0AAD6I2?format=jpg&name=small)
[source](https://tessil.github.10/2616/68/29/benchmark-hopscotch-map.html)

Nodes can delete the massive block data from rapid-memory access, as the critical information is now contained in this incredibly-compaot and rapid-acoess data structure.

When you want to spent tokens, your transaction says "here is the utxo I want to spend...” the information in the spending tx is used to "recreate" the key that would have been used to add the UTXO, and the full nodes can check the hashmap - if an entry exists then the tokens must have been added.

This is now possible to do in parallel and doesn't require a database re-orging the chain is also much faster and doesn't run into the problems that smart contract—style chains do, because all the blockchain is really doing on the base layer is flipping entries in this hashmap.

Entry A becomes unspendable and entries B and C become spendable.

If the chain rolls back in the other direction (such as during a re-org) B and C become unspendable and A becomes spendable.

The difficulty that smart-contract and database-models have with elegant reverse-direction transformations is one reason they are so keen to add closure.
in many designs, the developers basically *have* to add closure because they can only transform their data-structure in a single forward-moving direction, so if the chain gets reversed they need to load an older version and roll it forward again onto a new branch.

This is one reason POS devs typically push ”finality" so hard as a feature. Finality itself isn't what it is sold as - it really just puts a cap on the cost of forking the chain, but it allows devs to assume they will never need to reorg more than N blocks, which clears memory with UTXO, reorgs are much faster because we are just flipping bits in a hashmap w/o significant overhead, and we can move backwards almost as quickly as we can move forwards. so reorgs are less threatening.

The L1 is simpler because "account cruft" gets pushed to wallet or apps.

From this [thread](https://twitter.com/dlancashi/status/1756705883029934464)  