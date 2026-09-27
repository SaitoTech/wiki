---
title: Saito Consensus Mechanism
description: Consensus Mechanism
published: true
date: 2026-09-27T03:47:02.346Z
tags: 
editor: markdown
dateCreated: 2022-02-17T10:09:00.217Z
---

# Saito Consensus

Readers with backgrounds in economics, distributed systems, and mechanism design are encouraged to visit our [theory section](/consensus/theory). This page offers an overview of the protocol for general readers.

The short version? Saito separates **"who gets to build a block"** from **"who gets paid its fees."** This is the same competition in Bitcoin and Ethereum. In Saito, they're two different competitions, decided in two different ways, a block apart.


---

## The journey of one transaction

1. You send a transaction. You attach a cryptographic signature naming the peer (or peers) you're sending it to — its **first hop**.
2. That peer can relay it onward to *their* peers, adding their own signature. Each hop the transaction takes gets recorded, permanently and unforgeably, in the transaction itself.
3. Nodes compete to gather up enough of these fee-paying transactions to earn the right to produce the next block.
4. Once a block is produced, every fee in it is **burned** — destroyed. Nobody has been paid yet.
5. A separate, open competition now begins to *resurrect* those burned fees and hand them out. Whoever wins that competition splits the reward with one of the people who relayed the winning transaction.
6. If nobody wins that competition in time, the fees stay burned forever.

Everything below is a closer look at steps 3–6.


---

## 1. Routing work: how blocks get built

When a transaction moves through the network, its fee doesn't stay whole — it **halves at every hop** beyond the first. A transaction with a 10 SAITO fee is worth:

- 10 units to the 1st-hop node
- 5 units to the 2nd-hop node
- 2.5 units to the 3rd-hop node
- ...and so on

This declining value is called **routing work**, and it does two separate jobs that are worth keeping distinct in your head, because Saito borrows PoW's vocabulary while changing what it means:

- **Job 1 — earning the right to build a block.** Nodes accumulate routing work by collecting fee-paying transactions, and use it to meet a network-wide difficulty threshold (the **burn fee**) that adjusts up or down to keep blocks arriving at a steady pace. This is the "proof-of-work"-*flavored* part of Saito, but no hashing is involved here — it's proof that you did the socially useful work of gathering and relaying real transactions.
- **Job 2 — determining who gets paid later.** The same fee-halving numbers are reused, later, to weight a lottery that decides who among the block's relayers gets paid (see below). It's the *same arithmetic*, applied to a *different question*, at a *different time*. If you remember one thing from this page, remember that "routing work" means two different things depending on which job it's doing.


## 2. The golden ticket: how nodes get paid

Producing a block burns every fee inside it. Getting paid is a second, independent race.

Once a block is produced, a hashing competition begins — mechanically, this part *is* like Bitcoin mining: find a hash below a target. Whoever finds a valid solution — a **golden ticket** — first gets to trigger a payout, *if* they submit it in the very next block. Miss that one-block window, and the fees in question are gone. Permanently.

A few things about this competition that surprise people coming from Bitcoin or Ethereum:

- **Anyone can compete for a golden ticket**, whether or not they relayed a single transaction. It's an open hashing race, separate from the routing side of the network.
- **The payout is split**, not winner-take-all: half goes to whoever found the golden ticket, half goes to a routing node **randomly selected from the block's transactions**, weighted by each hop's share of routing work (Job 2, above). A node that did the original block-producer's work is eligible to win this lottery too — but only as one competitor among many, on the same odds as everyone else who relayed something.
- **Difficulty adjusts fast**: it rises if two blocks in a row produce a golden ticket, and falls if two blocks in a row don't.
- **Miners can choose which solution to submit, if they find more than one** — and this is a *stabilizing* feature, not a loophole. If difficulty drifts below its natural equilibrium, miners can select solutions that pay them, which is *more* profitable when difficulty is low — pulling difficulty back up while they profit. Someone who tried to deliberately suppress solutions to force difficulty down wouldn't gain an edge over anyone else: a lower difficulty makes mining easier for *every* miner equally, including whoever is trying to game it, so the attempt just hands out cheaper, more profitable mining to the whole network at the schemer's own expense.

This is why Saito doesn't inherit Bitcoin's classic 51%-attack economics. In Bitcoin, hash power buys you the ability to rewrite history and double-spend, because block production *is* the reward-winning race. In Saito, block production and the golden-ticket race are two separate competitions — controlling a large share of one doesn't hand you leverage over the other, and there's no reward for rewriting a past block, because the fees at stake were never paid to begin with unless a golden ticket claimed them in time.

## 3. Deflation, by design

Every block's fees are burned. Most of the time, some of them come back — through the golden-ticket lottery — but not all, and not always. Blocks that never produce a golden ticket in time lose those fees forever. This creates ongoing deflationary pressure, and it's intentional: it's what makes attacking the network expensive without needing a fixed, inflation-funded reward like Bitcoin's block subsidy.

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
| Who builds the next block? | Whoever wins the mining/staking race | Whoever gathers the most fee-weighted routing work |
| Who gets paid for it? | The same party, immediately | A *separate* hash-race winner, split with a randomly chosen relayer — decided one block later, or not at all |
| What secures the network? | Cost of acquiring mining/staking power | Cost of acquiring both routing reach *and* hash power, for two unrelated competitions |
| What happens to fees if no one "wins"? | N/A — reward is fixed regardless | Burned permanently |

For implementation details and specific security mitigations, see the [implementation notes](https://wiki.saito.io/consensus/implementation-notes).

