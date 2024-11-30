---
title: Nakamoto Consensus is a Keynesian Beauty Contest
description: 
published: true
date: 2024-11-30T08:18:40.662Z
tags: 
editor: markdown
dateCreated: 2024-11-30T08:18:40.662Z
---

# Nakamoto Consensus is a Keynesian Beauty Contest

*Written by David Lancashire on December 21, 2023*
![keynesian-beauty-contest.webp](/blog/keynesian-beauty-contest.webp)
In the Keynesian Beauty Contest, a newspaper asks its readers to select the best six images from a curated shortlist. After voting is complete, the reader whose ballot best matches overall public sentiment is crowned the winner. The mechanism is:

1. **A majoritarian voting system**, which creates
2. **An economic penalty on minority opinion**, which creates
3. **A self-reinforcing incentive to side with the majority**

Keynes intended his contest as an analogy for the stock market, but it equally describes Nakamoto Consensus, where consensus around the longest chain also emerges through a voting mechanism that punishes anyone who disagrees with majority opinion.

Despite the obvious parallels, few academics working on “cryptoeconomics” have read Keynes, or other economists like Mancur Olson who focus explicitly on incentivizing collective action. Instead, computer scientists focus overwhelmingly on building distributed voting mechanisms.

This intellectual bias has led computer science to approach consensus as a problem that requires voting. The blindness to other approaches starts with the way academics conceptualize the problems—consider the way the Byzantine Generals Problem is invariably described with the assumption that participants must honestly or dishonestly signal their preferred courses of action. They vote and only then do they act.

This drift away from incentives towards voting mechanisms is a major intellectual hurdle in distributed systems development, because as soon as we create voting mechanisms we automatically create majoritarian attacks on them. But isn’t our goal to avoid incentivizing collusion? Deciding how to distribute money based on majority opinion is not a workable approach.

And this is why understanding the Keynesian Beauty Contest matters. Because knowing that Satoshi designed Bitcoin as a beauty contest mechanism allows us to ask a simple question: why bother with the first step at all? Why add a voting mechanism? Why not look for a way to impose a cost-of-attack guarantee on malicious nodes that punishes attackers regardless of whether they control majority opinion?

Few people in distributed systems conceptualize the challenge this way, not trivially because many consider it an impossible problem, but there are already [formally-proven](https://github.com/SaitoTech/working-paper) methods of accomplishing exactly this. In our case, Saito Consensus does it by using “routing work” to increase the cost of producing blocks that orphan honest blocks, while also decreasing the amount of revenue attackers can earn from producing those blocks. Because of the way the payout mechanism works, attacking a routing work mechanism always costs money. Incentives impose a cost-of-attack directly or indirectly via a gameable voting mechanism.

By delivering what actually matters (the penalty and its results) without the need for a voting mechanism, routing work gives us all the benefits of the incentive structure in the Keynesian beauty contest (a self-reinforcing emergent consensus and natural incentive to cooperate) without adding the crippling majoritarian attacks. It gives us the properties that matter for distributed consensus without the technical vulnerabilities that come from adding majoritarian voting.

It will be interesting to see how long it takes computer science as a discipline to throw off its intellectual shackles. Until that happens, governance will continue to add attack vectors into distributed systems. And the solution to those problems will doubtless be yet more governance. This circularity is a problem with using voting mechanisms, but not a fundamental feature of consensus design. We can do better. And in order to solve the fundamental problems, we have to.
