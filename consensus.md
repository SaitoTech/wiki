---
title: Saito Consensus Mechanism
description: Consensus Mechanism
published: true
date: 2024-05-23T12:11:18.439Z
tags: 
editor: markdown
dateCreated: 2022-02-17T10:09:00.217Z
---

# Saito Consensus

Saito Consensus eliminates the [sybil attacks](/consensus/sybil-proof),  [majoritarian attacks](/consensus/majoritarian-attacks),and several other [attack vectors](/consensus/attack-vectors) common in proof-of-work and proof-of-stake consensus mechanisms by correcting the collective action problems buried in their incentive structures. This page offers a brief introduction to how consensus works.

## 1. PRODUCING BLOCKS

When users send transactions into the network they add cryptographic routing signatures that specify the first-hop node(s) to which they are sending their transaction(s). Nodes add similar signatures as they relay these transactions to their own peers. This gives all transactions an unforgeable record of the path they have taken into the network.

The amount of routing work in any transaction is derived from its chain of signatures. It is the total fee halved with every hop beyond the first that the transaction has taken into the network. Nodes gather transactions until they have enough routing work to meet a difficulty criteria maintained by consensus. Blocks without adequate routing work are invalid by consensus rules.

## 2. THE PAYMENT LOTTERY

When a block is produced all of the fees in it are burned. But miners may start hashing to solve a mining puzzle that will resurrect these burned fees and bring them back into circulation. We call the solution to this puzzle the golden ticket.

If a golden ticket solving the previous block (block N) is included in its very next block (block N+1), consensus issues a payout worth the average fees burned over the last epoch. In the classic Saito mechanism, half are paid to the miner that found the golden ticket and half are paid to a random routing node from the routing signatures embedded in the block. The block producer is eligible for this payment as the last routing node.

A weighted lottery is used to select the winning routing node. A random hash in the golden ticket is first hashed to pick a random transaction from the previous block, with each transaction's chance of selection weighted to reflect by its share of fees in the block. The random hash that selected the transaction is then hashed again to select a node from the routing path of that winning transaction, with each router's chance of selection weighted according to its share of the total routing work held by all nodes at all positions in that routing path. In a 2-hop routing path the first hop has a 2/3 chance of payout while the second has a 1/3 chance. In a 3-hop routing path the first hop has a 10/17.5 chance of payout, while the second hop has a 5/17.5 chance of payout and the third has a 2.5/17.5 chance of payout, etc.

This process repeats block by block as nodes burn money to produce blocks, and then burn energy to resurrect payments. This creates a game that is profitable for honest nodes who process user-paid fees, but costly anyone who must spend their own money to generate routing work and attack the chain.

## 3. IMPROVING SECURITY

To improve security and prevent deflation Saito adds recursive payouts and a ATR payout. The way that recursive payouts work is that whenever a golden ticket is included in block N the block producer for that block must include the payouts for block N-1 as described above. But if block N-1 did not contain a golden ticket, the block producer must recurse to block N-2 and hash the golden ticket again to issue a router payout for that block.

The missing "miner" payout from block N-2 is collected by consensus and placed in a treasury that is used to issue payouts to the oldest unspent UTXO in the blockchain as part of the ATR mechanism described below.

## 4. AUTOMATIC TRANSACTION REBROADCASTING (ATR)

ATR divides the blockchain into epochs of N blocks. Once a block falls out of the current epoch, its unspent transaction outputs (UTXO) become unspendable. But any UTXO which meet rebroadcast criteria must be re-included in the next block in ATR transactions. These transactions include the original transaction as embedded data, but provide new UTXO spendable by the original address.

The criteria for rebroadcasting is that the UTXO is unspent and contains enough tokens to pay a rebroadcasting fee. The rebroadcasting fee is equal to or greater than the average fee per byte paid by new transactions over the previous epoch.

The UTXO may also be issued a staking payout on rebroadcasting. This ATR payout improves cost-of-attack by pulling fees away from attackers who spend their own money to produce blocks. It also improves censorship-resistance because attackers who prevent users from making transactions are forcing them into a state where the attacker must transfer them income. In addition to the economic and security benefits of this approach, we note that permissionless and permanent data storage finally becomes possible and economically sustainable through this mechanism. Anyone who wants the blockchain to store their data in perpetuity need only attach a large enough UTXO that the ATR payout issued matches or is greater than the ATR fee collected.

## 5. ADVANCED SAITO

Additional mechanisms which increase network robustness:

* consensus can maintain a smoothed average of the fees included in each block over the last epoch. in the event that the block reward spikes well in excess of this smoothed average, the excess portion can be burned for good. This adds a deflationary burn which penalizes attackers who use their own tokens to attack the network.

* consensus can maintain a smoothed average of the fee-throughput to aggregate routing depth over the last epoch. in the event that this ratio decreases significantly, the block reward can automatically reduced with a deflationary burn. This adds a deflationary burn which penalizes attackers who use their own tokens to attack the network.

* consensus can requires all valid chains to contain N golden tickets over the last M blocks and declare forks unextendable unless they meet these minimal hashing requirements. This provides wrap-around spam-resistance to cash-only attacks at the cost of making halting attacks theoretically possible for attackers with unlimited hashpower.

* routing policies at the block level can be added to incentivize nodes to following sensible routing policies and not spam the network or relay malicious blocks, while also speeding up relay speeds for valid blocks from honest producers.

* block producers can be required to affix tokens (making them unspendable for X blocks and ineligible for the ATR payout) when producing blocks. Social slashing of these locked tokens is possible in some situations, permitting even low fee-throughput chains to maintain a high cost-of-attack.


### APPENDIX I: SAITO TERMINOLOGY

**Paysplit:** a variable between 0 and 1 that determines the percentage of the block reward that is allocated to mining nodes.

**Powsplit:** a variable between 0 and 1 that determines the target percentage of blocks desired to contain golden tickets.

**Golden Ticket:** a transaction from a miner containing a valid solution to the computational lottery puzzle embodied in the previous block hash.

**Genesis Period:** the length of the epoch in number of blocks.




