---
title: Tasks
description: this would all be incredibly helpful...
published: true
date: 2023-12-26T18:26:46.509Z
tags: 
editor: markdown
dateCreated: 2022-04-25T10:02:25.251Z
---

# Stuff People Can Help With
If you're not interested in joining or leading an application-development project, we have a list of standalone tasks that are more challenging. These are areas we are interested in exploring that could push us forward significantly, but that are not immediate priorities. If you can help us push forward that can change quickly.

## Compression of Routing Sigs
The path information that stores transaction routing sigs currently takes up a considerable amount of space. The reason for this is that every hop tracks the sender and the receiver and the signature associated with each hop. Look at how profligate a two-hop transaction might be:

```
[
"0" : { 
  "from" : "03ef28eba9f770682ee3805937ee73cc8d25052213afe775977d02e859954c98ad",
  "sig" : "a93e1c8d825edd61188d9af7e2c694b4d606aea09787f0443de1c081fb2778b631a3669e72944ad9b33ae4a7adb8817abba8893e1e34a217d21a01032753f456",
  "to" : "02f85c4312b2385f96e1aa55ec86c99fd1596cec0914266a86e2e2df70bc368809"
} ,
"1" : { 
  "from" : "02f85c4312b2385f96e1aa55ec86c99fd1596cec0914266a86e2e2df70bc368809",
  "sig" : "0b988c8260890d4dcc041f576f88c0ff6682a83e029b4dc7f3dc28ae60d3e7d300b9385f1c57953e810eaf390d976a3558d33e6e436d3f012902d8f047919975",
  "to" : "2AnXk35mKoJPHRWkViMWkFkZCR7JBWMwSfAShnZBK9jRv"
}
]
```

In the future it will be trivial to remove most of the addresses when creating compact blocks. The recipient of the previous hop can of course be assumed to be the sender of the next for instance. And addresses can be indexed separately.

Even with this approach, our routing signatures themselves are still large, contribute enough byte-data as hops grow that the cost-saving of using Saito over other networks will gradually disappear as the hop-length of the transaction increases. Longer routing paths also impose greater storage costs on the network long-term, although we could also conceivably prune them from transaction during ATR rebroadcasting.

With that said, one question is whether we can avoid this by using a commutative form of signature validation, where instead of three separate signatures that are added to transactions separately signers instead modify an existing signature. This may mean using an entirely different PKI algorithm and set-of-keys for routing work, but it might also be an extremely productive area of research. If we can find a way to replace multiple signatures with a single signature, the size of all transactions will fall non-trivially, which will assist with scale and faster transaction and block propagation generally.

If you are interested in helping us look into this, please note that any technique adopted must preserve the order of signatures. This is to prevent the block producer, for instance, from claiming to be the first node in the routing path and attacking the fairness of the routing lottery.

## N > 2 Diffie Hellman Key Exchange
Our ```encrypt``` module automates the process of creating a shared secret between two browsers. The technique we use is the Diffie-Hellman Key Exchange, which is the same sort of cryptographic exchange that secures online banking in the traditional Internet. The major difference is that doing this on Saito is better as there are no Man-In-The-Middle attacks.

It is possible to do this sort of exchange between more than 2 keys. The number of "transactions" needed to complete the process increases exponentially as the number of participants increase, but there is no reason we can't have groups of arbitrary size protected. This is more hardcore work involving underlying cryptography, but having this done would be tremendously useful in speeding up group chat and group gaming functions.

## Virtual Machines and Base Scripting

We do not want to be running a VM on the base Saito network layer that executes smart contracts. But there are open source VMs out there which support smart contracts and might be useful to deploy on Saito. We are also interested in exploring base-layer scripting.

It would be a meaningful research project for someone to look into what sort of open source VMs are available and start thinking about which approaches to scripting might be suitable for integration with Saito.

Having someone handle this research could easily speed up having some sort of smart contracts or scripting deployed atop Saito and available for reference by Saito applications.


## Creative Ways to Identify Attack Conditions?

One of the ways that Saito gains security is by increasing the cost-of-attack in real-time. The network can do this by increasing the number of tokens that attackers must burn in order to produce blocks in conditions where the network is observably under attack.

The current network design takes advantage of one such condition -- when the number of fees being paid into the network spikes above 125% of a long-term smoothed average the network responds by burning most of the additional tokens. This is done to ensure that attackers (who may be matching the work of the honest network) cannot recapture both their own fees as well as those of the honest network.

We would be interested in having other people think through what variables Saito's consensus layer can measure to identify attack conditions. If we can identify conditions that are heavily associated with attack conditions and which can be measured and thus agreed-upon by all of the nodes in the network at the point of block-validation, then we can respond to attacks by having our consensus layer increase the network burn requirements.

