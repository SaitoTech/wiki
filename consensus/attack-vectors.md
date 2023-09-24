---
title: Attack Vectors
description: how Saito is secure against common and uncommon attack vectors
published: true
date: 2023-09-24T00:39:29.323Z
tags: 
editor: markdown
dateCreated: 2022-03-22T10:08:41.187Z
---

# Attack Vectors 
Saito is secure against classes of attack which have no defense mechanisms in other chains. This page explains how these defense mechanisms work. Those interested in a mathematical overview of security may be interested in our [optimal attack reward](/consensus/math) calculations.

## 1. SYBIL ATTACKS
A sybil attack involves using a cheap or free form of work to undermine the income of a network participant who is performing a more expensive but essential network operation. Saito is secure against sybil attacks as the network's paid form of work is derived from fee collection and the only way to get paid more money (i.e. extract wealth) is to collect more money for the network and then collect only a portion of it in return.

Fortuitously, the cryptographic signatures Saito introduces to measure fee collection in its distributed network makes it possible to identify network-layer sybils. This can be done by examining the transaction-embedded routing paths and looking for nodes which occupy intermediate positions in the routing network and consume more in value than they contribute to their peers.

As every hop in a routing path lowers the profitability of every single node on that path, there is a strong incentive for all nodes to purge sybils from their routing paths. Block producers who permit sybils to form in the routing paths feeding them routing work experience an immediate 50 percent drop in their ability to produce blocks and collect payment. But even exterior notes which direct transaction flow to low-value sybils will be less profitable than their peers, and forced off the network through organic economic competition. Why should their users pay twice the fee to compensate for the extra and unnecessary hop?

Readers who believe that sybils may prevent communications between nodes are reminded that the blockchain can serve as a tool to communicate with distant peers as necessary.

- An expanded description and link to formal proof of Saito's *Sybil Proof*ness can be found [here](/consensus/sybil-proof).

## 2. TRANSACTION HOARDING
All blockchains which give transaction fees directly to the nodes that produce blocks are vulnerable to transaction-hoarding attacks.

In these attacks, block producers who pay to collect transactions refuse to share those transactions with their peers lest those peers "free-ride" on their work and gain market share at their expense. This problem emerges slowly as blockchains scale and the block reward falls, as the steps nodes need to take to prevent "free-riding" require them to cease the free distribution of consensus-level data. Hoarding creates many secondary problems. XThin-style fast block propagation techniques become unworkable when peers are unwilling to share pre-confirmation transaction set, while in hoarding equilibria users looking for fast confirmations now have incentives to direct their transactions to the largest and more profitable block producers, unleashing self-fullfiling centralization pressures on the network.

Saito is secure against transaction hoarding attacks. It achieves this by paying the nodes which collect transactions from users the largest share of the routing payment. Access nodes are incentivized to form at user-facing portions of the network - ensuring there will always be nodes competing to offer competitive and efficient routing into the network. Those nodes provide topological defense against attackers deeper in the network. And should these nodes not act in their own interests (hoarding can effect a zero-sum transfer of wealth from routers to block producers), users can always step in by re-routing their transaction flow to first-hop peers that are willing to defend the network.

Readers should note that once transactions are in circulation, the profitability of routing nodes depends on their forwarding received transactions as quickly and efficiently as possible. Any node which hoards transactions risks losing the chance of receiving payment for their work should the same transaction work its way into a block via another routing path. Mathematically, sharing transaction flow increases expected income in all situations in which the node is not capable of immediately producing a block and does not have the only copy of the transaction in circulation. While letting another node put the transaction into the block gives them a partial chance of payment, the routing node that forwards gains a much larger statistical chance of a payout should that node end up successful in using the transaction to produce a block.

## 3. BLOCK-FLOODING ATTACKS
Proof-of-Work networks require block producers to burn money to produce viable blocks. All peers are expected to forward all blocks by default, under the understanding that the hashing costs needed to create a block prevent block-flooding (DOS) attacks on the network. Does Saito's separation of block production from the hashing mechanism open the network to spam or block-flooding attacks?

Saito imposes block-flooding protections by stipulating that peers facing local network congestion only forward blocks once they have been convinced those blocks form part of the longest-chain. While nodes may thus forward the first block they receive from attackers, they will not forward subsequent blocks at the same block depth. The fact that every additional block produced imposes a cost on attackers ensures that this approach provides the same guarantee as POW: attackers cannot flood the network with data without paying the cost of block production that bites at N+1 blocks. Cryptographic sigs that can be attached to blocks as they propagate provide an additional way for nodes to monitor their peers for compliance with network routing policies. Non-compliant peers can be pushed into restrictive/punitive routing defaults.

There are additional steps that can be taken to increase the cost of block-spamming, such as requiring block producers to freeze/pledge a certain amount of network tokens when producing blocks, and permit those tokens to be seized on any fork should a party submit proof that the same funds have been "staked" to another block at a similar block depth. This mechanism implements a form of the same sort of staking/slashing penalty that POS relies upon to defend against these attacks, but one where cost-of-attack can be imposed within the logic of the longest-chain and cannot be skirted by majoritarian coalitions within the network with control over the longest-chain. Attackers who seek to remove blocks that will impose these costs face Saito's unavoidable cost-of-attack.

