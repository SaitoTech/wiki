---
title: Incentive Misalignments in Non-Saito Blockchains
description: 
published: true
date: 2023-12-11T03:43:07.244Z
tags: 
editor: markdown
dateCreated: 2022-03-25T07:08:04.493Z
---

# Saito Economics

The [Saito Whitepaper](https://saito.io/saito-whitepaper.pdf) discusses the two incentive problems that prevent POW and POS blockchains from achieving the scale necessary to support web3 applications: a tragedy-of-the-commons problem that leads to blockchain bloat; and a free-rider problem that encourages participants to do paid-work like mining and staking at the expense of the unpaid work that ultimately pays for mining and staking.

These problems are collective action problems: types of market failure that  occur when participants have incentives to behave in ways that maximize their own profits but impose costs on society as a whole. In the tragedy-of-the-commons problem, miners make money today by putting data on the blockchain that must be supported by other members of the network in the future. There is a privatization of gain (today) and a socialization of losses (tomorrow). In the free-rider problem, participants maximize profits by refusing to pay for necessary but costly activities like running peer-to-peer infrastructure, and spend their money instead on the narrow set of paid network activities as this strategy *maximizes income regardless of whether the other participants in the network do*.

Economists have written about these types of market failures for decades. An entire school of research (“public choice theory”) is in fact devoted to what happens in markets with these sorts of incentive misalignments. The critical problem is that in a open network you cannot punish individuals who follow their incentives without the exactly the sort of trusted third-party or market cartel (collusion) that negates the raison d’etre of a public blockchain.

Among the two problems that Saito solves, the tragedy of the commons problem is the easier of the two problems to eliminate, and we will not spend much time on it here. In short, Saito fixes the problem by introducing a market-based pruning mechanism to the blockchain. This mechanism results in transactions paying their fees out to block producers over time rather than all-at-once. This prevents nodes from adding transactions to the chain that do not pay enough fees to cover the actual costs of operating the blockchain. In addition to eliminating blockchain bloat, the Saito solution fixes several other intransigent problems, such as allowing the network to properly calculate the cost of on-chain storage into perpetuity. If you want to store data on a blockchain forever, Saito will actually let you do it.

Eliminating the free-rider problem is harder as it requires replacing mining and staking with routing work, a measure of how efficient nodes are at collecting and sharing the fees that users are paying to use the network. Instead of paying for mining and staking and asking participants to pay for other stuff, Saito simply pays them for sharing fees and other forms of value with the other participants in the network. In Saito Consensus, nodes compete to source any transactions that pay fees to use the network. This is the equivalent of paying for routing (specifically, the routing of fee-bearing data) and using this activity to secure the network — an activity we are already paying for — eliminates the need for separate fees for mining and staking.

The use of a form of work that derives claims-on-payment from money-flows opens the door to the prospect of circular economic attacks on the payment mechanism. Saito is not unique in facing this problem. This is actually a critical and unsolved vulnerability in POW and POS networks. Picture what can happen to those networks, for instance, once it is possible for participants to rent hash/stake, produce blocks, and then use the income from those blocks to pay for the cost of renting more hash/stake.

Saito Consensus prevents this kind of fee-circularity with an elegant cryptographic lottery with a critical economic property: attackers must spend more money attacking the lottery than they can ever gain by producing a block. This solution is known as the “golden ticket” system. It eliminates the 51 percent attack and ensures that attacks remain quantifiably costly even under majoritarian conditions. The golden ticket system also ensures that payments flow to the nodes that are servicing users and performing routing work regardless of whether they are the ones that produce the block itself.

The result is an ingenious up-ending of economic fundamentals of blockchain, but in a manner that actually delivers on the original promise of Bitcoin. Saito creates a truly permissionless data network that remains self-sufficient and trustless at scale: it is actually capable of paying for all of the activities in the network that contribute value. If you are new to Saito, you may enjoy this “poker video” which attempts to offer a visually-intuitive explanation of the lottery mechanism that forces attackers into a catch-22 and requires them to haemorrhage money should they wish to attack the chain.

The outcome in either case is a network with the scale to support web3 data-throughput, and the economic structure to support the maintenance of whatever blockchain infrastructure provides the greatest value to network users.

The rest of this site contains information documenting Saito consensus and introducing developers to the network. If you have questions about Saito or are interested in getting involved, please join our Telegram channel or any of the numerous communities that are living and growing on Saito.