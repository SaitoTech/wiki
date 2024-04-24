---
title: majoritarian-attacks
description: 
published: true
date: 2024-04-24T23:05:11.998Z
tags: 
editor: markdown
dateCreated: 2023-09-20T01:58:02.086Z
---

# Eliminating 51% Attacks

- Consult the [whitepaper](https://saito.io/saito-whitepaper.pdf) to learn the basics.

- For a complete mathematical proof [see here](https://wiki.saito.io/consensus/math).

- Official Blog [post](https://saito.tech/eliminating-51-attacks-in-proof-of-work-blockchains/) on the same subject.

### Consensus

Blockchain consensus protocols can be considered objective competitions which determines what additions may be considered valid and canonical. By all participants recognizing a single consensus protocol, a distributed network can reach full consensus with (PoS) or without (PoW, Saito) total coordination (each node is not required data from every other node).

## Majority Assumptions

### Proof of Work

Consensus design for distributed ledgers has evolved since Bitcoin, which uses a longest-chain-rule and threshold of hash-based work within blocks to determine the priorities between competing blocks during disputes. Despite many technical advancements atop the Bitcoin model, every consensus protocol, except for Saito's, falls prey to *Majoritarian Attack*, commonly referred to as the 51% Attack. 

While blockchain has provable and objective cost-of-attack when the majority of consensus power can be assumed held by honest and competing participants, the economic security unique to blockchain breaks down completely when a majority of power is held by one party or coalition. This majority coalition of 51% or more holds the power to censor all other blocks made by the 49% minority, because they can always build a longer chain.

The biggest issue with 51% attacks is the fact that they are economically sustainable - this is contrary to naive popular belief, which states that a 51% has a cost per unit of time, but no profit. Because attackers can produce a longer chain of all their own blocks, they can earn all rewards. All without increasing their work production (cost), attackers have the incentive and the means to *continue* the attack *indefinitely*.

[Discouragement Attacks](https://saito.tech/on-discouragement-attacks/) can make tolerating losses more amenable to attackers as they can force all honest participants to share those losses and effectively 'buy out'  honest shares of consensus power by marginalizing their profits until they are forced to drop out.

### Proof of Stake

Advanced Proof of Stake systems like Ethereum may not map onto the PoW metaphor as simply, but these systems are themselves not immune to majority assumptions and the relevant attack vectors from 51% or even 33% colusion of consensus power. Ethereum ultimately resorts to handling such attackers through *[Social Consensus](https://ethereum.org/en/developers/docs/consensus-mechanisms/pos/attack-and-defense/#people-the-last-line-of-defense)* i.e. a user-initiated and approved fork.

Because Proof of Stake systems introduce closure to maintain what security they can offer, their consensus model is fundamentally different than that of Proof of Work or Saito, which both allow anyone to participate in consensus without first interacting with the chain. Proof of Stake is essentially a traditional distributed system which requires the staking of a token to contribute towards, and punishes the subset of misbehaviors it can detect by slashing those staked tokens.

While the principles of a 51% attack described on this page are fundamentally shared in any Proof of Stake system, it is also important to recognize that Saito solves the problem all while making less compromises on openness than Proof of Stake is required to.

Proof of Stake is more complicated, but not fundamentally more secure. This document describes the problem and its solution on the simpler, Nakamoto model, which has the same downstream implications towards PoS.

## How a 51% Attack Works

Fundamentally, 51% attacks work because the majority holder of consensus power can always build a longer valid chain than the remaining 49% of network participants can muster. Since the open and objective measure which the network agrees upon to accept new blocks is the longest chain or similar measure, a slight majority, on average, can always censor the rest of the network and still make a longer chain of work.

In an extreme scenario, the attacker could choose to never let the other half of the network produce a block on the longest chain ever again. This means that the attacker may produce 100% of blocks and earn all the rewards at only 51% the cost. There are many other possible specific attacks, like address censorship, consensus delay and double-spends, but the key ability behind all of it comes from the ability of the majority attacker to overwrite and censor the blocks, and the work, performed by the honest network.

In practice, the 49% of the network, who cannot always detect such an attack, is still burning almost half the resources to perform the security function of the network, but because they must always commit this security function to their last-known perspective on the longest fork, and the attacker can always create a longer one; the honest network constantly has the rug pulled out from under them.

This Losing one's work to a longer fork is for that work to be 'orphaned' (technical term). Work-orphaning will happen under honest network conditions too, as two or more honest block producers will sometimes produce blocks intended for the same slot, and only one can occupy it. Every time the attacker creates a longer fork which competes with the honest minority network, the minority has their work 'orphaned,' and must start over again.

Since work is not cumulative, the majority, on average, always wins - on a long enough timescale the majority always has the longest chain of valid work and the rewards that go with it.

## How Saito Eliminates 51% Attacks - Cumulative, Block Agnostic Work

### Routing Work

The objective measure of work required for Saito block production is special in many ways, but the most relevant for eliminating the 51% attack is that work in Saito is *Block Agnostic -* that is, nodes are not forced to commit their work to a specific block or point in the chain's history.

Whereas in other blockchains, consensus nodes must commit to the longest-known fork, consensus nodes in Saito can produce work and earn rewards *without even knowing* what the full blockchain looks like. This is achieved thanks to the fact that *routing work* (required for block production) is committed within individual transactions, not blocks.

In Saito, transactions are signed by senders such that the right to its claim rewards belong to the node it was sent to - nodes can further relay like this to share the rewards and increase the chance of the transction entering the next block. The more 'routing signatures' a transaction has, the less block work it can contribute. Relevant to 51% attacks, the important aspect of this system is that the source of valid block work, transaction fees, *do not require a commitment to any particular fork.*

- See [this](https://wiki.saito.io/en/consensus) article or the [whitepaper](https://saito.io/saito-whitepaper.pdf) for a complete description of routing work.

### Golden Ticket

While routing-signatures earn nodes the right to rewards, there is one more important step to *unlocking* those rewards for distribution: the Golden Ticket. This is a mining puzzle which takes place *after* a valid block is published, and is used to unlock its rewards.

This is a crucial component, as it makes it costly to use spoofed transaction fees to produce blocks for free - instead, the money is locked up and the cost to unlock it makes the attack unprofitable. If instead genuine users are paying fees, that cost to unlock is part of what they pay for security; the attacker trying to run his fees in circles gets no utility from such security, as they are sending money to themselves.

### Comparing Saito to PoW

In Bitcoin, a node with 51% of hashpower produces a block and forces the entire network to start over on that new most recent block; it does not matter if the honest network sometimes finds a block first, because the attacker can always wait until their solo-mined-chain is longer. All work from the honest network is censored.

In Saito, a node with 51% of the current transaction fees must use those fees to produce a block, but the other 49% of transaction fees which were not involved do not suddenly lose their value, and can still be used to make valid blocks. This means any minority of work which remains unincluded in a block remains valuable to consensus nodes, and their ability to contribute to blocks cannot be censored by a malicious majority.

Even if a malicious majority can create a longer chain and censor block production from the honest network for some time, their longest chain has no ability to censor the transactions which an honest minority is building up while the attacker censors them. Honest nodes can always include their work at the end of the attacker's fork, meaning that whatever share of work they accumulate is equal to the share of blocks they can create - this is not possible when a 51% attack exists.

During an attempted attack, consensus nodes who were not allowed to make blocks accumulate work the longer they are censored, and the attacker quickly loses their work as they consume it to produce consecutive blocks, while the rest of the network's store of work grows and grows - both forces serving to reduce the length of the attack.

If an attacker in Saito wants to produce consecutive blocks, they must use up their transaction fees in place of the honest network's fees. Since producing new blocks does not remove the valid work derived from the transaction fees of all other consensus nodes, honest nodes can maintain their *accumulation* of work, which cannot be eliminated just because a new block is made - this preservation of work which is independent of blocks is not possible in PoW or PoS, and is the missing piece to eliminating 51% attacks in any consensus protocol.

Since the amount of work the honest network accumulates can only grow the longer they are censored, the amount of work the attacker must produce to keep censoring them also grows without bound, no matter if the attacker has 51% of inbound fees or 99%.

Even if the attacker owns 100% of inbound fees, as soon as they begin abusing users, new routing nodes are free to enter the network and begin taking market share and interrupting the majority fork.  The ability for recovery from 100% attacks is not possible in any other blockchain.


---


- We invite researchers and auditors to consult a more rigorous [mathematical proof](/consensus/math) of Saito's elimination of the 51% attack.

