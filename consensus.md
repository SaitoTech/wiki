---
title: Saito Consensus Mechanism
description: Consensus Mechanism
published: true
date: 2026-09-27T05:38:10.179Z
tags: 
editor: markdown
dateCreated: 2022-02-17T10:09:00.217Z
---

# Saito Consensus

Readers with backgrounds in economics, distributed systems, and mechanism design are encouraged to visit our [theory section](/consensus/theory). This page offers an ELI5 of Saito Consensus for general readers.


## A Quick Overview of Routing Work Mechanisms

Adding routing signatures to transactions lets Saito separate **who builds blocks** from **who gets paid for blocks.** To see how this works, consider the case of a user sending a transaction into the network:

1. When users send transactions into the network, they attach cryptographic signatures to these transactions specifying the peer to which they are forwarding their transactions -- this is the **first hop** peer.
2. Peers that receive these transactions can forward them to *their* peers, adding their own signatures in the process -- their recipients are the **second hop** peers. This process repeats hop-by-hop as these transactions spread across the network.
3. Nodes which collect enough fee-paying transactions can produce a block by proposing one in an ever-repeating falling-price or "Dutch Clock" auction. This auction picks the most efficient fee-collector each round as the block producer.
4. No-one is paid when a block is produced: every fee in the block is **burned**. But a second competition begins which may *resurrect* these burned fees and distribute them to both the miners that run the payout lottery and the routing nodes that produce the blocks.

The result of this process is that the longest-chain consists of blocks proposed by the most efficient burners-of-fees. Saito is designed so that overcoming this disadvantage forces attackers to burn their own money. Details on how this works requires a closer look at steps 3–4.


## Routing Work and Block Production

The consensus algorithm dictates how many units of "routing work" a block must contain to be considered valid by the other nodes in the network. Because Saito implements a "Dutch Clock" auction, this figure starts high immediately after a block is produced and falls over time. This means waiting can sometimes be a profitable strategy!

But how much "routing work" does a block contain? That figure depends on the total amount of transaction fees it is offering to burn, and how many hops each transaction has taken to reach that node. At the **first hop**, the node gets an amount of work equal to the fee paid. But as a transaction moves through the network, this amount **halves at every hop** beyond the first. A transaction with a 10 SAITO fee is worth:

- 10 units to the 1st-hop node
- 5 units to the 2nd-hop node
- 2.5 units to the 3rd-hop node
- ...and so on

The most efficient block producer is the one at the strategic position in the network where incoming fees combine to push them over the threshold. And if no-one receives such a transaction, the price of producing a block falls until one of the nodes with existing transaction flow is eligible to produce a block. Eventually, the "richest" node will produce a block.

At that point, a block is produced and all of the fees in that block are burned. No-one is paid. The auction to produce the next block resets and the countdown to produce the block begins as more transactions flow into the network and the competition to produce blocks continues.

**Overview**: Saito nodes burn money to produce blocks -- proving they did the socially useful work of gathering and relaying real payments. The fact that the network burns all fees makes producing blocks expensive and ensures that attackers always lose money. Protecting this property -- keeping it expensive to attack once fees are paid out to network nodes -- is the critical solution Saito introduces.

## The Golden Ticket and Routing Payouts

Once a block is produced, a hashing competition begins where miners compete to find a **golden ticket** in a process similar to Bitcoin mining. If such a ticket is included in the very next block, the winning miner is paid 50% of the fees from that previous block while a routing node is randomly picked to win the rest as a routing payout.

What makes Saito secure is how this routing node is chosen.

First a winning transaction is chosen based on its share of fees-in-block. If a block has 100 SAITO in fees and one transaction contributes 10 SAITO in fees, that transaction has a 10% chance of winning the payout lottery.

Once a winning transaction is chosen, the lottery picks a node from its routing path. But this payout is biased against block producers -- who are always the deepest nodes in the routing paths. The same routing paths that are used to protect block production are examined to protect the payoffs. The chance of any node winning in a three-hop routing path are:

- ~57% chance to the 1st-hop node -- 10 / 17.5
- ~28.5% chance to the 2nd-hop node -- 5 / 17.5
- ~14.5% chance to the 3rd-hop node -- 2.5 / 17.5

Like playing in a rigged Casino, this creates a game that is expensive to play with your own money but profitable to play with other people's fees. Making a block with your own funds always burns half of your fees. Adding fees from other people helps reduce that cost, but pulls more money away from you in the routing payout than it contributes in routing work.

This elegant lottery is why Saito doesn't inherit 51%-attack economics. Nodes maximize profitability by taking turns to propose blocks, not by orphaning competitor blocks and struggling to replace them with blocks that require the attacker to burn their own money, or accept lower payouts than they could get simply by waiting their turn.

## Automatic Transaction Rebroadcasting (ATR)

One of the benefits of Saito paying routing nodes is that the servers that bear the real cost of running the network are the ones that are paid, not validators or miners who can shirk those responsibilities to maximize their profitability. This makes Saito more suitable for big-data applications. But how can we prevent the blockchain from growing out-of-control as a result?

Saito Consensus solves this with an elegant data-pruning mechanism known as Automatic Transaction Rebroadcasting (ATR). This mechanism divides the blockchain into fixed-length epochs. When a block ages out of the current epoch, its unspent outputs (UTXO) become unspendable but are moved **automatically** into the latest block by the block producer. Any block that does not include these transactions is considered invalid by consensus rules.

ATR takes also allows the following:

- rebroadcast UTXO can be charged a fee
- rebroadcast UTXO can be given a payout

This has two immediate consequences:

- **ATR raises the cost of attacking the network** by pulling a portion of the block reward away from attackers and distributing them to the users in the network, and particularly any users who cannot spend their tokens because the network is censored or under attack.

- **ATR makes permanent on-chain storage economically self-sustaining.** Anyone who wants data stored forever simply needs to attach a large enough balance that the rebroadcast payout keeps covering its own rent in perpetuity.

---

## Summary

| Question | Bitcoin | Ethereum | Saito |
|---|---|---|---|
| who proposes blocks? | miners | stakers | anyone |
| who gets paid? | miners | stakers | miners & routers |
| permissionless? | yes | no | yes |
| 51% attack? | exists | exists | none |
| sybil attack? | exists | exists | none |
| incentive compatible? | no | no | yes |

For implementation details and specific security mitigations, see the [implementation notes](https://wiki.saito.io/consensus/implementation-notes).

