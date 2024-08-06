---
title: Saito Consensus Mechanism
description: Consensus Mechanism
published: true
date: 2024-08-06T16:57:12.560Z
tags: 
editor: markdown
dateCreated: 2022-02-17T10:09:00.217Z
---

# Saito Consensus

Saito Consensus eliminates the [sybil attacks](/consensus/sybil-proof),  [majoritarian attacks](/consensus/majoritarian-attacks),and several other [attack vectors](/consensus/attack-vectors) common in proof-of-work and proof-of-stake consensus mechanisms by correcting the collective action problems buried in their incentive structures. This page offers a brief introduction to how consensus works.

## 1. HOW BLOCKS ARE PRODUCED

When users send transactions into the network they add cryptographic routing signatures that specify the first-hop node(s) to which they are sending their transaction(s). Nodes add similar signatures as they relay these transactions to their own peers. As a result, when a block is produced all of its transactions have an unforgeable record of the path they have taken into the network.

The amount of routing work in any transaction is derived from its transaction fee and this chain of signatures. It consists of the transaction fee halved with every hop beyond the first that the transaction has taken into the network. A transaction with a 10 SAITO fee offers 1st-hop nodes 10 units of routing work, 2nd-hop nodes 5 units of routing work, and so on.

Nodes gather transactions until they have enough routing work to meet a difficulty criteria maintained by consensus that auto-adjusts to keep blocktime reasonably constant. We refer to this difficulty level as the "burn fee" as when the block is produced all of the transaction fees included in the block are burned.

## 2. HOW PAYMENTS ARE ISSUED

Once a block is produced miners may start hashing to solve a mining puzzle based on the block hash similar to proof-of-work. We call the solution to this puzzle the golden ticket.

If a golden ticket for block N is included in the very next block (N+1), consensus issues a payout to the miner that found the solution and a random routing node selected from the transactions in the block. The block producer is eligible to win this routing payout as it is the last routing hop in every transaction, but other nodes may win as well.

A weighted lottery selects the winning routing node as follows. A random nonce from the golden ticket is hashed to select a transaction from the previous block, with each transaction's chance of selection weighted based on its fee's share of the total fees in the block. That number is then hashed again to select a node from the routing path of the winning transaction, with each router's chance of selection weighted according to its share of the total routing work in that routing path. In a transaction with a 2-hop routing path and a 10 SAITO fee, the first hop has a 10/5 chance of payout while the second has a 5/15 chance. In a transaction with a 3-hop routing path and a 10 SAITO fee the first hop has a 10/17.5 chance of payout, while the second hop has a 5/17.5 chance of payout and the third has a 2.5/17.5 chance of payout, etc.

This process repeats block by block. Nodes burn fees to produce blocks, and then burn hashpower to resurrect fees. This creates a game that is profitable for honest nodes to play, but costly for attackers who must spend their own money to generate the fake routing work needed to orphan blocks produced more efficiently by other nodes.

## 3. IMPROVING SECURITY

To improve security and prevent deflation (from unsolved blocks) Saito adds recursive payouts and a ATR payout. Whenever a golden ticket is included in a block (N) that block must include the payouts for the previous block (N-1) as described above. If block N-1 did not contain a golden ticket, the block producer recurses to block N-2 and hashes the golden ticket again to issue a router payout for block N-2.

The missing "miner" payout from block N-2 is collected by consensus and placed in a treasury that issues payouts to the oldest unspent UTXO in the blockchain as part of the ATR mechanism described below. The mining payout may also be smoothed in this fashion.

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




