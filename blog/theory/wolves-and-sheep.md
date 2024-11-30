---
title: Wolves and Sheep
description: 
published: true
date: 2024-11-30T08:45:33.710Z
tags: 
editor: markdown
dateCreated: 2024-11-30T08:45:33.710Z
---

# Wolves and Sheep

![wolves-and-sheep.webp](/blog/wolves-and-sheep.webp)

*Written by David Lancashire on July 27, 2021*

It has become conventional wisdom that there’s no way to tell attackers (wolves) from honest nodes (sheep) in an open network. The strength of this opinion is based partially on its promotion by talented developers like Vitalik Buterin and Zooko Wilcox-O’Hearn. But this opinion is nonetheless incorrect: to see why consider the difference that Bitcoin exploits:

> While honest users build on the chain-tip, attackers build from a block at least one confirmation deeper into the chain.

This difference exists because attackers who are re-organizing the chain must produce two blocks in the same amount of time that the honest network has to produce merely one. The network exploits this difference to tax attackers: the cost of producing blocks is identical for wolves and sheep, but sheep who produce at the tip of the longest-chain are far more profitable.

So blockchains do differentiate between wolves and sheep – they do it by taxing behavioral properties that any node might exhibit, but that attackers must exhibit. It does not matter if this tax occasionally penalizes an honest node with an unfortunately dim view of consensus. As long as attackers are disadvantaged relative to a subset of honest nodes, the network can maintain its cost-of-attack while incentivizing honest behavior.

But don’t majoritarian attacks put wolves back on equal footing with sheep? Some developers may make this claim (“what I meant was…”) but note the shift in logic: they have moved from asserting there are no behavioral differences between wolves and sheep to asserting that no differences exist which can be leveraged to penalize wolves in majoritarian conditions. And this claim is also false.

All we need to disprove it is a single a difference that can systematically tilt income away from all wolves and towards an unknown subset of sheep. And it turns out there is at least one behavioral difference with this property:

> When an attacker puts a transaction (that will be profitable for them to collect) into a block, they must be one hop deeper into the routing network than at least one honest node or user.

If an attacker is making money producing blocks, those blocks must by definition contain fees that come from someone else. In the absence of a block reward, every wolf that is not burning their own money to produce blocks must have at least one transaction in that block that was routed to them from an honest user or sheep, either sent to them as an unconfirmed transaction or stolen by them from a previously-published block.

As with Bitcoin’s tax on re-org depth, this difference can be leveraged to suppress the profitability of wolves: simply make block production more costly for deep-hop nodes, while forcing them to compete with shallow-hop nodes for control of the longest-chain. Saito does this by halving the value that fees contribute for producing blocks with every hop a transaction takes across the network. Any node at routing depth N+1 can produce only half the blocks and/or earn half the profits as a node at position N given the same set of transactions.

Taxing fee-transfers this way puts attackers at a disadvantage in producing blocks. This solution is counterintuitive to POW and POS developers as it requires the ratio between two variables that are fixed in their networks (cost of block production and income from producing blocks) to float. It also requires something missing in both POW and POS: cryptographic signatures that track who routes fees inwards towards block producers. Saito then tightens the noose further on wolves through a cryptographically-biased lottery that makes collecting payments less statistically likely for deep-hop nodes.

To conclude: security mechanisms in blockchains do not identify bad actors by intent. In this sense, those who insist it is impossible to tell the difference between “wolves” and “sheep” in blockchains are forgetting something they used to know: blockchains have always imposed cost-of-attack by taxing behaviors which must necessarily be exhibited by wolves and simply not caring if the trap ensnares a few unlucky honest sheep in the process.
