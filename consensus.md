---
title: Saito Consensus Mechanism
description: Consensus Mechanism
published: true
date: 2022-09-05T06:01:51.804Z
tags: 
editor: markdown
dateCreated: 2022-02-17T10:09:00.217Z
---

# Saito Consensus

This page offers a straight-forward description of how Saito Consensus works. We have separate pages explaining how Saito eliminates common [attack vectors](/consensus/attack-vectors), a brief [math paper](/consensus/math) demonstrating cost-of-attack properties and [open proposals](/consensus/proposals) on technical implementation. You may also be interested in the [economic problems](/consensus/economics) Saito Consensus solves and [critical videos](/consensus/videos) covering the mechanism.

## 1. PRODUCING BLOCKS

Saito adds cryptographic routing signatures to transactions. When users send transactions into the network they add a routing signature that specifies the first-hop node(s) to which they are sending their transaction(s). Nodes add similar routing signatures as they forward these transactions. The same transaction sitting in different mempools will have the same core transaction data with a different set of routing signatures.

The blockchain now sets a "difficulty" for block production that can be met by producing a block with enough block-level routing work. This is the sum of the "routing work" contained in each individual transaction in the block, which is the value of its transaction fee halved with each additional hop beyond the first that the transaction has taken to reach the block producer. Transactions provide no "routing work" to nodes that are not in their routing path.

Once the block is produced all of the fees in the block are burned. The fundamental problem Saito solves is how to resurrect this fee and distribute it to value-producing nodes in the network without enabling circular fee-recycling attacks such as are possible in all proof-of-work and proof-of-stake class consensus mechanisms.

## 2. THE PAYMENT LOTTERY

Each block contains a proof-of-work challenge. When a block is produced miners start hashing to find a solution that meets consensus-level difficulty criteria. When a miner finds a solution they submit it to the network in the form of a "golden ticket" transaction.

If a valid golden ticket for block N is included in block N+1, Saito resurrects the burned fees from block N and distributes them to participants in the network in UTXO attached to block N+1. This process repeats block by block: Saito charges participants (in tokens) for the right to produce a block, and then charges them again (in hash) to unburn those funds.

When funds are unburned half of the fees that are resurrected are issued to the miner which found the golden ticket and half are issued to a random routing node sourced from the transaction routing paths in block N. A random variable associated with the golden ticket's hash solution is used to select the lucky router, with each transaction's chance of winning weighted according to the share of fees it contributed to block N. Once a transaction is selected the same random number is then hashed again to select a routing node from the list of nodes in the lucky transaction's routing path. These nodes are weighted according to their position in the routing path. If a transaction paying a 10 SAITO fee passes through two relay nodes before its inclusion in a block by the third routing node (i.e. block producer), the first relay node will have a 57\% change of winning (10 / 17.5), the second relay node will have a 29\% (5 / 17.5) chance of winning, while the block producer will have a 14\% (2.5 / 17.5) chance of winning. If a transaction has no routing path, the sender of the transaction is assigned 100\% of the routing work in that transaction.

This mechanism kills majoritarian and other economic attacks against consensus. The "Classic Saito" design targets a difficulty where the network can produce an adequate amount of golden tickets to recapture payments and is secure at the cost of deflation from unsolved blocks.


## 3. INCREASING COST-OF-ATTACK

It is possible to increase cost-of-attack against Saito Consensus such that the expense of attacking the network is well above 100% of the fee throughput of the network. This is a striking feature of Saito Consensus and differentiates it from other mechanisms where cost-of-attack is capped at 51% of fee throughput and for-profit attacks on consensus are always possible through collusion among participants.

One way to increase security is to maintain a smoothed average of the fees included in each block. In the event that the block reward is seriously in excess of this smoothed average (current target 1.25) the payment for both miner and router is reduced proportionally and the excess portion is burned for good. This ensures there are no theoretical situations in which attackers can recapture more money from the payments lottery than they are forced to contribute in attacking the network.

A more sophisticated improvement comes from adjusting mining difficulty to target 1 golden ticket every 2 blocks. If 2 consecutive blocks are produced without a golden ticket, difficulty decreases slightly. If 2 consecutive blocks are produced with golden tickets, difficulty increases slightly. The same effect can also be achieved by permitting multiple golden tickets in blocks although working out the details here is left as an exercise for the reader.

Once a golden ticket is included in block N+1, the process for issuing a payment to the miner and router from the preceding block N is unmodified. If block N did not contain a golden ticket, we now recurse to block N-1 and divide the payment from block N-1 between a random routing node and a "staking treasury" maintained as a consensus-level variable. The process of selecting the winning routing node is the same as that described above. And this process can be repeated for all previously unpaid blocks, although an upper limit to backwards recusion may be applied for practical purposes. It is preferable for routers not to receive payouts more than two blocks back.

Rather than maintain a staking table (which adds symmetrical attacks on the staking/closure mechanism), Saito distributes the funds in the staking treasury to UXTO holders during the course of ATR processing (see below). We recommend readers become familiar with automatic transaction rebroadcasting before reading our [technical docs](https://github.com/SaitoTech/saito-implementation-proposals/blob/main/proposals/001_simplified_staking.md) covering ATR implementation details.

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




