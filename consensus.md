---
title: Saito Consensus Mechanism
description: Consensus Mechanism
published: true
date: 2023-09-10T06:41:05.749Z
tags: 
editor: markdown
dateCreated: 2022-02-17T10:09:00.217Z
---

# Saito Consensus

Saito Consensus eliminates the [sybil attacks](https://github.com/SaitoTech/papers/blob/50e5b243eb4d4062654f2751b056b6bb3fc053b5/sybil/A_Simple_Proof_of_Sybil_Proof_Lancashire-Parris_2023.pdf), [majoritarian attacks](/consensus/math) and other [attack vectors](/consensus/attack-vectors) common in proof-of-work and proof-of-stake class of consensus mechanisms. You may also be interested in the [economic problems](/consensus/economics) Saito Consensus solves and [critical videos](/consensus/videos) covering the mechanism.

## 1. PRODUCING BLOCKS

When users send transactions into the network they add cryptographic routing signatures that specify the first-hop node(s) to which they are sending their transaction(s). These nodes add similar routing signatures as they propagate these transactions.

Transactions without a valid routing path contain no routing work. The amount of routing work contained in other transactions depends on the total fee paid by the transaction and the number of nodes in the routing path. For details on how routing work is calculated, please see this page.

The blockchain maintains a "difficulty" for block production that is measured in routing work. Blocks which do not contain the required amount of routing work are invalid according to consensus rules.


## 2. THE PAYMENT LOTTERY

When a block is produced all of the fees in the block are burned. Miners then start hashing to find a golden ticket: a hash puzzle that will allow consensus to issue a payout.

If a golden ticket for block N is included in block N+1, consensus issues a reward worth the average amount of fees burned per block over the last epoch. Half are paid to the miner that found the golden ticket and half are issued to a routing node.

The routing node is selected by using the costly hash to pick a random transaction from the previous block (weighted by its share of fees in the block). The costly hash is then hashed again to generate a second random number that is used to select a random node from the routing path of the winning transaction (weighted by its share of the aggregate routing work held by all nodes in that routing path).

This process repeats block by block. Nodes burn money to produce blocks, and then burn energy to release payments, creating a game that is profitable for honest nodes who burn user-paid fees, but costly for attackers who must spend and then burn their own money to outpace the honest nodes and prevent their work being added to the longest-chain.

## 3. IMPROVING SECURITY

The "Classic Saito" design produces one golden ticket every two blocks on average and is secure at the cost of deflation from unsolved blocks.

To avoid deflation we introduce recursive payouts and a ATR payout. Whenever a golden ticket is included in block N we issue the payouts for block N-1 as described above. If block N-1 did not contain a golden ticket, we recurse to block N-2 and repeat the process to issue a router payout for that block.

The missing "mining" payout from block N-2 is collected by consensus for eventual distribution to the UTXO holders in the network as part of the ATR mechanism described below.

To increase security further, consensus maintains a smoothed average of the fees included over the last epoch. In the event that the block reward spikes in serious excess of this smoothed average (current target 1.25) the payment for both miner and router is capped at the target and the excess portion is burned for good. This adds a deflationary burn to the network which only kicks in when the network is under attack.

## 4. AUTOMATIC TRANSACTION REBROADCASTING (ATR)

Saito divides the blockchain into "epochs" of N blocks. If the latest block is 500,000 and N is 100,000 blocks, then the current epoch streches from block 400,001 onwards.

Once a block falls out of the current epoch, its unspent transaction outputs (UTXO) are invalid by consensus rules. Any UTXO from that block which meet rebroadcast criteria must be re-included by the producer of the next block in the form of an "automatic transaction rebroadcasting" (ATR) transaction. These ATR transactions include the original transaction as embedded data, but provide new UTXO spendable by the original address.

The criteria for rebroadcasting is not only that the UTXO is still unspent, but that the UTXO itself contains enough tokens to pay a rebroadcasting fee. This rebroadcasting fee should be equal to or greater than the average fee per byte paid by new transactions over the previous epoch. The UTXO may also be issued a payout as described in the section above, where the earnings are proportional to the UTXO's share of the unspent tokens circulating around the blockchain.

The new UTXO may be greater to or less than the value of the previous UTXO, with the exact balance determined by market forces rather than hardcoded by developers. In addition to the economic and security benefits of the ATR payout, we note that permanent data storage becomes possible through this mechanism.

## 5. ADVANCED SAITO

Additional mechanisms which increase network robustness:

Saito requires all valid chains to contain N golden tickets over the last M blocks. Forks are considered invalid unless they meet minimal hashing requirements.

Routing policies at the block level allow nodes to ensure peers are following sensible routing policies and not spamming the network or relaying malicious blocks.

Block producers can be required to affix tokens (making them unspendable for X blocks) when producing blocks. Slashing these locked tokens is possible in some situations.


### APPENDIX I: SAITO TERMINOLOGY

**Paysplit:** a variable between 0 and 1 that determines the percentage of the block reward that is allocated to mining nodes.

**Powsplit:** a variable between 0 and 1 that determines the target percentage of blocks desired to contain golden tickets.

**Golden Ticket:** a transaction from a miner containing a valid solution to the computational lottery puzzle embodied in the previous block hash.

**Genesis Period:** the length of the epoch in number of blocks.




