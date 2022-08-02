---
title: Saito Consensus Mechanism
description: Consensus Mechanism
published: true
date: 2022-08-02T02:58:29.454Z
tags: 
editor: markdown
dateCreated: 2022-02-17T10:09:00.217Z
---

# Saito Consensus

This page offers a straight-forward description of how Saito Consensus works. We have separate pages explaining how Saito eliminates common [attack vectors](/consensus/attack-vectors), a brief [math paper](/consensus/math) demonstrating cost-of-attack properties and [open proposals](/consensus/proposals) on technical implementation. You may also be interested in the [economic problems](/consensus/economics) Saito Consensus solves and [critical videos](/consensus/videos) covering the mechanism.

## 1. PRODUCING BLOCKS

Saito adds cryptographic routing signatures to transactions. When users send their transactions into the network they add a routing signature that specifies the node to which they are sending their transaction. Nodes add similar routing signatures as they receive and forward these transactions. This gives all transactions an unforgeable record of the path the transaction has taken into the network. The same transaction in different mempools will have the same core transaction data but a different set of routing signatures.

The blockchain now sets a "difficulty" for block production that can be met only by producing a block that contains enough "routing work". The amount of "routing work" in any block is the aggregate of the "routing work" in the transactions in the block. The amount of "routing work" in any transaction is the value of its transaction fee halved with each additional hop beyond the first that the transaction has taken into the network.

Block production difficulty in Saito Consensus consequently reflects the difficulty of collecting fees (efficiently) from network users and sharing them with other peers on the network. In order to prevent nodes from stealing routing work from their peers, we specify that transactions provide no "routing work" to block producers who are not in their routing path.

Once the block is produced all of the fees in the block are burned.

## 2. THE PAYMENT LOTTERY

Each block contains a proof-of-work challenge. When a block is produced miners start hashing to find a solution. We call this solution the "golden ticket". The exqct mechanism is designed so that tickets cannot be forged or stolen in-transit.

If a valid golden ticket for block N is included in block N+1, Saito will resurrect the burned block reward from block N. The payments in block are thus for fees burned in the previous block. The process repeats block by block. Saito charges nodes (in burned fees) for the right to produce a block, and then charges them again (in hash) for the right to unburn the payouts from the previous block.

When any block contains a golden ticket, who collects the payout from the previous block depends on a random variable from the golden ticket solution. That random number is used to select a winning transaction from the previous block, with all transactions weighted according to their share of fees in the previous block. The same number used to select the winning transaction is then hashed again to select a routing node from the list of nodes in the transaction routing path. These nodes are weighted according to their individual share of the aggregate amount of routing work generated. If a transaction paying a 10 SAITO fee passes through two relay nodes before its inclusion in a block by the third routing node (i.e. block producer), the first relay node will have 10 / 17.5 percent (57\%) of aggregate routing work, the second will have 5 / 17.5 percent (29\%) of the aggregate routing work, and the block producer will have 2.5 / 17.5 percent (14\%) of the routing work in that transaction. If a transaction has no routing path, the sender of the transaction is assigned 100\% of the routing work in that transaction.

In the event that the block reward is seriously in excess of a smoothed average maintained by consensus (current target 1.25), the payment for both miner and router is reduced proportionally and the excess portion is burned for good. This ensures there are no theoretical situations in which attackers can recapture more money from the payments lottery than they are forced to contribute in attacking the network.

The "Classic Saito" design targets a difficulty where the network can produce an adequate amount of golden tickets to recapture payments. The network is secure at the cost of deflation from unsolved blocks.


## 3. INCREASING COST-OF-ATTACK

Set mining difficulty to auto-adjust to target 1 golden ticket every 2 blocks. If 2 consecutive blocks are produced without a golden ticket, difficulty decreases slightly. If 2 consecutive blocks are produced with golden tickets, difficulty increases slightly.

Once a golden ticket is included in block N, the payment to the miner and router for the preceding block N-1 is unmodified. If block N-1 did not contain a golden ticket, we recurse to block N-2 and hash our random variable again to select a winning routing node from block N-2. This routing node receives half of the payout from block N-2. The other half is collected by a "staking treasury" maintained by the consensus software. This process can be repeated for all previously unpaid blocks, although an upper limit to backwards recusion may be applied for practical purposes, and it is preferable for routers not to receive payouts more than two blocks back.

There is no staking table. The funds in the staking treasury are paid to UXTO holders during the course of ATR processing (see below). We recommend readers become familiar with automatic transaction rebroadcasting before reading our [technical docs](https://github.com/SaitoTech/saito-implementation-proposals/blob/main/proposals/001_simplified_staking.md) covering ATR implementation details.

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

**Powspit:** a variable between 0 and 1 that determines the target percentage of blocks solved through golden tickets.

**Golden Ticket:** a transaction from a miner containing a valid solution to the computational lottery puzzle embodied in the previous block hash.

**Genesis Period:** the length of the epoch in number of blocks.




