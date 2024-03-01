---
title: Incentive Misalignments in Non-Saito Blockchains
description: 
published: true
date: 2024-03-01T03:10:51.306Z
tags: 
editor: markdown
dateCreated: 2022-03-25T07:08:04.493Z
---

# Saito Economics

**under construction**

Those familiar with market failures and blockchain should skip ahead to the [Saito Whitepaper](https://saito.io/saito-whitepaper.pdf).



<!--
Saito consensus primarily addresses two well studied market failures: situations in which the rational incentives of all participants individually lead to less prosperous outcomes for the collective. These suboptimal outcomes are pervasive due to the extreme sensitivity of systems to 'defection;' few dishonest players can exploit the honesty of the group and turn the 'honest' strategy into a losing one.

This dynamic is commonly referred to as a [Prisoner's Dilemma](https://en.wikipedia.org/wiki/Prisoner%27s_dilemma); the Wikipedia link lists some notable real-life examples. The standard solution to these market failures is to privatize access to the good in order to protect against exploitation. Obviously, privatization of the blockchain is not an acceptable avenue, so adressing these market failures is key to instantiating a thriving and open network.

Saito is the
-->
<ul>
  <li>  <a style="text-decoration:none" href="#fr"> Free Rider Problem </a> </li>
  <li> <a style="text-decoration:none" href="#totc"> Tragedy of The Commons </a> </li>
</ul>

## <div id="fr"> Free Rider Problem </div>

* A [video](https://youtu.be/XJiE8TrwW2A) on the Free Rider Problem and its relationship to blockchain is also available.

Free Rider Problems occur between the funding of a non-excludable good (one that everyone can enjoy) and the benefit of that good. Consider a group dedicated to removing litter at a free nature-park: all park-goers enjoy the benefit of a cleaner park, but only those donating time or money to the group have to pay for it. Everyone else is allowed to 'free-ride' off the expense of the maintainers.

> *Markets need to control the distribution of benefits to induce people to pay for them. If you're producing something that everyone can enjoy, you'll have difficulty convincing someone to pay you to cover the cost.*
> [Saito FAQs](https://saitofaqs.com/faq/how-does-saito-solve-the-free-rider-problem)

The classic solution to this problem is to *privatize* the once public good - to exclude access to its benefits in order to force payment from those seeking access to the good. But this solution is inadequate for goods which can't be restricted from public use, or which have open access as a founding principle: like blockchain.

### In Blockchain

One of the key innovations in Bitcoin was that the act of securing the longest chain by mining atop it was not to be restricted to any authorized party, but to be a responsibility available to and rewarding to anyone; this is crucial for the incorruptibility of the network.

Likewise, any user wishing to send transactions need only to propagate that data to a node, or set of nodes, capable of mining it into a block - at least that was the vision. In theory and in practice, the collection of fee-paying transactions results in a Free Rider Problem.

### In Theory

Miners who wish to make money off of transaction fees must possess those transactions within their mempools before they begin mining. Since it can't be known who will produce the block, transactions must be sent to an arbitrary and large set of miners if they are likely to be included as soon as possible.

Because nodes or other services which collect and transmit transactions *do not know* who the next miner will be and thus *must* transactions and the right to earn their fees to all miners, the nodes who actually route fees into the network are unable to earn those fees. The miners are Free Riders atop transaction-routing nodes.

Similar dynamics apply to any blockchain which cannot cryptographically certify and share claims on transactions fees, including all manner of Proof-of-Stake chains as well as  more exotic consensus mechanisms. Speeding up some aspect of consensus *technically* cannot solve the Free Rider Problem, which is an incentive-level roadbloack to scaling.

In order for transaction collection to happen at scale on a PoW or PoS blockchain, the infrastructure which collects transactions must privatize that service in order to ensure they receive payment. This results in large nodes capable of choosing how rewards are distributed - both users and block producers become reliant upon them; this is a grave omen for security, as the largest private firm in the network now has their finger on how the nodes providing security can earn.

### In Practice
<br>
<figure>
  <img src="/raspi4-btc.jpg" alt="An image of a small computer (Raspberry Pi) running a Bitcoin Node.">
  <figcaption style="opacity: 80%; text-align: center;"> Bitcoin Nodes are not powerful - image is under <a href="https://github.com/kdmukai/raspi4_bitcoin_node_tutorial?tab=MIT-1-ov-file#readme">MIT License</a> </figcaption>
</figure>

Different blockchains cope with the Free Rider Problem in different ways. Bitcoin very famously chooses to forgoe scaling so as to risk no compromises in the ability of interested volunteers to run nodes which verify the chain and route transactions to miners. Because the miners are expected to free-ride off of these nodes for the network to function, the chain has chosen to remain small in order to keep allowing low powered computers fulfill this task without compensation.

<figure>
  <img src="/cons-node-service.png" alt="Alt: What are the cons of using a Node Service? By using a node service you are centralizing the infrastructure aspect of your product. For this reason, projects that hold decentralization to the upmost importance might prefer self-hosting nodes rather than outsourcing to a 3rd party. Read more about the benefits of running your own node. -- from ethereum.org">
  <figcaption style="opacity: 80%; text-align: center;"> Ethereum recognizes the danger of node infrastructure privatization - from <a href="https://ethereum.org/developers/docs/nodes-and-clients/nodes-as-a-service#cons-of-using-a-node-service">ethereum.org</a> </figcaption>
</figure>

Ethereum is a great example of the opposite approach. In pushing the Free-Rider Problem towards its natural conclusion, crucial network infrastructure tends towards private control and centralization. The flagship example is the API node service [Infura](https://youtu.be/fJGuxcEvats) which

<!--
The Free Rider Problem in Proof of Work, Proof of Stake, and their cousins manifests itself between the mismatch in the ability to earn fees by mining or holding stake, and the ability to *collect and include* fees by running full nodes. Clearly it is not an increase in mining or staking which scales the blockchain's throughput, but an increase in the collective bandwidth of network full nodes.

Saito takes principled issue with an all too common, naive libertarian response to this mismatch: "Miners or Stakers who increase their transaction bandwidth will increase their rewards." The reason is simple: holding a high volume of transaction fees does not grant the ability for such a node to earn those fees, because it does not grant them the ability to produce blocks.

Nodes which already produce a certain proportion of blocks cannot use an increase in fee volume to actually include those transactions and earn those fees, so these nodes have poor incentives to increase their bandwidth. The only way to increase fee rewards as a miner or staker is
-->

<!-- 
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