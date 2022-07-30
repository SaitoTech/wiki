---
title: Saito Consensus Mechanism
description: Consensus Mechanism
published: true
date: 2022-07-30T05:44:25.144Z
tags: 
editor: markdown
dateCreated: 2022-02-17T10:09:00.217Z
---

# Saito Consensus

This page offers a straight-forward description of how Saito Consensus works. We have separate pages explaining how Saito eliminates common [attack vectors](/consensus/attack-vectors), a brief [math paper](/consensus/math) demonstrating cost-of-attack properties and [open proposals](/consensus/proposals) on technical implementation. You may also be interested in the [economic problems](/consensus/economics) Saito Consensus solves and [critical videos](/consensus/videos) covering the mechanism.

## 1. PRUNING THE BLOCKCHAIN

Saito divides the blockchain into "epochs" of N blocks. If the latest block is 500,000 and N is 100,000 blocks, then the current epoch streches from block 400,001 onwards.

Once a block falls out of the current epoch, its unspent transaction outputs (UTXO) are considered invalid by consensus rules. Any UTXO from that block which contains enough tokens to pay a rebroadcasting fee must be re-included by the producer of the next block for that block to be considered valid. The rebroadcasting fee is twice the average fee per byte paid by new transactions as determined over a smoothing period.

Block producers rebroadcast UTXO slips by creating special "automatic transaction rebroadcasting" (ATR) transactions. These ATR transactions include the original transaction as embedded data, but come with new UTXO. Each UTXO that meets rebroadcast criteria is rebroadcast in a separate ATR transaction at present although there is room for optimization here. The rebroadcasting fee is deducted from each UTXO and added to the block reward. After two epochs block producers will no longer require access to historical block data, but are required to retain the 32-byte header hash to prove the connection with the genesis block.

## 2. PRODUCING BLOCKS

Saito adds cryptographic signatures to transactions. When users make transactions they sign the core data and then add a separate routing signature that specifies the node to which they are forwarding their transaction. Should users send their transactions to two different nodes they thus create variant "transaction-bunles" which have the same core data but different routing paths. As nodes receive and forward transactions they add their own signatures to these chains, giving all transactions an unforgeable record of the path they have taken into the network. This dynamic means that the same transaction in different mempools will have the same core data but a different set of routing signatures.

The blockchain now sets a "difficulty" for block production that can be met by producing a block that contains enough "routing work". The amount of "routing work" in any block is the aggregate of the "routing work" contained in the transactions that the block producer includes in the block. The amount of "routing ork" in any transaction is the value of its transaction fee halved with each additional hop beyond the first that the transaction has taken into the network.

The usefulness of transactions for producing blocks falls as their routing path grows. And transactions provide no "routing work" to nodes that are not contained in their routing paths. Block production difficulty in Saito Consensus consequently reflects the difficulty of collecting fees (efficiently) from network users and sharing them with other peers on the network.

Once the block is produced all of the fees in the block are burned. Honest nodes thus make blocks free-of-charge using transactions which have been routed to them. Attackers must spend (and burn) their own money to produce blocks.

## 3. THE PAYMENT LOTTERY

Each block contains a proof-of-work challenge. When a block is produced miners try to solve it. Should they find a solution they broadcast it into the network as part of a "golden ticket". The golden ticket is designed so that it cannot be forged or stolen in-transit.

If a valid golden ticket is included in the next block, Saito will resurrect the burned block reward. The payments in block N+1 are thus for the block reward burned in block N. The block reward for block N+1 is then burned and the process is repeated.

When a block is solved in block N+1, the payment for block N is the block reward from block N split between the miner that found the solution and a routing node selected using the random number associated with the winning hash. That random number is hashed to select a winning transaction in the block, with transactions weighted according to their share of fees in overall block. The random number is then hashed again to select a routing node from the list of nodes in the routing paths in that transaction. The chance that nodes in that path have of winning is weighted according to their individual share of routing work over the aggregate amount generated.\footnote[1]{If a transaction paying a 10 SAITO fee passes through two relay nodes before its inclusion in a block, the first relay node is deemed to have done 10 / 17.5 percent (57\%), the second node is deemed to have done 5 / 17.5 percent (29\%), and the block producer is deemed to have done 2.5 / 17.5 percent (14\%) of the routing work for that transaction. If a transaction is included without a routing path, the originator is assigned all of the work for that transaction.}

In the event that the block reward is seriously in excess of a smoothed average maintained by consensus (current target 1.25), the payment for both miner and router is reduced proportionally and the excess portion is burned for good. This induces deflation in the event of attacks on the lottery mechanism and ensures there are no theoretical situations in which attackers can recapture more money from the payments lottery than they are forced to contribute in attacking the network.

In "Classic Saito" mining difficulty auto-adjusts until the network produces one golden ticket on average per block. The network is secure at the cost of deflation from unsolved blocks.


## 4. IMPROVING SAITO

We can increase cost-of-attack and minimize deflation by inclusion of a staking mechanism. Users can deposit UTXO into a staking table in exchange for a share of the block reward. This payment counterbalances the ATR penalty assigned to rebroadcast transactions, and enables a long-term way to keep store-of-value on the chain. Staked UTXO are locked and unspendable until they are paid out, at which point they will automatically persist in the staking tables in a spendable (withdrawable) state. After several years UTXO may be auto-ejected and require manual re-staking.

The payment mechanism is modified as follows. Once a golden ticket is included in block N+1, the payment to the miner and router for the preceding block N is unmodified. If block N did not contain a golden ticket, the random variable used to select the winning routing node from block N is hashed again. This is used to pick a winning entrant from the set of unpaid UTXO maintained in the table of stakers. The random variable is then hashed again to pick a winning routing node for block N-1 in the same process as above. This process can be repeated for all previously unpaid blocks, although an upper limit to backwards recusion may be applied for practical purposes, beyond which point any uncollected funds are simply burned.

Some minor modifications are useful. When all stakers have been paid out, the staking table is recalculated and the amount paid to staking UTXO should be re-calculated as the average of the amount paid into the treasury by the staking reward during the *previous* genesis period, normalized to the percentage of the staking table represented by each UTXO. The percentage of the block reward that would be paid to stakers is thus put into the staking treasury, and the payments come from that treasury and are smoothed over time. A longer smoothing period may be used if desired. This smoothing function should also permit tokens to be burned in the event of a gross disparity between the current and historical average. Limits may be put on the size of the staking pool to induce competition between stakers if desirable, although we prefer to keep the table completely open.

In order to make staking work with ATR, block producers who rebroadcast staked-UTXOs must indicate in their ATR transactions whether the outputs are in the current or pending pool. We recommend that a hash representation of the state of the staking table is included in every block in the form of a commitment, but this is not strictly necessary as it is theoretically possible to reconstruct the state of the staking pool within one genesis period at most.

A target difficulty is selected which represents the ideal number of staker-to-miner payouts. We are starting with 1 golden ticket every 2 blocks on average. At this rate, mining difficulty is adjusted upwards if two blocks containing golden tickets are found in a row and downwards if two blocks without golden tickets are found in a row.


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




