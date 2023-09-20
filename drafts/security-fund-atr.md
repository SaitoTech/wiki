---
title: Blockchain Security Budget and ATR
description: 
published: true
date: 2023-09-20T00:12:14.526Z
tags: 
editor: markdown
dateCreated: 2023-09-20T00:12:14.526Z
---

# Blockchain Security Budget and ATR

## Background

Every public blockchain needs to fund its security, and in general, the greater the security fund, the more *economically secure* that blockchain becomes, due to the fact that attackers must overcome a proportion of the money spent on security in order to successfully and profitably attack the chain.

Given that this 'security budget' is fundamental to the novel security that blockchain provides, a natural question then is: who is paying for it? In Bitcoin currently, the majority of the security budget, the rewards which incentivize miners to secure the network, come from *inflation.* What this means in practice is that *Bitcoin holders* are who pays for the majority of Bitcoin security - for now.

If Bitcoin is to become completely non-inflationary as planned, then the *entire* security budget must come from *transaction fees*. A heated debate in the Bitcoin community, which is emblematic of the core issue for all public blockchain, is whether the security budget will remain high enough to secure the network as inflation rewards diminish towards zero.

Many holders want inflation as low as possible so their coins become more valuable, but others worry that transaction fees alone will not be sufficient to defend the network, and thus the supply should grow to fund security. When it comes to the question of who will pay for the security fund, ATR provides a fair and simple supplement: make those sitting on blockchain *storage* pay to keep their limited space on-chain.

## Automatic Transaction Rebroadcasting (ATR)

Automatic Transaction Rebroadcasting is a simple consensus rule which states that a block is invalid if it does not forcibly rebroadcast all transactions which are at least $m$ blocks old - $m$ being the chosen 'epoch length.' Every transaction added to the chain thus has a 'lifespan' of $m$ blocks, and when it reaches the end of that lifespan, or epoch, will be automatically rebroadcast by the block producer into the latest block and will automatically pay a fee proportional to the average fee-per-byte paid during the epoch since it was added.

Put simply, every transaction must pay a fee every $m$ blocks which is related to the current fees new transactions are paying to occupy chain space. Since the fee paid when transactions undergo their ATR is similar to the average fee paid by new transactions, old transactions end up paying the market rate for space on the blockchain.

> Does this mean the blockchain isn't permanent? Doesn't that mean it can't be trusted or isn't a real blockchain?

Saito's security protocol pays staking rewards at the same time it charges ATR fees - users seeking permanent storage can ensure this by making sure their UTXO balance is in equilibrium with the staking portion (25%) of the fee-reward  distribution: a UTXO worth at least four times the fee rate. UTXOs which sustain the blockchain by using their staking rewards as rent can persist indefinetely on-chain without their balance diminishing.

On the more philosophic level, the removal of data from the blockchain in a systematic way does not make it any less of a universal and uncensorable ledger. In fact, without charging for storage or removing UTXOs too small to pay their for their storage burden, the chain itself becomes less sustainable and less likely to be funded into the future. ATR ensures that the blockchain can always pay for itself without centralized intervention.

## Security Budget

Independent of Saito's other innovations to consensus, Automatic Transaction Rebroadcasting is an important resolution to the problem all blockchain's must face around how to fund the security budget. It solves issues on both sides of the coin:

Even if a high-throughput chain can generate enough fees to reach a satisfiable level of total security, it eventually loses the ability to maintain the same fee-rate as the storage burden grows unbounded. Likewise, a low-throughput chain like Bitcoin requires sufficient fee-flow for security. ATR solves both issues: it charges a market rate for blockchain storage and puts those rewards into the hands of block producers.

The security impact is greater for chains with larger blocks, as the cost of processing the entire epoch necessary to learn of the transactions which must be rebroadcast represents a greater cost to block producers than when blockspace is artificially limited.

If blockspace is artificially scarce and users pay for that scarcity, block producers will not have the similar cost associated with processing and verifying a large amount of data - instead those resources go to hashing or staking. It remains a sustainable and fair method of increasing the rewards honest block producers and attackers compete to earn, and keeps holders majorly sheltered from the costs - unlike inflation.

ATR works best when blockspace is unconstrained and is allowed to set a market price for storage. Block producers can thus scale the blocksize as high or low as users are willing to pay for it by paying for it directly via ATR fees. The work required to sustain the actual block data and the work which contributes to security become one and the same.