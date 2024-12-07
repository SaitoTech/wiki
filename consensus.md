---
title: Saito Consensus Mechanism
description: Consensus Mechanism
published: true
date: 2024-12-07T20:11:13.418Z
tags: 
editor: markdown
dateCreated: 2022-02-17T10:09:00.217Z
---

# Saito Consensus

Saito Consensus is a distributed consensus mechanism provably secure against a specific type of [routing attack](/consensus/sybil-attacks) considered impossible to solve in other consensus mechanisms. It is also believed to be secure against the [majoritarian attacks](/consensus/majoritarian-attacks) common in proof-of-work and proof-of-stake mechanisms. This page offers a brief overview of how consensus works.

## 1. HOW BLOCKS ARE PRODUCED

When users send transactions into the network they add cryptographic routing signatures to these transactions specify the first-hop node(s) to which they are sending them. Nodes add similar signatures as they relay these transactions onwards to their own peers. As a result, all transactions ciculating on the network have an unforgeable record of the path they have taken into the network from their originating user to the node that holds them in its mempool.

All unconfirmed transactions offer "routing work" to the nodes that possess them. The amount of routing work in any transaction consists of the transaction fee halved with every hop beyond the first that the transaction has taken into the network. A transaction with a 10 SAITO fee offers 1st-hop nodes 10 units of routing work, 2nd-hop nodes 5 units of routing work, 3rd-hop nodes 2.5 units of routing work, and so on.

Nodes gather transactions until they have enough routing work to meet a difficulty criteria maintained by consensus. We refer to this difficulty level as the "burn fee" as when the block is produced all of the transaction fees included in the block are burned. This "burn fee" is automatically adjusted by consensus over time to keep blocktime constant as fee-throughput changes. If several blocks are produced in rapid succession the "burn fee" adjusts upwards to make it more expensive to produce blocks. And if a longer period passes without a block the "burn fee" is reduced.

## 2. HOW PAYMENTS ARE ISSUED

Once a block is produced all of the fees in the block are burned. This ensures that attackers who spend their own money to produce blocks always face a tax for doing so. Once a block has been published a cryptographic hashing puzzle starts that has the ability to resurrect and distribute the fees. This puzzle works similarly to proof-of-work -- the goal is to find a computationally difficult hash linked to the previous block -- except here the hashpower is determining whether the fees in the previous block will be resurrected and paid-out rather than who has the right to extend the chain. This ensures majority hash is not sufficient to control the chain.

If a golden ticket for block N is included in the very next block (N+1), consensus issues a payout to the miner that found the solution and a random routing node who contributed to the previous block. The block producer is eligible to win this routing payout as the last hop in the routing path of every transation, but other nodes may win as well. The exact amount of the payout can vary, as under certain conditions where fee-throughput spikes rapidly the consensus mechanism will initiate a deflationary burn to ensure less is paid out than collected.

The process of picking a winner is as follows. We hash the golden ticket solution to choose a transaction from the block, with the chance of each transaction winning weighted according to its share of all fees in the block. That hash is then hashed again to select a hop from the routing path of the winning transaction, with each hop weighted according to its share of the total sum of routing work in the routing path. For a transaction with a 2-hop routing path and a 10 SAITO fee, the 1st-hop has a 10/5 chance of payout while the 2nd-hop has a 5/15 chance. In a transaction with a 3-hop routing path and a 10 SAITO fee the 1st-hop has a 10/17.5 chance of payout, while the 2nd-hop has a 5/17.5 chance of payout and the third has a 2.5/17.5 chance of payout, etc.

This process repeats block by block. Nodes burn fees to produce blocks, and then burn hash to resurrect fees. If no golden ticket is found all of the fees from the previous block remain burned.

