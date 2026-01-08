---
title: Saito Consensus Mechanism
description: Consensus Mechanism
published: true
date: 2026-01-08T16:13:19.773Z
tags: 
editor: markdown
dateCreated: 2022-02-17T10:09:00.217Z
---

# Saito Consensus

Readers with backgrounds in economics, distributed systems, and mechanism design are encouraged to visit our [theory section](/consensus/theory), which connects the problems Saito addresses to the literature in each field and shows where Saito is and is not constrained by traditional impossibility results.

The remainder of this page offers a technical overview of the protocol starting from the perspective of a user who sends a transaction they want included in the blockchain. It explains first how blocks are produced and then covers how the fees are securely redistributed to the fee-collecting nodes in the network.


### 1. HOW BLOCKS ARE PRODUCED

When users send transactions into the network they add cryptographic routing signatures which specify the first-hop node(s) to which they are sending their transactions. Nodes add similar signatures as they relay these transactions onwards to their own peers. As a result, all transactions included in blocks contain an unforgeable record of the path they have travelled from their originating user to the node that included it in a block.

Nodes compete to collect transactions to secure a kind of "routing work" that is used to produce blocks. The amount of routing work in any transaction consists of the transaction fee halved with every hop beyond the first that the transaction has travelled into the network. A transaction with a 10 SAITO fee offers 1st-hop nodes 10 units of routing work, 2nd-hop nodes 5 units of routing work, 3rd-hop nodes 2.5 units of routing work, and so on.

Consensus adjusts the amount of "routing work" that nodes needs to propose blocks to target a desired blocktime: if blocks are produced more rapidly the "burn fee" rises, and if blocks are produced more slowly the "burn fee" falls. This difficulty criteria is known as the "burn fee" as once the block is produced all of the fees paid by the transactions within it are burned. This establishes a baseline cost that must be paid in equilibrium to propose a block.

### 2. HOW NODES ARE PAID

Once a block is produced a hashing competition begins. The competition works similarly to the mining puzzle in proof-of-work, except that instead of competing for the right to produce blocks, miners are competing for the right to resurrect and distribute the fees that were burned in the previous block.

If a golden ticket for block N is included in the very next block (N+1), consensus divides those fees between the miner that found the solution and a random routing node from the routing paths of one of the transactions in the previous block. The block producer is eligible to win as the last hop in the routing path of every transation, but other nodes may win as well.

The lottery first selects a transaction from the block, with each transaction weighted by its share of overall fees in the block. The random solution is then hashed again to select a routing hop from the winning transaction, with each hop weighted by its share of routing work in the path. For a transaction with a 2-hop routing path and a 10 SAITO fee, the 1st-hop has a 10/5 chance of payout while the 2nd-hop has a 5/15 chance. In a transaction with a 3-hop routing path and a 10 SAITO fee the 1st-hop has a 10/17.5 chance of payout, while the 2nd-hop has a 5/17.5 chance of payout and the third has a 2.5/17.5 chance of payout, etc.

This process repeats block by block. Nodes burn in-network tokens to produce blocks, and then burn ex-network hash to resurrect them. Hashing difficulty adjusts upward if two blocks in a row are produced with golden tickets, and downwards if two blocks in a row are produced without golden tickets. This basic implementation achieves cost-of-attack at the price of significant deflationary pressure from the blocks whose fees are burned but never resurrected and redistributed by a golden ticket.

### 3. AUTOMATIC TRANSACTION REBROADCASTING (ATR)

ATR divides the blockchain into epochs of N blocks. Once a block falls out of the current epoch, its unspent transaction outputs (UTXO) become unspendable. But any UTXO which meet rebroadcast criteria must be re-included in the next block in ATR transactions. These transactions include the original transaction as embedded data, but provide new UTXO spendable by the original address.

The criteria for rebroadcasting is that the UTXO is unspent and contains enough tokens to pay a rebroadcasting fee. The rebroadcasting fee is equal to or greater than the average fee per byte paid by new transactions over the previous epoch.

The UTXO may also be issued a staking payout on rebroadcasting. This ATR payout improves cost-of-attack by pulling fees away from attackers who spend their own money to produce blocks. It also improves censorship-resistance because attackers who prevent users from making transactions are forcing them into a state where the attacker must transfer them income. In addition to the economic and security benefits of this approach, we note that permissionless and permanent data storage finally becomes possible and economically sustainable through this mechanism. Anyone who wants the blockchain to store their data in perpetuity need only attach a large enough UTXO that the ATR payout issued matches or is greater than the ATR fee collected.

### IN CLOSING

For details on implementation refinements and security mitigations, see our [implementation nodes](/consensus/implementation-notes).

