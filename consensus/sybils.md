---
title: Sybils
description: 
published: true
date: 2024-10-03T09:54:29.662Z
tags: 
editor: markdown
dateCreated: 2023-09-24T00:24:44.788Z
---

## What is a Sybil Attack

The traditional definition of a sybil attack is -- as per [Wikipedia](https://en.wikipedia.org/wiki/Sybil_attack) -- "a type of attack on a computer network in which an attacker subverts the service's reputation system by creating a large number of pseudonymous identities and uses them to gain a disproportionately large influence."

In blockchain, the term is used more loosely to describe any attack that disrupts a mechanism by substituting a cheaper or free activity for the kind of honest work that is needed by design. This is why many different types of activities are referred to as "sybil attacks" and why developers typically claim their mechanisms are "sybil-resistant" by identifying a single attack vector and making trade-offs to disincentivize that specific form of attack.

Proof-of-stake developers thus claim their networks are sybil-resistant because permissioned voting rings prevent nodes from creating false identities and voting with them. Proof-of-work developers claim their mechanisms are sybil-resistant because requiring nodes to hash to produce blocks prevents nodes from spamming the network with cheap/free blocks. Airdrops that limit who is eligible for token giveaways often refer to those mechanisms of closure as sybil-resistant mechanisms.

None of these approaches address sybil attacks as a fundamental attack vector. Proof-of-stake mechanisms have no control over whether sybils dominate their voting mechanisms. In proof-of-work networks you can still sybil the network by setting up cheap routing nodes and seeding the peer-to-peer network in a way that affects how block and transaction data propagates. In proof-of-stake networks In POW you can sybil the network simply by setting up routing nodes that add additional hops and favor/disfavor.

Saito solves the problem on the fundamental level. It accomplishes this because all sybil attacks necessarily require adding inefficiency into the network structure, and routing work as a consensus mechanism punishes participants who cooperate with sybils to produce and distribute blocks. This makes it less likely that sybils will produce blocks, and it makes the blocks they produce less profitable than they would be in the absence of the sybil node.

We have a mathematical proof that Saito Consensus is [sybil-proof](/consensus/sybil-proof). What becomes possible is a network that can pay for fee-collection, which means a network that can fund the user-facing nodes that pay for the bandwidth needed to operate the network.

### Collaboration

The optimal outcome for the network at large is that independent and competing nodes nonetheless have incentives to collaborate in ways that increase the efficiency and coordination of the routing network from which transactions come from. Much like how a person becomes unwell when regions of the brain fail to adequately communicate between one another, distributed networks become pathological when they disincentivize collaboration and coordination.

Not only is hoarding bad for network efficiency, it also concentrates power into the hands of the largest block producers. Users get transactions confirmed more quickly by sending to nodes who can actually produce blocks - not marginal producers. This leads to a self-reinforcing strategy where larger influences gain more and more power within the network and smaller contributions are irrational.

The fundamental cause of this illness is the ability to Sybil leading to the incentive to hoard. By eliminating Sybil Attacks, Saito defines what it means to be a second generation blockchain and can maintain a healthy, fair and open network at any scale. Nodes are rewarded for contribution, not their ability to cheat.
<hr>

### Proof

- Please refer [this](https://wiki.saito.io/e/en/consensus/sybil-proof) this page for an introductory as well as formal proof that Saito blockchain eliminates Sybil attacks in the routing network.