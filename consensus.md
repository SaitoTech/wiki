---
title: Saito Consensus Mechanism
description: Consensus Mechanism
published: true
date: 2026-09-27T04:42:43.929Z
tags: 
editor: markdown
dateCreated: 2022-02-17T10:09:00.217Z
---

# Saito Consensus

Readers with backgrounds in economics, distributed systems, and mechanism design are encouraged to visit our [theory section](/consensus/theory). This page offers an ELI5 overview of Saito Consensus for general readers.

The short version? Saito separates **who gets to build a block** from **who gets paid for that block.** What is one competition in Bitcoin and Ethereum is two different competitions Saito decides in two different ways.


## Overview: Sending a Transaction

1. When users send transactions into the network, they attach cryptographic signature naming the peer (or peers) to which they are forwarding their transactions -- their **first hops**.
2. Peers that receive these transactions can forward them to *their* peers, adding their own signatures in the process -- their **second hops**. This process repeats as each hop gets recorded, permanently and unforgeably, in the versions of these transaction spreading across the network.
3. Nodes which collect enough of these fee-paying transactions can earn the right to produce the next block in a repeating falling-price or "Dutch Clock" auction. This auction picks the most efficient collector-of-fees each round as the block producer.
4. Once a block is produced, every fee in it is **burned**. No-one is paid, but a second competition begins which may *resurrect* the burned fees and distribute them to both the miners who secure the payouts and the routing peers who collect the money that powers it.

Everything below is a closer look at steps 3–4.


## A Closer Look at Block Production

The consensus algorithm dictates how many units of "routing work" must be contained in a block for it to be valid under consensus rules. This figure starts very high immediately after a block is produced, and slowly decreases until 

How much "work" a block contains depends on the transaction fees in it, and how many hops each has taken to reach that node. At the **first hop**, the node gets an amount of work equal to the fee paid. But as a transaction moves through the network, this amount **halves at every hop** beyond the first. A transaction with a 10 SAITO fee is worth:

- 10 units to the 1st-hop node
- 5 units to the 2nd-hop node
- 2.5 units to the 3rd-hop node
- ...and so on

Once a block is produced, all of the fees in the block are burned. No-one is paid. The auction to produce the next block restarts and the countdown begins until the next block is produced by another node contributing fee-flow to the network.

**Overview**: Saito nodes burn money to produce blocks -- proving they did the socially useful work of gathering and relaying real payments. Burning all of the fees makes this step expensive for nodes that try to attack the system, and ensures that attackers always lose money to attack the network. This cost-of-attack property is what the golden ticket lottery protects, even as it brings the fees back into circulation.

## The Golden Ticket: issuing payouts

Once a block is produced, a hashing competition begins where miners compete to find a **golden ticket**. If that ticket is included in the very next block, the winning miner collects 50% of the fees from that previous block, and a random routing node is picked from one of its transactions to win the remaining 50% as a routing payout.

What makes Saito secure is how the winning routing node is chosen.

The winning transaction is chosen based on its share of fees-in-block. If a block has 100 SAITO in fees and one transaction contributes 10 SAITO in fees, that transaction has a 10% chance of winning the payout lottery. 

Once a transaction is chosen, the lottery picks a node from its routing path. The block producer is eligible for payout as the deepest hop in this routing path, but every other node is eligible too. And the payout lottery is biased towards early-hop nodes. Chances of winning on a three-hop routing path are:

- 57% chance to the 1st-hop node -- 10 / 17.5
- 28.5% chance to the 2nd-hop node -- 5 / 17.5
- 14.5% chance to the 3rd-hop node -- 2.5 / 17.5

The lottery is rigged against the block producer, creating a game that is profitable to play with other people's money, but that is expensive to play if you have to contribute your own money. 

Like playing in a rigged Casino, adding your own fees to a block is always a net loss. Making a block with your own wallet always burns half of your fees. Adding fees from other people helps reduce that cost, but gives those routing nodes a greater claim on your own wallet than you get from theirs.

This elegant lottery is why Saito doesn't inherit 51%-attack economics. In Bitcoin, hash buys you the ability to orphan blocks for free. In Ethereum, stakers can collude to orphan blocks. With Saito, 

## 4. Automatic Transaction Rebroadcasting (ATR): permanent storage that pays for itself

The blockchain is divided into fixed-length epochs. When a block ages out of the current epoch, its unspent outputs (UTXO) would normally become unspendable — unless the owner keeps paying to rebroadcast them.

- The rebroadcast fee must meet or exceed the network's average fee-per-byte over the previous epoch.
- Rebroadcasting can also come with a staking payout, funded by the fee itself.

Two consequences fall out of this:

- **It raises the cost of attacking the network**, because it continuously pulls fees away from anyone trying to spend their way into control of block production.
- **It makes permanent on-chain storage economically self-sustaining.** Anyone who wants data stored forever just needs to attach a large enough balance that the rebroadcast payout keeps covering its own rent, indefinitely, with no ongoing action required from the owner.

---

## In short

| Question | Bitcoin / Ethereum | Saito |
|---|---|---|
| Who builds blocks? | Whoever wins the mining/staking race | Whoever burns the most tokens |
| Who gets paid? | The same party, immediately | A *separate* hash-race winner, split with a randomly chosen relayer — decided one block later, or not at all |
| What secures the network? | Cost of acquiring mining/staking power | Cost of recovering your own money, if you try to attack by creating fake transactions |
| What happens to fees if no one "wins"? | N/A | Burned permanently |

For implementation details and specific security mitigations, see the [implementation notes](https://wiki.saito.io/consensus/implementation-notes).

