---
title: A Simple Proof of Sybil Proof
description: 
published: true
date: 2024-11-30T08:34:43.547Z
tags: 
editor: markdown
dateCreated: 2024-11-30T08:34:43.547Z
---

# A Simple Proof of Sybil Proof

![sybil-proof.webp](/blog/sybil-proof.webp)

*Written by David Lancashire on February 16, 2023*

Saito Consensus is a sybil-proof layer-one blockchain. The technical proof is contained in our paper on [cost of attack](https://saito.io), but as that has reasonably advanced mathematics and the implications are not obvious without commentary, this blog post offers a simpler explanation for readers seeking an intuitive understanding of Saito’s sybil-proof properties.

We start with two straightforward claims:

> **Proposition #1**  
> Nodes that use public routing work to produce blocks are disincentivized from delaying the production of those blocks, as that strictly reduces expected income.
>
> **Proposition #2**  
> All participants are incentivized to share transactions publicly to induce direct competition between peers under proposition #1 and thereby secure the fastest confirmations for the lowest fee.

These claims can be formally proven but should be self-evident to anyone familiar with [Saito Consensus](https://saito.io). Under them, adding unnecessary routing hops to transactions is a strictly inferior strategy unless attackers compensate for the fall in the final-hop value of their transactions by adding their own fee-bearing transactions.

## On The Irrationality of Self-Generated Routing Work

All sybil-attacks necessarily involve transactions where the attacker does not occupy the first-hop in the transaction path. This is trivially true: attackers cannot increase their payout by adding hops to transactions where they already have 100% of the claims on payout.

The irrationality of sybilling second-hop transactions can be proven by examining what happens when an attacker sybils a block with only one transaction, such as the following block produced by NODE B that contains 50 units of final-hop routing work.

| Transaction | Fee | Router | Hop | Routing Work |
|-------------|-----|--------|-----|--------------|
| 1           | 100 | Node A | 1   | 100          |
|             |     | Node B | 2   | 50           |

With 100 SAITO in total fees and fifty-percent of those burned in the costly lottery, only 50 SAITO are available for the routing payout in this block. As transaction #1 is the only transaction that exists it has a 100% chance of selection in the payment lottery and NODE A has 2/3 and NODE B has 1/3 of the expected routing payout. We can easily calculate their expected income as 33.3 SAITO and 16.6 SAITO respectively.

The sybil attack we are concerned with involves NODE B adding an additional hop (“self-cloning”) to transaction #1 to increase its share of that transaction’s overall routing payout, while simultaneously creating the smallest fee-paying transaction needed to keep its final-hop routing work constant at 50 SAITO as per proposition #1.

This gives us the following attack block:

| Transaction | Fee | Router | Hop | Routing Work |
|-------------|-----|--------|-----|--------------|
| 1           | 100 | Node A | 1   | 100          |
|             |     | Node B | 2   | 50           |
|             |     | Node B | 3   | 25           |
| 2           | 25  | Node B | 1   | 25           |

With 125 SAITO in total fees there are now 62.5 SAITO available for the routing payout. Our golden ticket mechanism will select the first transaction with (100 / 125) probability and the second with (25 / 125) probability. NODE A has (100 / 175) chance of winning if the first transaction is selected and (0 / 25) if the second transaction is selected. NODE B has (75 / 175) chance of winning if the first transaction is selected and (25 / 25) if the second transaction is selected. NODE B must finally deduct the 25 SAITO it has contributed to the block (that it spent to sybil) from its profits. Its expected income is now:

- NODE A = 62.5 * ((100 / 175) * 0.8) + (62.5 * ((0 / 25) * 0.2)) = 28.57 SAITO
- NODE B = 62.5 * ((75 / 175) * 0.8) + (62.5 * ((25 / 25) * 0.2)) – 25 = 8.92 SAITO

The attacker has decreased their expected income from 16.6 SAITO to 8.92 SAITO. It is easy to demonstrate that losses accelerate as the attacker adds more routing hops to transaction #1.

## An Intuitive Understanding of Sybil-Proofing

Something fascinating happens when an attacker sybils a routing-work blockchain. Whereas all the fees in the block were previously potential income to the attacker, the lottery is now taxing their wallet directly.

For a routing work mechanism to be sybil-proof, it is sufficient to show that the tax on self-generated routing-work is greater than the total income a node 1-hop deeper in the network can expect from an equivalent amount of final-hop routing work. In the Saito Classic mechanism the tax is 50% of all fees put into the block, and first-hop nodes earn at minimum 50% of routing payout. Since any additional fees in the block by definition come from the attacker, it is theoretically impossible to generate positive expected income.

As long as the lottery tax remains provably costly regardless of the amount of routing work that the attacker has in the block, any network that has the same work-decay and payout-decay functions as Saito Classic by definition inherits the same sybil-proof properties. In practice, our goal is to force cost-of-attack significantly above 100% of fee-throughput, so that in a best-case scenario the attacker is hemorrhaging money rather than merely breaking even.

This requires the introduction of a staking payout and the increase in cost-of-attack that can come from the added difficulty of finding combinatorial lottery solutions that simultaneously issue the routing payments from multiple blocks to the attacker. In the paper referenced above, we show very clearly that cost-of-attack is a minimum of 137 percent in a network with such a structure. This means an attacker must spend ~137% of network fee-throughput to earn 100% of the fees in that block which do not come from their own wallet. With full control of the staking table, the attacker can eke out profits at approximately 75% control of the staking table. This can easily be addressed in the paper as mentioned – by the imposition of an income cap that limits payouts to 125% of a smoothed average. Under these situations cost-of-attack rises much higher than 137% to start, and remains above 100% even if attackers gain full control of the staking payout.
