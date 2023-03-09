---
title: Saito Consensus Mechanism
description: Consensus Mechanism
published: true
date: 2023-03-09T07:50:09.577Z
tags: 
editor: markdown
dateCreated: 2022-02-17T10:09:00.217Z
---

# Saito Consensus

This page offers a straight-forward description of how Saito Consensus works. We have separate pages explaining how Saito eliminates common [attack vectors](/consensus/attack-vectors), a brief [math paper](/consensus/math) demonstrating cost-of-attack properties and [open proposals](/consensus/proposals) on technical implementation. You may also be interested in the [economic problems](/consensus/economics) Saito Consensus solves and [critical videos](/consensus/videos) covering the mechanism.

## 1. PRODUCING BLOCKS

Saito adds cryptographic routing signatures to transactions. When users send transactions into the network they add a routing signature that specifies the first-hop node(s) to which they are sending their transaction(s). Nodes add similar routing signatures as they forward these transactions. The same transaction sitting in different mempools will have the same core transaction data with a different set of routing signatures unique to the path that version of the transaction has taken to reach its specific mempool.

The blockchain now sets a "difficulty" for block production that can be met by producing a block containing a defined amount of routing work. The amount of routing work in a block is the sum of the "routing work" contained in each individual transaction in the block, which is itself calculated as the value of the transaction fee halved by each additional hop beyond the first that the transaction has taken to reach the block producer. Transactions provide no "routing work" in blocks where they do not have a valid routing path that connects the sender to the block producer.

Once a block is produced all of the fees in the block are burned. One of the fundamental problems Saito solves is how to resurrect this fee without enabling circular fee-recycling attacks such as those possible in proof-of-work and proof-of-stake class consensus mechanisms.

## 2. THE PAYMENT LOTTERY

Each block contains a proof-of-work challenge. When a block is produced miners start hashing to find a solution. We call this solution the "golden ticket". The mechanism is designed so that tickets cannot be forged or stolen in-transit.

If a valid golden ticket for block N is included in the very next block, N+1, Saito resurrects the burned block reward from block N. These resurrected funds are then split between the miner that found the solution and a random node in the routing network. We repeat this process block by block as Saito charges nodes (in burned fees) for the right to produce blocks and then again (in hash) for the right to unburn and distribute the payments.

Choosing a winning routing node is done using a random number provided by the golden ticket. That random number is hashed first to select a transaction from the previous block with all transactions weighted according to their share of the total fees contributed to the block. The random number is then hashed again to select a routing node from the list of nodes in the winning transaction's routing path, with the chance of each node's success halving with each additional hop.

If a transaction paying a 10 SAITO fee passes through two relay nodes before its inclusion in a block by a third routing node (i.e. block producer), the first relay node will have 10 / 17.5 percent (57%) of aggregate routing work, the second will have 5 / 17.5 percent (29%) of aggregate routing work, and the block producer will havea  2.5 / 17.5 percent (14%) share. If a transaction has no routing path, the sender of the transaction is assigned 100% of the routing work in that transaction.

This mechanism kills majoritarian and other economic attacks. The "Classic Saito" design targets a difficulty where the network can produce an adequate amount of golden tickets to recapture payments and is secure at the cost of deflation from unsolved blocks.


## 3. INCREASING COST-OF-ATTACK

It is possible to increase cost-of-attack against Saito Consensus such that the expense of attacking the network is well above 100% of the fee throughput of the network. This is a striking feature of Saito Consensus and differentiates it from other mechanisms where cost-of-attack is capped at 51% of fee throughput and for-profit attacks on consensus are always possible through collusion among participants.

One way to increase security is to maintain a smoothed average of the fees included in each block. In the event that the block reward is seriously in excess of this smoothed average (current target 1.25) the payment for both miner and router is reduced proportionally and the excess portion is burned for good. This ensures there are no theoretical situations in which attackers can recapture more money from the payments lottery than they are forced to contribute in attacking the network.

A more sophisticated improvement comes from adjusting mining difficulty to target 1 golden ticket every 2 blocks. If 2 consecutive blocks are produced without a golden ticket, difficulty decreases slightly. If 2 consecutive blocks are produced with golden tickets, difficulty increases slightly. The same effect can also be achieved by permitting multiple golden tickets in blocks although working out the details here is left as an exercise for the reader.

Once a golden ticket is included in block N+1, the process for issuing a payment to the miner and router from the preceding block N is unmodified. If block N did not contain a golden ticket, we now recurse to block N-1 and divide the payment from block N-1 between a random routing node and a "staking treasury" maintained as a consensus-level variable. The process of selecting the winning routing node is the same as that described above. And this process can be repeated for all previously unpaid blocks, although an upper limit to backwards recusion may be applied for practical purposes. It is also preferable for routers not to receive payouts more than two blocks back: if those payments are issued they should be redirected into the staking treasury.

Rather than maintain a staking table (management of which opens symmetrical attacks discouragement on the staking/closure mechanism), Saito distributes the funds in its staking treasury to all UXTO holders in the network during the course of ATR processing (see below). We recommend readers become familiar with automatic transaction rebroadcasting before reading our [technical docs](https://github.com/SaitoTech/saito-implementation-proposals/blob/main/proposals/001_simplified_staking.md) covering ATR implementation details.

These changes drive cost-of-attack well above 100% of fee throughput in all situations except those where attackers control 100% of staking payouts, which is effectively impossible given the fact that every UTXO in the network is staking by default.

## 4. AUTOMATIC TRANSACTION REBROADCASTING (ATR)

Saito divides the blockchain into "epochs" of N blocks. If the latest block is 500,000 and N is 100,000 blocks, then the current epoch streches from block 400,001 onwards.

Once a block falls out of the current epoch, its unspent transaction outputs (UTXO) are considered invalid by consensus rules. Any UTXO from that block which contains enough tokens to pay a rebroadcasting fee must be re-included by the producer of the next block for that block to be considered valid. The rebroadcasting fee is twice the average fee per byte paid by new transactions as determined over a smoothing period.

Block producers rebroadcast UTXO slips by creating special "automatic transaction rebroadcasting" (ATR) transactions. These ATR transactions include the original transaction as embedded data, but come with new UTXO. Each UTXO that meets rebroadcast criteria is rebroadcast in a separate ATR transaction. The rebroadcasting fee is deducted from each UTXO and added to the block reward. A staking payout may be added during the rebroadcasting process. 


## 5. ADVANCED SAITO

We welcome feedback on consensus design. Other improvements under consideration and/or testing:

Protecting against cash-only attacks by requiring the blockchain to have N golden tickets over the last M blocks, and considering chains invalid unless they meet minimal hashing conditions.

Routing and congestion policies which leverage block-level signatures and allow nodes to police and ensure their peers are not spamming the network.

Possible adding requirements for block producers to provide stake (making tokens unspendable for X blocks) when producing blocks, increasing the cost of some kinds of work-reuse and spamming attacks.


### APPENDIX I: SAITO TERMINOLOGY

**Paysplit:** a variable between 0 and 1 that determines the percentage of the block reward that is allocated to mining nodes.

**Powsplit:** a variable between 0 and 1 that determines the target percentage of blocks solved through golden tickets.

**Golden Ticket:** a transaction from a miner containing a valid solution to the computational lottery puzzle embodied in the previous block hash.

**Genesis Period:** the length of the epoch in number of blocks.




