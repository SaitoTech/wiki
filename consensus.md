---
title: Saito Consensus Mechanism
description: Consensus Mechanism
published: true
date: 2023-06-29T01:14:49.606Z
tags: 
editor: markdown
dateCreated: 2022-02-17T10:09:00.217Z
---

# Saito Consensus

This page offers a straight-forward description of how Saito Consensus works. Separate pages explaining how Saito eliminates common [attack vectors](/consensus/attack-vectors), a brief [math paper](/consensus/math) on cost-of-attack properties and [open proposals](/consensus/proposals) on technical implementation. You may also be interested in the [economic problems](/consensus/economics) Saito Consensus solves and [critical videos](/consensus/videos) covering the mechanism.

## 1. PRODUCING BLOCKS

When users send transactions into the network they add a cryptographic routing signature that specifies the first-hop node(s) to which they are sending their transaction(s). First-hop nodes add similar routing signatures as they propagate those transactions to their peers. Whichever version of the transaction is included in a block will have a chain of routing signatures unique to the path it took to reach the block producer.

The blockchain maintains a "difficulty" for block production that must be met by including a set amount of routing work in the block. Blocks which do not contain this amount of routing work are invalid according to consensus.

The amount of routing work in a block is the aggregate amount of "routing work" available for the block producer in each individual transaction in the block. This is calculated as the value of the transaction fee halved by each subsequent hop beyond the first that the transaction has taken to reach the block producer. Transactions without a valid routing path connecting the sender and block producer provide no routing work. It is also possible to simply specify that block producers may not include transactions that do not contain a valid routing path.

## 2. THE PAYMENT LOTTERY

When a block is produced all of the fees in the block are collected into a network treasury rather than paid out to block producers as is common in other designs. The following mechanism describes how to safely recover those fees and distribute them to participants in the network.

Each block contains a implicit proof-of-work challenge. When a block is produced miners start hashing to find a valid solution ("golden ticket"). This computational puzzle works similarly to that in Bitcoin, save that the mechanism is designed so that solutions cannot be forged or stolen in-transit.

If a golden ticket for block N is included in block N+1, the network issues two payouts: the first to the miner that found the solution and the second to a random node in the routing network. The amount of the mining payout is 50% of the fees included in the previous block. The amount of the router payout is 50% of the fees included in the previous block.

This process repeats block by block as Saito charges nodes (in burned fees) for the right to produce blocks and then again (in energy costs) for the right to unburn and distribute the payments.

## 3. SECURE ROUTER SELECTION

The winning routing node is selected using the random number provided by the golden ticket which solves the difficulty puzzle. That number is used to select a transaction from the previous block with each transaction's chance of selection being proportional to its share of fees contributed to the block. The random number which selected the transaction is then hashed again to select a random node from the routing path of that transaction. Each node in the routing path has a chance of winning this proportional to its share of the aggregate routing work held by all members of that routing path.

If a transaction paying a 10 SAITO fee passes through two relay nodes before its inclusion in a block by a third routing node (i.e. block producer), the first relay node will have 10 / 17.5 percent (57%) of aggregate routing work, the second will have 5 / 17.5 percent (29%) of aggregate routing work, and the block producer will havea  2.5 / 17.5 percent (14%) share. If consensus permits block producers to include transactions without valid routing paths and in the event the winning transaction has no routing path, the sender of the transaction should be assigned 100% of the routing work in that transaction.

The "Classic Saito" design targets a difficulty where the network can produce one golden ticket every two blocks on average and is secure at the cost of deflation from unsolved blocks.


## 4. IMPROVING THE BASE MECHANISM

To prevent attackers gaming the lottery mechanism, we have consensus maintain a smoothed average of the fees included over the last epoch. In the event that the block reward is seriously in excess of this smoothed average (current target 1.25) the payment for both miner and router is capped at the target and the excess portion is burned for good.

To avoid deflation we introduce recursive payouts. Whenever a golden ticket is included in block N+1 we issue the payouts for block N as described above. If block N did not contain a golden ticket, we recurse to block N-1 and use our golden ticket to select a winning routing node for that black. This process can be repeated for all previously unpaid blocks, but it is preferable not to recurse more than two blocks back if difficulty is targeting 1 solution every 2 blocks.

Saito adds a payout to the UXTO holders in the network that is processed during the course of ATR processing (see below). This payout is funded by fees intended for the "mining payout" which is left uncollected in recursive block payouts described above.

## 5. AUTOMATIC TRANSACTION REBROADCASTING (ATR)

Saito divides the blockchain into "epochs" of N blocks. If the latest block is 500,000 and N is 100,000 blocks, then the current epoch streches from block 400,001 onwards.

Once a block falls out of the current epoch, its unspent transaction outputs (UTXO) are invalid by consensus rules. Any UTXO from that block which meet rebroadcast criteria must be re-included by the producer of the next block in the form of an "automatic transaction rebroadcasting" (ATR) transaction. These ATR transactions include the original transaction as embedded data, but provide new UTXO spendable by the original address.

The criteria for rebroadcasting is not only that the UTXO is still unspent, but that the UTXO itself contains enough tokens to pay a rebroadcasting fee. This rebroadcasting fee should be equal to or greater than the average fee per byte paid by new transactions over the previous epoch. The UTXO may also be issued a payout as described in the section above, where the earnings are proportional to the UTXO's share of the unspent tokens circulating around the blockchain.

The new UTXO may be greater to or less than the value of the previous UTXO, with the exact balance determined by market forces rather than hardcoded by developers. In addition to the economic and security benefits of the ATR payout, we note that permanent data storage becomes possible through this mechanism.

## 6. ADVANCED SAITO

Additional mechanisms that increase network robustness include: 

Creating wrap-around spam resistance to block flooding attacks by requiring all valid chains to contain N golden tickets over the last M blocks, such that forks are considered invalid unless they meet minimal hashing conditions.

Routing and congestion policies which leverage block-level signatures and allow nodes to police their peers to ensure that their peers are following sensible routing policies and not spamming the network or relaying malicious blocks.

Requirements for block producers to provide stake (making tokens unspendable for X blocks) when producing blocks, increasing the cost of some kinds of work-reuse and spamming attacks. Slashing these locked-up tokens is possible in some situations if the same tokens are staked for blocks within a set depth of each other.


### APPENDIX I: SAITO TERMINOLOGY

**Paysplit:** a variable between 0 and 1 that determines the percentage of the block reward that is allocated to mining nodes.

**Powsplit:** a variable between 0 and 1 that determines the target percentage of blocks solved through golden tickets.

**Golden Ticket:** a transaction from a miner containing a valid solution to the computational lottery puzzle embodied in the previous block hash.

**Genesis Period:** the length of the epoch in number of blocks.




