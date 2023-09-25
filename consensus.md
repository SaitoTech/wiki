---
title: Saito Consensus Mechanism
description: Consensus Mechanism
published: true
date: 2023-09-25T06:16:13.543Z
tags: 
editor: markdown
dateCreated: 2022-02-17T10:09:00.217Z
---

# Saito Consensus

Saito Consensus eliminates the [sybil attacks](/consensus/sybil-proof), [majoritarian attacks](/consensus/majoritarian-attacks), [collective action problems](/consensus/economics) and other [attack vectors](/consensus/attack-vectors) common in proof-of-work and proof-of-stake class of consensus mechanisms.

## 1. PRODUCING BLOCKS

When users send transactions into the network they add cryptographic routing signatures that specify the first-hop node(s) to which they are sending their transaction(s). Receiving nodes add similar routing signatures as they propagate these transactions, creating an unforgeable record within transactions of the path they have taken into the network.

These routing paths can be examined to confirm the amount of "routing work" available in a transaction. Transactions without a valid routing path contain no routing work. The amount in any other transaction is the total fee paid by the transaction divided in half with each hop beyond the first that the transaction has taken into the network.

The blockchain maintains a "difficulty" for block production that is measured in routing work. Nodes produce blocks when they have enough routing work in the transactions in their mempool to meet this difficulty criteria. Blocks which do not contain the required amount of routing work are invalid according to consensus rules.


## 2. THE PAYMENT LOTTERY

When a block is produced all of the fees in the block are burned. Miners then start hashing to find a golden ticket that will solve the block that has already been produced.

If a golden ticket for block N is included in the very next block (N+1), consensus issues a payout worth the average fees burned per block over the last epoch. Half are paid to the miner that found the golden ticket and half are issued to a node that routed transactions into the block.

The routing node is selected by using a random number associated with the golden ticket to pick a random transaction from the previous block (weighted by share of fees burned). A second random number is then used to select a node from the routing path of the winning transaction (weighted by its share of the aggregate routing work held by all nodes in that routing path).

This process repeats block by block. Nodes burn money to produce blocks, and then burn energy to release payments, creating a game that is profitable for honest nodes who burn user-paid fees, but costly for attackers who are forced to spend more than they can collect to outpace the honest chain.

## 3. IMPROVING SECURITY

The "Classic Saito" design produces one golden ticket every two blocks on average and accepts deflation from unsolved blocks.

To avoid deflation Saito introduces recursive payouts and a ATR payout. Whenever a golden ticket is included in block N consensus includes a payout for block N-1 as described above. Once this payout is completed, if block N-1 did not contain a golden ticket, we recurse to block N-2 and repeat the process and issue a router payout for that block.

The missing "miner" payout from block N-2 is collected by consensus for eventual distribution to the UTXO holders in the network as part of the ATR mechanism described below.

## 4. AUTOMATIC TRANSACTION REBROADCASTING (ATR)

ATR divides the blockchain into epochs of N blocks. Once a block falls out of the current epoch, its unspent transaction outputs (UTXO) become unspendable. But any UTXO which meet rebroadcast criteria must be re-included in the next block in ATR transactions. These transactions include the original transaction as embedded data, but provide new UTXO spendable by the original address.

The criteria for rebroadcasting is that the UTXO is unspent and contains enough tokens to pay a rebroadcasting fee. The rebroadcasting fee is equal to or greater than the average fee per byte paid by new transactions over the previous epoch.

The UTXO may also be issued a staking payout on rebroadcasting. This improves censorship-resistance by ensuring attackers who prevent users from making transactions are transferring them income. In addition to the economic and security benefits of this approach, we note that permissionless and permanent data storage finally becomes possible and economically sustainable through this mechanism.

## 5. ADVANCED SAITO

Additional mechanisms which increase network robustness:

Saito Consensus maintains a smoothed average of the fees included in each block over the last epoch. In the event that the block reward spikes in serious excess of this smoothed average, the payout can be reduced and the excess portion burned for good. This add a deflationary burn to the network which only kicks in when the network is under attack.

Saito requires all valid chains to contain N golden tickets over the last M blocks. Forks are considered invalid unless they meet minimal hashing requirements. This provides wrap-around spam-resistance to cash-only attacks.

Routing policies at the block level allow nodes to ensure peers are following sensible routing policies and not spamming the network or relaying malicious blocks.

Block producers can be required to affix tokens (making them unspendable for X blocks) when producing blocks. Social slashing of these locked tokens is possible in some situations.


### APPENDIX I: SAITO TERMINOLOGY

**Paysplit:** a variable between 0 and 1 that determines the percentage of the block reward that is allocated to mining nodes.

**Powsplit:** a variable between 0 and 1 that determines the target percentage of blocks desired to contain golden tickets.

**Golden Ticket:** a transaction from a miner containing a valid solution to the computational lottery puzzle embodied in the previous block hash.

**Genesis Period:** the length of the epoch in number of blocks.




