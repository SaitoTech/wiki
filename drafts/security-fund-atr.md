---
title: Blockchain Security Budget and ATR
description: 
published: true
date: 2024-02-13T19:24:22.945Z
tags: 
editor: markdown
dateCreated: 2023-09-20T00:12:14.526Z
---

# Blockchain Security Budget and ATR

## Background

Every public blockchain needs to fund its security, and in general, the greater the security fund, the more *economically secure* that blockchain becomes, due to the fact that attackers must overcome a proportion of the money spent on security in order to successfully and profitably attack the chain.

- Read about how Saito eliminates 51% attacks [here](/consensus/majoritarian-attacks).

Given that this 'security budget' is fundamental to the novel security that blockchain provides, a natural question then is: who is paying for it? In Bitcoin currently, the majority of the security budget, the rewards which incentivize miners to secure the network, come from *inflation.* What this means in practice is that *Bitcoin holders* are who pays for the majority of Bitcoin security - for now.

If Bitcoin is to become completely non-inflationary as planned, then the *entire* security budget must come from *transaction fees*. A heated debate in the Bitcoin community, which is emblematic of the core issue for all public blockchain, is whether the security budget will remain high enough to secure the network as inflation rewards diminish towards zero and user fees must fill in the gap.

Many holders want inflation as low as possible so their coins become more valuable, but others worry that transaction fees alone will not be sufficient to defend the network, and thus the supply should grow to fund security. When it comes to the question of who will pay for the security fund, ATR provides a fair and simple supplement: make those using blockchain *storage* pay a market rate to keep their space on-chain.

## Automatic Transaction Rebroadcasting (ATR)

Automatic Transaction Rebroadcasting is a simple consensus rule which states that a block is invalid if it does not forcibly rebroadcast all transactions which are at least $m$ blocks old - $m$ being the chosen 'epoch' length. Every transaction added to the chain thus has a 'lifespan' of $m$ blocks, and when it reaches the end of that lifespan, or epoch, will be automatically rebroadcast by the block producer into the latest block and will automatically pay a fee proportional to the average fee-per-byte paid during the epoch since it was added.

Put simply, every transaction must pay a fee every $m$ blocks which is related to the current fees new transactions are paying to occupy chain space. Since the fee paid when transactions undergo their ATR is proportional to the average fee paid by new transactions, old transactions compete for inclusion alongside new transactions, rather than simply remaining for free even though storage costs have changed.

Because the UTXO set of Saito is constantly being refreshed such that no transaction is greater than $m$ blocks old (the epoch length), nodes in Saito are thus able to verify than any possible  transaction is valid while only holding the last $2m$ historic blocks.

> Does this mean the blockchain isn't permanent? Doesn't that mean it can't be trusted or isn't a real blockchain?

**ATR cannot revert or invalidate historic block data.** What ATR does is refresh the age of all valid UTXOs and charge them a fee for that (mandatory) re-inclusion. Because all UTXOs exist in more recent block history, the data needed to validate any of them also exists solely in that recent block history.

### Staking and Permanent Data

Saito's security protocol pays staking rewards at the same time it charges ATR fees - users seeking permanent storage can ensure this by making sure their UTXO balance is in equilibrium with the staking portion (25%) of the fee-reward  distribution: a UTXO worth at least four times the fee rate. UTXOs which sustain the blockchain by using their staking rewards as rent can persist indefinitely on-chain without their balance diminishing.

On the more philosophic level, the removal of data from the blockchain in a systematic way does not make it any less of a universal and uncensorable ledger. In fact, without charging for storage or removing UTXOs too small to pay their for their storage burden, the chain itself becomes less sustainable and less likely to be funded into the future. ATR ensures that the blockchain can always pay for itself without centralized intervention and prevents forms of economic abuse where users add data for a small fee which must be preserved forever.

## Security Budget

Independent of Saito's other innovations to consensus, Automatic Transaction Rebroadcasting is an important resolution to the problem all blockchain's must face around how to fund the security budget. It solves issues on both sides of the coin:

Even if a high-throughput chain can generate enough fees to reach a satisfiable level of total security, it eventually loses the ability to maintain a stable fee-rate as the storage burden grows unbounded. Likewise, a low-throughput chain like Bitcoin requires sufficient fee-flow for security. ATR solves both issues: it charges a market rate for blockchain storage and puts those rewards into the hands of block producers; the nodes who end up storing and distributing the blockchain thus are paid for dealing with greater amounts of data, and thus can scale with demand.

The security impact is greater for chains with larger blocks, as the cost of processing the entire epoch necessary to learn of the transactions which must be rebroadcast represents a greater cost to block producers than when blockspace is artificially limited. Verifying and distributing block data in a large-block chain with ATR thus becomes its own form of *useful* work which rewards nodes supporting network infrastructure.

ATR works best when blockspace is not artificially constrained, thus allowing it to set a true market price for storage. Block producers can thus scale the blocksize towards what users are willing to pay via ATR fees. The work required to sustain the actual block data and the work which contributes to security become one and the same. A blockchain can thus finally pay for 'useful' work.


## Conclusion

Rather than paying for:

* Hashing (random number crunching)
* Staking (hoarding)
* Protien Folding (unrelated to blockchain)
* Artificial Intelligence (unrelated to blockchain)

ATR (and routing work) pay for the crucial infrastructure without which blockchain could not survive. Rather than trickling the minimum funding to this infrastructure or relying on volunteers or private companies to take responsibility, Saito ensures that nodes in the network compete to provide these services and are directly rewarded for doing so. By funding these operatoins through consensus, the blockchain prevents the privatization of the infrastructure layers, and supports truly public access at any scale.