Saito additionally insists that any chain of N blocks proposed by block producers must contain a reasonable number of golden ticket solutions, to ensure that attackers are burning hashpower as well as money in long-range attacks on consensus. Given that the cost of producing the longest chain is significantly higher in Saito than Bitcoin, and there are no edge-cases where attacks can be carried out profitable, this ensures that spamming the chain costs roughly double that amount that it does in POW and POS networks where similar attacks can be carried out through self-funding hash and stake rental mechanisms.

The economic structure of the routing network incentivizes nodes to monitor their peers and maintain efficient network connections. Nodes which flood the network with data invite disconnection by imposing unnecessary costs on their peers. While nodes on the edge of the network may offer attackers an access point for data-flooding attacks, high-throughput nodes towards the center have strong economic incentives to penalize peers which impose undue costs on them. Malicious nodes must necessarily start their attacks from positions on the edge of the network, where their attacks require "flipping" honest nodes one-by-one. And note that flipping honest nodes onto an attacker's chain requires building deep rather than shallow forks, and committing to the cost-of-attack Saito enforces through its fee-burning and hashing mechanisms.

## 4. GRINDING ATTACKS
Proof-of-Stake networks without an explicit cost to block production are susceptible to grinding attacks. These occur when it is possible for nodes to create a large number of variant blocks in order to find one that benefits them.

This is not possible in Saito as block producers have no control over the block reward. Nodes which delay producing blocks for any reason also risk losing the entire value of their routing work, lowering their profitability and alienating the routing nodes with whom they are cooperating in sourcing transaction flow. Miners who find a golden ticket and fail to submit it promptly will not find another in time to collect any payment.

## 5. MAJORITARIAN ATTACKS
Saito is the only blockchain that is fully secure against 51 percent attacks. To understand how Saito accomplishes this, note that attackers who wish to attack the blockchain must necessary produce the same amount of routing work as the honest nodes as a prerequisite for issuing the longest-chain. Once that is done they must then match the amount of honest mining in the network in order to produce the golden tickets which allow them to get their money back from these blocks.

Security reaches the 100 percent level as attackers who do not include the "routing work" of honest nodes in their attack blocks face a non-stop increase in attack costs. Not only are they forced to match ALL CUMULATIVE OUTSTANDING ROUTING WORK when producing blocks (requiring a limitless increase in tokens) but the increased pace of block production traps miners in a situation where their mining costs must also rise as less time is available between blocks to find valid solutions.

The only way attackers can escape this trap is by "defusing" the accumulation of "routing work" outside their fork by including other people's transactions in their blocks. But in this case attackers must necessarily double their mining costs as it now takes two golden tickets on average to find a solution that will pay them (rather than an honest routing node) the block revenue. The security of the network is guaranteed by 100 percent of fee volume rather than merely 51 percent.

## 6. THE DEATH OF MOORE'S LAW
Blockchains secured by proof-of-work collapse once the supply curve of hashpower becomes reasonably elastic. This is why the death of Moore's Law is an existential threat all proof-of-work chains: commodity hardware production makes the slope of the supply curve for hashpower fully elastic. This problem is also why the shrinking block reward is a major issue for Bitcoin, as reduced miner revenue slows the pace of improvements in mining technology and makes 51 percent attacks feasible as well as profitable.

Saito remains secure beyond the death of Moore's Law. The reason for this is that the golden ticket system ensures that collecting 100 percent of the routing reward always costs 100 percet of network fees. The addition of proof-of-stake component adds a deadweight loss on top of this that imposes costs on attackers that are proportional to the percentage of the stake that is not controlled by the attacker multiplied by the proportion of total network revenue that is allocated to the staking pool.

As a result, the only situation in which attackers can theoretically avoid losing money attacking the network is if they control 100 percent of network hashpower, control 100 percent of the outstanding network stake, and are able to match 100 percent of the network stake. But even in this situation, the rational response for users facing an attack (an increase in the pace of block production) is to expand their own stake in the network. Economic forces move the network back to security even from extremes of centralized control. This is different from existing proof-of-stake implementations, in which stakers have an incentive to liquidate their stake when the network comes under attack.

## 7. I-HAVE-ALL-THIS-MONEY-WHY-DEAR-GOD-WILL-NO-ONE-SELL-ME-A-PEPSI ATTACKS
Occasionally people new to Saito think their way into circular critiques where there is some hypothetical attack on a Saito node that consists of an attacker maneuvering itself into being someone's only point of access to the network and leveraging that to censor transaction flows, extract supra-market rents or produce a dummy blockchain at a much slower rate than the chain produced by the honest network. We call these I-HAVE-ALL-THIS-MONEY-WHY-DEAR-GOD-WILL-NO-ONE-SELL-ME-A-PEPSI attacks.

All consensus systems fail in situations where one's view of the longest chain (i.e. consensus) is dictated by an attacker. Saito is no different than other blockchains in this regard. For those concerned about these issues, the important thing to note is that only Saito provides explicit economic incentives that prevent these issues. While proof-of-work and proof-of-stake variant networks typically suffer from an underprovision of unpaid access nodes, in Saito access to the network is easy: any scarcity in access points is an immediate and profitable commercial opportunity.

## 8. OTHER ATTACKS
Concerned about other attacks? Write up the description of the attack with which you are concerned and let's add it to the list.
