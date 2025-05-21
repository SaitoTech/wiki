---
title: majoritarian-attacks
description: 
published: true
date: 2025-05-21T11:04:57.244Z
tags: 
editor: markdown
dateCreated: 2023-09-20T01:58:02.086Z
---

# Eliminating 51% Attacks

- Consult the [whitepaper](https://saito.io/saito-whitepaper.pdf) to learn the basics.

- For a complete mathematical proof [see here](https://wiki.saito.io/consensus/math).

- Official Blog [post](https://saito.tech/eliminating-51-attacks-in-proof-of-work-blockchains/) on the same subject.


## Impossibility Proofs

The most common reason people consider the 51% attack impossible to solve is that well-known academic papers on the limits of distributed consensus claim this is the case. The fastest way to see how Saito Consensus avoids these problems is noticing the way it breaks the axiomatic assumptions of these results.

### 1. Bracha and Toueg (1985)

The paper *Asynchronous Consensus and Broadcast Protocols* by Bracha and Toueg (1985) is the most widely-cited proof that probabilistic protocols with **n** total participants can tolerate at most **(n-1)/2** malicious participants.

Bracha and Toueg conceptualize consensus mechanisms as consisting of *processes* which can be programmed to behave honestly or maliciously. The foundation of their claim is that in permissionless mechanisms byzantine processes can do anything honest processes can do. If malicious nodes wish to prevent the network from achieving consensus, they need merely to propose the same number of "atomic steps" as the honest minority is proposing, stalemating consensus by preventing it from resolving on any particular outcome.

> In an atomic step of the system, a process can try to receive a message, perform an arbitrarily long local computation, and then send a finite set of messages. The computation and the messages sent are prescribed by the protocol, that is, a function of the message received and the local state.

The problem with Bracha and Toueg is that their model of the network consists of *processes*, which leads them into assuming that all nodes can perform the same actions for the same cost at all times. Missing from their view of the network is the need for resource expenditure in taking an atomic step. They assume malicious nodes can simulate the behavior of honest nodes without penalty. And they assume there is no economic or cryptographic mechanism to penalize processes sharing a malicious message over an honest one. 

This assumption -- symmetrically costless participation -- was reasonable in the 1980s when consensus mechanisms did not manage economic assets and could not force nodes to burn tokens for proposing malicious state transitions.  It remained reasonable in the face of proof-of-work and proof-of-stake mechanisms because those mechanisms cannot impose penalities on malicious majorities. The assumption collapses in the face of Saito Consensus, because routing work charges nodes more to propose economically-inefficient state transitions, and attackers are forced to propose economically-inefficient transitions in order to orphan honest blocks.

As a result, the assumption Bracha and Toueg make that all *processes* face the same cost structure does not apply to Saito Consensus. Honest nodes run the network using other people's money. Their costs of producing blocks are lower than those of attackers, and because they never include their own fees in blocks they never need reduce their share of the overall network. But attackers necessarily force themselves out majority control of network resources if they continue to orphan honest blocks. The network is capable of reducing 


### 2. Dwork, Lynch, and Stockmeyer (1988)

A second but related series of impossibility results come from *Consensus in the presence of Partial Synchrony* by Dwork, Lynch, and Stockmeyer (1988). These authors note that when a system is partitioned in ways where block production resources are distributed in an equally balanced fashion, deterministic consensus can't be achieved.

The first problem with this approach is its assumption that block production capacity can be split evenly — but in routing work systems, this would require total control over how ever participant in the network creates transactions and sends messages. Such coordination is at minimum incompatible with informational decentralization. Nor is it reasonably to assert control of 100% of network participants in order to pull off an attack that claims control over a mere majority.

To avoid this problem we can imagine a situation where an attacker privately controls 50% of pre-attack fee-flow and is merely moving their own resources to a private chain. In this case the attacker only controls the 50% of the resources needed to produce blocks and their attack is essentially denying those fees to the honest chain and spending them on a private fork. Does this attack compromise Saito Consensus?

Fortunately not, for while it is theoretically possible for an attacker who controls exactly 50% of first-hop fee-flow to move their fee-flow to a private network, doing so is economically irrational in Saito Consensus. For the attacker, who was previously spending 50% of their own fees on producing golden tickets to unlocking routing payouts, is now spending 100% of their  fees-in-block to do the same. Even if an attacker could pull off such an attack they would not increase their revenue but merely raise their cost of getting paid.

The consensus mechanism continues to work exactly as promised -- imposing a quantifiable cost-of-attack on nodes which engage in the byzantine behavior of censoring honest transactions or orphaning honest blocks from the collective chain.





The 

can 
Consensus in the presence of partial synchrony


Proof of Work

There are two Consensus design for distributed ledgers has evolved since Bitcoin, which uses a longest-chain-rule and threshold of hash-based work within blocks to resolve competing forks during chain-splits. Despite many technical advancements atop the Bitcoin model, every consensus protocol, except for Saito's, falls prey to *Majoritarian Attack*, commonly referred to as the 51% Attack. 

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

In Bitcoin, a node with 51% of hashpower produces a block and forces the entire network to start over on that new most recent block; it does not matter if the honest network sometimes finds a block first, because the attacking majority can always wait until their solo-mined-chain is longer. Work and rewards of the honest network is censored.

In Saito, a node with 51% of the current transaction fees must use those fees to produce a block, but the other 49% of transaction fees which were not involved do not suddenly lose their value, and can still be used to make valid blocks. This means any minority of work which remains unincluded in a block remains valuable to consensus nodes, and their ability to contribute to blocks cannot be censored by a malicious majority.

Even if a malicious majority can create a longer chain and censor block production from the honest network for some time, their longest chain has no ability to censor the transactions which an honest minority is building up while the attacker censors them. Honest nodes can always include their valid work of any age at the end of the attacker's fork - this is not possible in PoW or PoS.

During an attempted attack, consensus nodes who were not allowed to make blocks accumulate work the longer they are censored, and the attacker quickly loses their work as they consume it to produce consecutive blocks, while the rest of the network's store of work grows and grows - both forces serving to reduce the length of the attack.

If an attacker in Saito wants to keep producing consecutive blocks after the censored minority has caught-up, they must begin supplementing their attack by paying for fees out-of-pcket and paying the miners. This dedicated attacker first runs out of 'work,' and then runs out of money.

Where PoW and PoS attackers can use their majority to control the chain forever and profit from doing so, the same attack in Saito grows in expense the longer it goes on no matter how large the attacker is.

### Conclusion

The preservation of work, work which is independent of blocks, is not possible in PoW or PoS, and is how Saito eliminates 51% attacks.

Since the amount of work the honest network accumulates can only grow the longer they are censored, the amount of work the attacker must produce to keep censoring them also grows without bound, no matter if the attacker has 51% of inbound fees or 99%.

Even if the attacker owns 100% of inbound fees, as soon as they begin abusing users, new routing nodes are free to enter the network and begin taking market share and interrupting the majority fork. The ability for recovery from 100% attacks is not possible in any other blockchain.


