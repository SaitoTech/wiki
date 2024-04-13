---
title: Saito Consensus Mechanism
description: Consensus Mechanism
published: true
date: 2024-04-13T06:52:17.987Z
tags: 
editor: markdown
dateCreated: 2022-02-17T10:09:00.217Z
---

# Saito Consensus

Saito Consensus eliminates the [sybil attacks](/consensus/sybil-proof),  [majoritarian attacks](/consensus/majoritarian-attacks),and several other [attack vectors](/consensus/attack-vectors) common in proof-of-work and proof-of-stake consensus mechanisms by correcting the collective action problems buried in their incentive structures. This page offers a brief introduction to how consensus works.

## 1. PRODUCING BLOCKS

When users send transactions into the network they add cryptographic routing signatures that specify the first-hop node(s) to which they are sending their transaction(s). Receiving nodes add similar signatures as they relay these transactions, creating an unforgeable record of the path transactions have taken into the network.

The blockchain maintains a "difficulty" for block production that specifies the amount of "routing work" blocks are required to contain. Nodes produce blocks when their mempool contains enough valid transactions to meet this criteria. Any blocks without adequate routing work are invalid by consensus rules.

The amount of routing work in any other transaction is its total fee halved with every hop beyond the first that the transaction has taken into the network. Transactions without a valid routing path connecting the block producer to the sending user contain no routing work. 

## 2. THE PAYMENT LOTTERY

When a block is produced all of the fees in the block are burned. But miners may start hashing to find a golden ticket that will trigger the resurrection of the burned fees and bring them back into circulation.

If a golden ticket for the previous block (block N) is included in the very next block (block N+1), consensus issues a payout worth the average fees burned per block over the last epoch. Half are paid to the miner that found the golden ticket and half are paid to a routing node.

The routing node is selected by using a two-part weighted lottery. A random number associated with the golden ticket is first hashed to pick a random transaction from the previous block, which each transaction's chance of selection weighted by its share of fees contributed to the block. The number is then hashed again to select a node from the routing path of the winning transaction, with each participant's chance of selected weighted according to its share of the aggregate routing work held by all nodes at all positions in that routing path.

This process repeats block by block. The network burns money to produce blocks, and then burns energy to resurrect payments. This creates a game that is profitable for honest nodes who proffer user-paid fees for burning, but costly for attackers who must spend more than they can ever collect to outpace the honest chain.

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




