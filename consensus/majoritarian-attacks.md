---
title: majoritarian-attacks
description: 
published: true
date: 2023-09-20T02:03:01.614Z
tags: 
editor: markdown
dateCreated: 2023-09-20T01:58:02.086Z
---

# Eliminating 51% Attacks

- For a complete mathematical proof [see here](https://wiki.saito.io/consensus/math).

### Consensus

Blockchain consensus protocols can be considered objective competitions which determines what additions may be considered valid and canonical. By all participants recognizing a single consensus protocol, a distributed network can reach full consensus without total coordination (each node is not required to query every other node), by simply judging this agreed upon objective measure between competing proposals, whether it be based on Proof of Work, Proof of Stake or something else.

## Majority Assumptions

### Proof of Work

Consensus design for distributed ledgers has come a long way since Bitcoin, which uses a longest-chain-rule and threshold of work within blocks to determine the priorities of competing blocks during disputes. Despite many technical advancements  atop the Bitcoin model, every consensus protocol, except for Saito's, falls prey to *Majoritarian Attack*, commonly referred to as the 51% Attack. 

While blockchain has provable and objective cost-of-attack when the majority of consensus power stems from honest, competing participants, the economic security unique to blockchain breaks down completely when a majority of power is held by any single, self-interested party. This majority coalition of 51% or more holds the power to censor all other blocks made by the 49% minority, because they can always build a longer chain.

The biggest issue with 51% attacks are there sustainability. Because overcoming the majority threshold allows attackers to produce all blocks without increasing their work production, attackers have the incentive and the means to *continue* the attack *indefinitely*.

### Proof of Stake

Advanced Proof of Stake systems like Ethereum may not map onto the Bitcoin metaphor as simply, but these systems are themselves not immune to majority assumptions and attack vectors unique those holding 51%, or even 33% of consensus power. Ethereum ultimately resolves to handling such pervasive attackers through *[Social Consensus](https://ethereum.org/en/developers/docs/consensus-mechanisms/pos/attack-and-defense/#people-the-last-line-of-defense)* i.e. a user initiated and approved fork.

While the principles of a 51% attack described on this page may not perfectly map to Proof of Stake, it is important to note that Saito views the concession to *Social Consensus* as a significant compromise on the objective consensus ability of blockchain and wholly inadequate solution to majoritarian attacks in Proof of Stake.

Since Saito is based off of Nakamoto Consensus, this document focuses on eliminating the possibility of 51% attacks in that context.

## How a 51% Attack Works

Fundamentally, 51% attacks work because the majority holder of consensus power can always build a longer valid chain than the remaining 49% of network participants can muster. Since the objective measure which the network agrees upon to accept new blocks is the longest chain or similar measure (DAGs for example, may not measure this in exactly these terms), a slight majority, on average, can always censor the rest of the network and still make a longer chain of work.

In an extreme scenario, the attacker could choose to never let the other half of the network produce a block on the longest chain ever again. This means that the attacker may produce 100% of blocks and earn all the rewards at only 51% the cost. There are many other possible specific attacks, like permanent censorship, consensus delay and double-spends, but the key ability driving it all comes from the ability of the majority attacker to overwrite the blocks, and the work, performed by the honest network.

In practice, the 49% of the network is still burning almost half the resources to perform the security function of the network, but because they must always commit this security function to the last-known perspective on the longest chain, and the attacker can always create a longer chain, the honest network constantly has the rug pulled out from under them.

Since work is not cumulative, the majority, on average, always wins - on a long enough timescale the majority always has the longest chain of valid work.

## How Saito Eliminates 51% Attacks - Cumulative, Block Agnostic Work

The objective measure of work required for Saito block production is special in many ways, but perhaps the most relevant for eliminating the 51% attack is that work in Saito is *Block Agnostic.*

Whereas in other blockchains, consensus nodes must commit to some recent fork in the blockchain in order to start producing the work which may earn them the right to build on top of that fork, consensus nodes in Saito can produce work and earn rewards *without even knowing* what the blockchain looks like. This is achieved through *routing work.*

In Saito, transactions are signed by senders such that the right claim rewards from it are given to relay nodes. This sharing of rewards can come directly from the author of the transaction, or from a relay node who wishes to propagate a transaction they were given. The more 'routing signatures' a transaction has, the more its reward is split between the routers and the less block work it can contribute to a block. Relevant to 51% attacks, the important aspect of this system is that the source of valid block work, transaction fees, *do not require a commitment to any particular fork.*

Note that a naive implementation of routing work alone is not sufficient for security under malicious majority conditions due to the possibility of fee-recycling attacks or more subtly, transaction hoarding attacks (which are possible when the reward decay of transaction routing is not set properly, or not at all, as is true in all other blockchains). Without providing detail, transaction rewards in Saito are split in half to Golden Ticket miners and routing nodes.

- See [this](https://wiki.saito.io/en/consensus) article or the [whitepaper](https://saito.io/saito-whitepaper.pdf) for a more complete description of routing work and securing it against fee-recycling attacks.

In Bitcoin, a node with 51% of hashpower produces a block and forces the entire network to start over on that new most recent block; it does not matter if the honest network sometimes finds a block first, because the attacker can always wait until their solo-mined-chain is longer. All work from the honest network is censored.

In Saito, a node with 51% of the current transaction fees must use those fees to produce a block, but the other 49% of transaction fees which were not involved do not suddenly lose their value, and can still be used to make valid blocks. This means any minority of work which remains unincluded in a block remains valuable to consensus nodes, and their ability to contribute to blocks cannot be censored by a malicious majority.

During an attempted attack, consensus nodes who were not allowed to make blocks accumulate work the longer they are censored, and the attacker quickly loses their work as they consume it to produce consecutive blocks, while the rest of the network's store of work grows and grows - both forces serving to reduce the length of the attack.

If an attacker in Saito wants to produce consecutive blocks, they must use up their transaction fees in place of the honest network's fees. Since producing new blocks does not remove the valid work within the transaction fees of all other consensus nodes, honest nodes can maintain their *accumulation* of work, which cannot be eliminated just because a new block is made - this preservation of work which is independent of blocks is not possible in PoW or PoS, and is the missing piece to eliminating 51% attacks in any consensus protocol.

Since the amount of work the honest network accumulates can only grow the longer they are censored, the amount of work the attacker must produce to keep censoring them also grows without bound, no matter if the attacker has 51% of inbound fees or 99%.

<hr>

- We invite researchers and auditors to consult a more rigorous [mathematical proof](/consensus/math) of Saito's elimination of the 51% attack.