A naive implementation of the above would target a hashing difficulty that averages one golden ticket every two blocks. This can be done by increasing mining difficulty if two blocks in a row are found with golden tickets and decreasing mining difficulty if two blocks in a row are found without golden tickets. This ensures the cost to any node of getting paid always averages half of the fees in the block, but achieves cost-of-attack at the cost of accepting significant deflationary pressure from the blocks whose fees are burned but never resurrected and redistributed by a golden ticket.

## 3. IMPROVING SECURITY AND PREVENTING DEFLATION

When a golden ticket is included in a block (N), qw calculate the winner of bock (N-1) as described above. If block N-1 did not contain a golden ticket, we hash the golden ticket again to find and issue a router payout for block N-2. Block producers who wish to guarantee they recover the routing payout must now do a significantly larger amount of hashing as the difficulty of finding a single solution that pays out two blocks is larger than finding two successive solutions that each pay out a single block.

The missing "miner" payout from block N-2 is collected by consensus and placed in a treasury that issues payouts to the oldest unspent UTXO in the blockchain as part of the ATR mechanism described below. We refer to these payouts as the ATR payouts -- they are directed to the holders of UTXO which are looping around the chain. If these unspent UTXO are well distributed -- a non-trivial amount do not belong to the attacker -- the ATR payout further increases cost-of-attack on the network. If all outstanding UTXO are in the possession of the attacker cost-of-attack is reduced but still exists.

## 4. AUTOMATIC TRANSACTION REBROADCASTING (ATR)

ATR divides the blockchain into epochs of N blocks. Once a block falls out of the current epoch, its unspent transaction outputs (UTXO) become unspendable. But any UTXO which meet rebroadcast criteria must be re-included in the next block in ATR transactions. These transactions include the original transaction as embedded data, but provide new UTXO spendable by the original address.

The criteria for rebroadcasting is that the UTXO is unspent and contains enough tokens to pay a rebroadcasting fee. The rebroadcasting fee is equal to or greater than the average fee per byte paid by new transactions over the previous epoch.

The UTXO may also be issued a staking payout on rebroadcasting. This ATR payout improves cost-of-attack by pulling fees away from attackers who spend their own money to produce blocks. It also improves censorship-resistance because attackers who prevent users from making transactions are forcing them into a state where the attacker must transfer them income. In addition to the economic and security benefits of this approach, we note that permissionless and permanent data storage finally becomes possible and economically sustainable through this mechanism. Anyone who wants the blockchain to store their data in perpetuity need only attach a large enough UTXO that the ATR payout issued matches or is greater than the ATR fee collected.

## 5. ADVANCED SAITO

Additional mechanisms which increase network robustness:

* consensus can maintain a smoothed average of the fees included in each block over the last epoch. in the event that the fees-in-block spike well in excess of this smoothed average, the excess portion can be burned. This adds a deflationary burn which penalizes attackers who use their own tokens to attack the network, as attacks must push fee-throughput significantly about the pre-attack average in any attempt to subvert the lottery.

* consensus can requires all valid chains to contain N golden tickets over the last M blocks and declare forks unextendable unless they meet these minimal hashing requirements. This provides wrap-around spam-resistance at the cost of making halting attacks theoretically possible for attackers with unlimited hashpower.

* routing policies at the block level can be added to incentivize nodes to follow sensible routing policies and not spam the network or relay malicious blocks, while also speeding up relay speeds for valid blocks from honest producers.

* block producers can be required to affix tokens (making them unspendable for X blocks and ineligible for the ATR payout) when producing blocks. Social slashing of these locked tokens is possible in some situations, permitting even low fee-throughput chains to maintain a high cost-of-attack.


### APPENDIX I: SAITO TERMINOLOGY

**Paysplit:** a variable between 0 and 1 that determines the percentage of the block reward that is allocated to mining nodes.

**Powsplit:** a variable between 0 and 1 that determines the target percentage of blocks desired to contain golden tickets.

**Golden Ticket:** a transaction from a miner containing a valid solution to the computational lottery puzzle embodied in the previous block hash.

**Genesis Period:** the length of the epoch in number of blocks.




