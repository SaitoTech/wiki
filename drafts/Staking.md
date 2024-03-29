---
title: Staking
description: Staking on Native Saito
published: true
date: 2024-02-19T22:11:41.373Z
tags: 
editor: markdown
dateCreated: 2024-02-19T21:00:59.990Z
---

# Staking on Saito

## Automatic Staking
All native Saito wallets will **automatically stake** their balances; there is no risk of slashing. All UTXOs on Saito can earn staking rewards with no further steps other than bridging to the native chain. There is no token lock-up.

Saito Consensus is non-inflationary and therefore the standard reward breakdown is highly dependent on the amount of fees within a given block. Deploying and maintaining popular applications is the best way for all Saito participants to earn more rewards.

## Rewards

**Early-Network Stakers:**

> Saito holders willing to bridge a [sufficient](https://wiki.saito.io/en/tokenomics#migration-to-native-saito-token) amount of tokens to the native chain will be eligible for increased rewards - the current estimate is 5%. Otherwise the standard reward is dependent on the fee-flow through the network.

To fully understand staking on Saito, it is necessary to understand the Golden Ticket and Automatic Transaction Rebroadcasting mechanisms.

The Golden Ticket mechanism securely generates random numbers to select routing nodes who will earn a share of transaction fees from a block they helped produce. The remaining fees will be paid to the miner who generated that random number and a random staker.

Elligible stakers for a block are selected during the Automatic Transaction Rebroadcasting process. This process tracks every live transaction in the Saito network and ensures their liveness by rebroadcasting and refreshing their UTXOs  at set intervals. When a transaction is rebroadcast into a new block, it pays a mandatory fee but also becomes elligible for the staking reward in that block.

Saito is a non-inflationary consensus mechanism, therefore, all rewards come from transaction fees and are split among routers, Golden Ticket miners, and UTXOs being rebroadcast (stakers). Staking rewards are a function of on-chain fee volume and may vary through time.

## Security

Staking in Saito exists to solve the problem of where to distribute token rewards should a Golden Ticket not be found for each individual block. Due to random chance, it may be the case that block producers can publish a valid block but Golden Ticket miners are unable to produce a ticket quickly enough.

In these instances, the routing rewards remain locked until a valid Golden Ticket for some future block *is* found - at that point, the routing rewards for all previous blocks are distributed to routers, the mining reward is distributed **only at the block including the Golden Ticket**, and the blocks which didn't include a Golden Ticket have their would-be mining rewards distributed to stakers.

Because attackers must spend tokens to produce blocks, they are constantly distributing tokens to stakers while taking themselves out of elligibility for staking rewards. A large portion of the money burned to launch such an attack would end up in the hands of stakers; attackers increase staking rewards.