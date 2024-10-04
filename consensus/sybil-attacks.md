---
title: Sybil Attacks
description: 
published: true
date: 2024-10-04T06:13:17.572Z
tags: 
editor: markdown
dateCreated: 2023-09-12T04:54:16.592Z
---

# Sybil Attacks

Saito Consensus is the first consensus mechanism that is known to be sybil-proof. While a mathematical proof of this claim is available in the paper [*A Simple Proof of Sybil Proof.*](https://github.com/SaitoTech/papers/blob/main/sybil/A_Simple_Proof_of_Sybil_Proof_Lancashire-Parris_2023.pdf), this page provides a non-technical introduction to what the problem is and how it can be solved.

## An Impossible Problem

> Many large decentralized systems rely on information propagation to ensure their
proper function... [we show] that there are no reward schemes in which information
propagation and no self-cloning is a dominant strategy.
<br>-Moshe Babaioff, Microsoft Research

A major centralizing pressure in blockchains is that nodes in possession of fee-bearing transactions do not have an incentive to share those transactions with their peers. Why share something worth money with those competing with you to collect it? Hoarding is the equilibrium response to 

Paying nodes who route transactions to the block producer can solve this problem, but quickly creates a secondary one, for how can we reward nodes that share transactions without encouraging them to add fake routing hops to maximize the number of routing hops they control and attack their competitors via the routing payout?

This is the problem Moshe Babaioff and his colleagues examined in their paper *[On Bitcoin and Red Ballons](https://arxiv.org/abs/1111.2626)* and promptly concluded it was impossible to solve, arguing that there are no reward schemes that can incentivize *information propagation* that do not also incentivize *self-cloning*. If you pay nodes to share, Moshe argues, you always encourage them to route their transactions through fake identities in order to maximize their expected share of the routing payout.

## A Groundbreaking Solution

Saito Consensus is the first consensus mechanism that solves this problem and properly incentivizes data propagation. It achieves this by eliminating sybil attacks entirely -- by ensuring that no costless strategies exist that will increase the expected payout nodes can expect from the payment lottery.

While the [mathematical paper](https://github.com/SaitoTech/papers/blob/main/sybil/A_Simple_Proof_of_Sybil_Proof_Lancashire-Parris_2023.pdf) linked above provides a rigorous proof of this, this page is intended to provide non-technical readers with an introduction to the problem. With this in mind, it's worth starting simply by pointing out exactly what *Babaioff* and his colleagues missed: what two critical assumptions they make about how blockchains must work that do not apply to routing work mechanisms and which permit routing approaches to skirt their impossibility proof.

The first assumption *On Bitcoin and Red Balloons* makes is that all nodes must face the same cost of producing blocks. This has been true in computer science research since the 1980s. This is true in proof-of-work mechanisms. And it is true in proof-of-stake mechanisms. But in routing mechanisms like Saito Consensus the cost of producing blocks differs for different nodes based on their position in the network and the compactness of the routing paths inside the transactions that they are putting into blocks.

Routing work mechanisms make it less expensive for nodes to produce blocks if they do so using transactions with compact routing paths. But adding fake routing hops to a transaction decreases the efficiency of the routing paths inside that transaction and thus makes it more expensive to produce a block using that transaction. The maths in our paper prove that this costs created by the addition of routing hops always increase costs faster than they increase the expected payout of those who sybil. This makes self-cloning a costly strategy?

But can we also incentivize propagation? *On Bitcoin and Red Balloons* assumes this is impossible because sharing a transaction cannot increase the income of nodes that share above what they could theoretically earn in a non-sharing equilibrium. Yet in Saito Consensus sharing increases the chance of both sender and recipient getting paid, because the recipient has their own mempool of routing work they can use to help get the transaction into a block faster than other nodes on other routing paths may be able to. Sharing shifts income away from nodes that hoard and towards nodes that share. There is a net increase in the income earned by nodes that share.

These two assumptions are buried in the *On Bitcoin and Red Balloons* paper where they are accepted uncritically in part because they describe how the Bitcoin network functions. Yet neither of these assumptions hold in routing work mechanisms, and the difference allows the creation of a secure network payout that cannot be attacked.

## A General Solution

Casual readers may ask how Saito Consensus can be a general solution given that the traditional definition of a sybil attack is -- as per [Wikipedia](https://en.wikipedia.org/wiki/Sybil_attack) -- "a type of attack on a computer network in which an attacker subverts the service's reputation system by creating a large number of pseudonymous identities and uses them to gain a disproportionately large influence."

The answer to this comes from observing that all sybil attacks involve the attacker exploiting a free or cheap activity in order to increase their expected claims-on-payout from a fee-distribution mechanisms. This is why developers who claim their mechanisms are "sybil-resistant" typically do so by identifying a single attack vector that involves exploiting a cheap activity (such as creating a new identity) and making it hard to exploit. Proof-of-stake developers argue POS is sybil-resistant because staking prevents people voting "for free". Proof-of-work advocates consider POW sybil-resistant because hashing makes it costly to flood the network with potential blocks. 

Yet neither POW nor POS is close to sybil-proof, as many cheap strategies remain which can undermine consensus. The most common of these attacks exist on the network layer, where attackers can strategically position nodes in ways where their routing decisions limit which blocks propagate quickly and become part of the longest-chain. Another costless way to attack consensus is simply not to forward network information or fee-bearing transactions to peers.

Recognizing this makes it possible to understand how Saito eliminates sybilling on a fundamental level: by making all forms of value-extraction expensive. Under routing work all activities that generate claims-on-payout require nodes to contribute more in inbound fee-flow than they can statistically recover. The maths in the paper linked above demonstrate this conclusively by comparing the expected payoffs of various routing and sharing strategies.

But what about other network-layer strategies? Are the same cheap workarounds available in Saito Consensus that exist in mechanisms? And the answer is no, because the routing paths that are embedded in the transaction are a measure of the efficiency of the network itself. Seeding the network with additional identities necessarily requires adding routing hops to either transactions or the network itself. Attackers are back to square one, because the increased inefficiency they have created decreases the expected payout for all nodes on that routing path.

Put more plainly, with Saito Consensus you can *try* to sybil, but all you do is reduce the efficiency of the network and increase your costs faster than your expected income. Sybilling becomes a strictly dominated strategy.

## Conclusion

Saito Consensus is a groundbreaking advance in distributed consensus. We encourage all readers to dig into the information problems described on this page and about how to address them using routing signatures.

