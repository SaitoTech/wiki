---
title: An Open Comment on Tim Roughgarden’s Lecture Notes on Blockchain
description: 
published: true
date: 2024-11-30T08:36:21.273Z
tags: 
editor: markdown
dateCreated: 2024-11-30T08:36:21.273Z
---

# An Open Comment on Tim Roughgarden’s Lecture Notes on Blockchain

![an-open-comment-on.webp](/blog/an-open-comment-on.webp)

*Written by David Lancashire on October 27, 2022*

This blog post is an open comment written in response to Tim Roughgarden’s public lecture on permissionless blockchains. It is intended for any computer science student who is approaching Saito with the sort of distributed systems background taught in Prof. Roughgarden’s and similar courses. You can check out the lecture notes below – from a computer science perspective they are excellent.

[https://timroughgarden.github.io/fob21/l/l9.pdf](https://timroughgarden.github.io/fob21/l/l9.pdf)

From the Saito perspective, there are some problems though. The most significant is that it is incorrect to view public blockchains as sybil-resistance mechanisms wrapped around consensus algorithms. We understand why many researchers like this dichotomy. The distinction is easy to teach and feels productive.

But the dichotomy is incorrect. Once any network offers an outbound payment for performing a work function, that function no longer constitutes a sybil-resistance mechanism: you cannot refund payments and still count purchases as expensive. Under these conditions, what imposes cost-of-attack is the consensus layer, which decides which nodes receive spendable tokens in exchange for their work.

Computer scientists typically deal with this problem by axiomatically assuming that a majority of miners/stakers are honest. Under these conditions, there *must* be a cost-of-attack, and if there is a cost-of-attack, surely we should attribute it to the hashing or staking function where the money is spent? This feels like a harmless exercise – no shortage of papers start by making assumptions about node honesty and then derive formal proofs of security from these and other axioms. The problem is that we are doing this to maintain the illusion that the sybil-resistance layer is operating independent of the consensus layer.

Once you break this illusion, you are pulled towards a more powerful reality – the realization that consensus mechanisms impose cost-of-attack by asymmetrically taxing attackers. Nakamoto Consensus achieves this by keeping hashing costs constant for all nodes but decreasing the expected return for attackers, who must build multiple blocks in the same time their honest peers need to produce only one.

It is true that in Bitcoin this asymmetrical tax collapses in the face of a Byzantine majority. And while there is no theoretical reason to believe this problem is unsolvable (do all forms of asymmetrical taxation have this weakness?), the coincidence will likely stir critics to ask why we should favor any particular framework over another if both end up predicting failure in the face of majoritarian assault?

And the answer here is that both approaches are not equally vulnerable. If you believe that your sybil-resistance and consensus functions are distinct in the way Tim and others posit, you do end up trapped: it is pointless to strengthen your consensus mechanism against malicious majorities if their existence undermines a fundamental axiom you need to keep your network secure. The framework you adopt essentially defines majoritarian attacks as an unsolvable problem.

But if you focus on the way consensus mechanisms asymmetrically tax attackers, you have an open road ahead. Because you are suddenly looking for additional behavioral differences between honest nodes and attackers that can be (1) observed in distributed systems, and (2) leveraged to make proposing changes-of-state more costly for attackers than honest nodes.

This more accurate worldview encourages us to manipulate the same economic levers that Nakamoto Consensus does. It teaches us to improve on Satoshi’s solution not only by decreasing the payouts we offer attackers but even doing things that no proof-of-stake or proof-of-work network can accomplish: asymmetrically increasing the cost that attackers pay to propose blocks. The routing work mechanism that Saito Consensus introduces simultaneously accomplishes both of these objectives.

At the end of the day, definitional frameworks matter. With an inaccurate worldview, partisans are forced into axiomatic frameworks that make progress a theoretical impossibility and steer them away from viable solutions. Shifting to a more accurate framework easily doubles the size of our solution space and permits the development of mechanisms like Saito that can continue to impose cost-of-attack on attackers even in the face of malicious majority coalitions.
