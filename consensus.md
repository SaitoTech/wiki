---
title: Saito Consensus Mechanism
description: Consensus Mechanism
published: true
date: 2025-04-08T19:16:57.716Z
tags: 
editor: markdown
dateCreated: 2022-02-17T10:09:00.217Z
---

# Saito Consensus

Saito Consensus is a distributed consensus mechanism provably secure against a specific type of [routing attack](/consensus/sybil-attacks) considered impossible to solve in other consensus mechanisms. It is also believed to be [incentive compatible](/consensus/incentive-compatibility) and secure against the [majoritarian attacks](/consensus/majoritarian-attacks) common in proof-of-work and proof-of-stake mechanisms. This page offers a brief overview of how consensus works.

## 1. HOW BLOCKS ARE PRODUCED

When users send transactions into the network they add cryptographic routing signatures which specify the first-hop node(s) to which they are sending their transactions. Nodes add similar signatures as they relay these transactions onwards to their own peers. As a result, all transactions ciculating on the network have an unforgeable record of the path they have taken into the network from their originating user to the node that holds them in its mempool.

All unconfirmed transactions offer "routing work" to the nodes that possess them. The amount of routing work in any transaction consists of the transaction fee halved with every hop beyond the first that the transaction has taken into the network. A transaction with a 10 SAITO fee offers 1st-hop nodes 10 units of routing work, 2nd-hop nodes 5 units of routing work, 3rd-hop nodes 2.5 units of routing work, and so on.

Nodes gather transactions in their mempool until they have enough routing work to meet a difficulty criteria maintained by consensus for the production of a block. We refer to this difficulty as the "burn fee" as when the block is produced all transaction fees in the block are burned. This "burn fee" is automatically adjusted by consensus to target a desired blocktime: If blocks are produced more rapidly the "burn fee" rises, and if blocks are produced more slowly the "burn fee" falls.

## 2. HOW PAYMENTS ARE ISSUED

Once a block is produced all fees in the block are burned. A hashing competition then begins which may resurrect them. This competition works similarly to the hashing puzzle in proof-of-work, except that finding a solution controls whether the fees in the previous block will be resurrected and who will receive payment rather than who has the right to extend the chain.

If a golden ticket for block N is included in the very next block (N+1), consensus issues a payout to the miner that found the solution and a random routing node. The block producer is eligible to win as the last hop in the routing path of every transation, but other nodes may win as well.

The lottery works as follows. We hash the mining solution to choose a transaction weighted by its share of overall fees in the block. We then hash the solution again to select a routing hop from the winning transaction, with each hop weighted by its share of routing work in the path. For a transaction with a 2-hop routing path and a 10 SAITO fee, the 1st-hop has a 10/5 chance of payout while the 2nd-hop has a 5/15 chance. In a transaction with a 3-hop routing path and a 10 SAITO fee the 1st-hop has a 10/17.5 chance of payout, while the 2nd-hop has a 5/17.5 chance of payout and the third has a 2.5/17.5 chance of payout, etc.

This process repeats block by block. Nodes burn network tokens to produce blocks, and then burn hash to resurrect fees. Hashing difficulty adjusts upward if two blocks in a row are produced with golden tickets, and downwards if two blocks in a row are produced without golden tickets. This achieves cost-of-attack at the price of significant deflationary pressure from the blocks whose fees are burned but never resurrected and redistributed by a golden ticket.


## 3. IMPROVING SECURITY AND PREVENTING DEFLATION

Security can be improved by using the same hash-solution to payout multiple blocks. When a golden ticket is included in a block (N), we calculate the winner of block (N-1) as described above. If block (N-1) did not contain a golden ticket, we hash the golden ticket again to find and issue a router payout for block (N-2).

Any missing "miner" payout from block (N-2) is collected by consensus and placed in a treasury. This treasury will issue payments to the unspent UTXO in the blockchain as part of the ATR mechanism described in the next section. If these unspent UTXO are well distributed, the ATR payout further increases cost-of-attack on the network as any attacker who is spending their own tokens to attack the network must redirect a portion to any users whose transactions they are censoring.

## 4. AUTOMATIC TRANSACTION REBROADCASTING (ATR)

ATR divides the blockchain into epochs of N blocks. Once a block falls out of the current epoch, its unspent transaction outputs (UTXO) become unspendable. But any UTXO which meet rebroadcast criteria must be re-included in the next block in ATR transactions. These transactions include the original transaction as embedded data, but provide new UTXO spendable by the original address.

The criteria for rebroadcasting is that the UTXO is unspent and contains enough tokens to pay a rebroadcasting fee. The rebroadcasting fee is equal to or greater than the average fee per byte paid by new transactions over the previous epoch.

The UTXO may also be issued a staking payout on rebroadcasting. This ATR payout improves cost-of-attack by pulling fees away from attackers who spend their own money to produce blocks. It also improves censorship-resistance because attackers who prevent users from making transactions are forcing them into a state where the attacker must transfer them income. In addition to the economic and security benefits of this approach, we note that permissionless and permanent data storage finally becomes possible and economically sustainable through this mechanism. Anyone who wants the blockchain to store their data in perpetuity need only attach a large enough UTXO that the ATR payout issued matches or is greater than the ATR fee collected.

## 5. ADVANCED SAITO

Additional mechanisms which increase network robustness:

* consensus can easily maintain a smoothed average of the fees included in each block over the last epoch. in the event that the fees-in-block spike well in excess of this smoothed average, the excess portion can be burned. This provides an additional penalty for attackers who use their own tokens to self-generate routing-work in an attempt to outpace the honest chain.

* consensus can require all valid chains to contain N golden tickets over the last M blocks. This provides wrap-around form of spam/sybil resistance at the cost of making halting attacks theoretically possible. Our production design requires 33% of blocks to have golden tickets.

* routing policies can be used to incentivize nodes to follow honest routing policies and not spam the network or relay malicious blocks / amplify block-flooding attacks. This approach may also be used to increase relaying speeds for valid blocks from honest producers.

* block producers may be required to affix tokens (making them unspendable for X blocks and ineligible for the ATR payout) when producing blocks. Social slashing of these locked tokens is possible in some situations, permitting even low fee-throughput chains to maintain a high cost-of-attack.


### APPENDIX I: SAITO TERMINOLOGY

**Paysplit:** a variable between 0 and 1 that determines the percentage of the block reward that is allocated to mining nodes.

**Powsplit:** a variable between 0 and 1 that determines the target percentage of blocks desired to contain golden tickets.

**Golden Ticket:** a transaction from a miner containing a valid solution to the computational lottery puzzle embodied in the previous block hash.

**Genesis Period:** the length of the epoch in number of blocks.




