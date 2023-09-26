---
title: Sybils
description: 
published: true
date: 2023-09-26T10:17:14.951Z
tags: 
editor: markdown
dateCreated: 2023-09-24T00:24:44.788Z
---

## Sybils Constrain Distributed Networks

### Introduction

Per [Wikipedia](https://en.wikipedia.org/wiki/Sybil_attack): "A Sybil attack is a type of attack on a computer network service in which an attacker subverts the service's reputation system by creating a large number of pseudonymous identities and uses them to gain a disproportionately large influence." In blockchain, the relevant and remaining avenue for Sybils is to do with claims on rewards for propagating transactions into the distributed network of nodes collectively working to build blocks.

The original goal of blockchain was to instantiate a public network which anyone could participate in without permission; a native coin was both the primary feature, and a necessary security function to incentivize certain behaviors without relying on an external controller of that coin. The great freedom of of a permissionless network also conjures up problems with identity: voting on blocks can always be cheated because there is no central authority verifying each identity is unique and deserving of a vote.

This is the primary problem Bitcoin solved using Proof of Work as verification - anyone can create a block, but the cost and rewards associated in doing so make agreeing on a single fork the optimal strategy for everyone in the network, assuming an [honest majority](https://wiki.saito.io/en/consensus/majoritarian-attacks). With Sybilling for block production solved, Bitcoin went from impossible to practical, and all first generation blockchain has either followed in its footsteps or has made lateral tradeoffs.

### Routing Networks

With all the focus on block production, many have missed that while blockchain can get up and running in a practical sense, Sybils constrain the efficiency of distributed permissionless networks; particularly they constrain the propagation of transaction data. Consider a blockchain which can allow arbitrary amounts of transaction data into blocks. The optimal behavior of the network is that nodes will generously share transactions and build blocks more quickly than if it was not shared. In practice this does not happen.

This is precisely where Sybilling forces first generation permissionless networks to remain sub-optimal. If transaction fees reward block producers, rational nodes will not share it for free and cannot make trustless deals around it. If routing nodes are allowed to place signatures claiming partial rewards from fees, then they are able to duplicate their their contribution by Sybiling and maximize their reward without contributing meaningful propagation of transactions into the network.

The ability for nodes to Sybil routing rewards is exactly why blockchains do not bother implementing routing signature schemes - they accept that the rational strategy is for nodes to hoard transactions either way. Hoarding and Sybilling are two opposite outcomes of the same problem and so eliminating Sybil Attacks also eliminates the incentive to hoard, thus making possible a routing signature scheme which is secure against Sybil Attacks and disincentivizes hoarding.

### Collaboration

The optimal outcome for the network at large is that independent and competing nodes nonetheless have incentives to collaborate in ways that increase the efficiency and coordination of the routing network from which transactions come from. Much like how a person becomes unwell when regions of the brain fail to adequately communicate between one another, distributed networks become pathological when they disincentivize collaboration and coordination.

Not only is hoarding bad for network efficiency, it also concentrates power into the hands of the largest block producers. Users get transactions confirmed more quickly by sending to nodes who can actually produce blocks - not marginal producers. This leads to a self-reinforcing strategy where larger influences gain more and more power within the network and smaller contributions are irrational.

The fundamental cause of this illness is the ability to Sybil leading to the incentive to hoard. By eliminating Sybil Attacks, Saito defines what it means to be a second generation blockchain and can maintain a healthy, fair and open network at any scale. Nodes are rewarded for contribution, not their ability to cheat.
<hr>

### Proof

- Please refer [this](https://wiki.saito.io/e/en/consensus/sybil-proof) this page for an introductory as well as formal proof that Saito blockchain eliminates Sybil attacks in the routing network.