---
title: Incentive Misalignments in Non-Saito Blockchains
description: 
published: true
date: 2024-03-05T06:48:23.530Z
tags: 
editor: markdown
dateCreated: 2022-03-25T07:08:04.493Z
---

# Saito Economics

Those familiar with market failures and blockchain may find the [Saito Whitepaper](https://saito.io/saito-whitepaper.pdf) a more succinct guide.

<ul>
  <li>  <a style="text-decoration:none" href="#mf"> Market Failures </a> </li>
  <li>  <a style="text-decoration:none" href="#complicated"> Is Saito Complicated? </a> </li>
  <li>  <a style="text-decoration:none" href="#fr"> Free Rider Problem </a> </li>
  <ul>
  	<li>  <a style="text-decoration:none" href="#chainIncentivesFR"> Blockchain Incentives </a> </li>
    <li>  <a style="text-decoration:none" href="#outcomesFR"> Sub-optimal Outcomes </a> </li>
    <li>  <a style="text-decoration:none" href="#solutionFR"> Saito Solution </a> </li>
  </ul><br>
  <li> <a style="text-decoration:none" href="#totc"> Tragedy of The Commons </a> </li>
  <ul>
  	<li>  <a style="text-decoration:none" href="#chainIncentivesTOTC"> Blockchain Incentives </a> </li>
    <li>  <a style="text-decoration:none" href="#outcomesTOTC"> Sub-optimal Outcomes </a> </li>
    <li>  <a style="text-decoration:none" href="#solutionTOTC"> Saito Solution </a> </li>
  </ul><br>
</ul>


## <div id="mf"> Market Failures </div>

Saito consensus primarily addresses two well studied market failures: situations in which the rational incentives of all participants individually lead to less prosperous outcomes for the collective. These suboptimal outcomes are pervasive due to the extreme sensitivity of systems to 'defection;' few dishonest players can exploit the honesty of the group and turn the 'honest' or 'nice' strategy into a losing one.

<br>
<div style="display: flex; justify-content: center; width: 100%;">
 <figure style="width: 70%; margin: auto;">
    <img style="width: 100%;" src="/prisoners_dilemma.svg.png" alt="A chart showing the prisoner's dilemma dynamic where defection is suboptimal globally, but individually preferred.">
    <figcaption style="opacity: 80%; text-align: center;">Staying silent results in less collective jailtime, but each individual has the incentive to testify anyways. <a href="#prisoner">Attribution</a></figcaption>
 </figure>
</div>
<br>

This dynamic is commonly referred to as a [Prisoner's Dilemma](https://en.wikipedia.org/wiki/Prisoner%27s_dilemma); the Wikipedia link lists some notable real-life examples. The standard solution to these market failures is to privatize access to the good in order to protect against exploitation. Since privatization of the blockchain is not an acceptable solution, adressing these market failures is crucial for scalable, secure and sustainable blockchain.

Saito is the first and only layer-1 blockchain to address these market failures on the consensus level, thereby avoiding the tough decision between remaining open or scaling network bandwidth. Saito consensus aligns the incentives for scale and openness as a single fee-sharing mechanism, and avoids collapse via bloat through a market-based rent system.

## <div id="complicated"> Is Saito Complicated? </div>

The cryptographic schemes in Saito which are repsonsible for addressing the market failures in Proof of Work and Proof of Stake are relatively simple, certainly less complicated than many modern Proof of Stake consensus protocols; so it is natural to ask: why is Saito the first and only blockchain to address these market failures?

The answer is that merely recognizing the true nature of the problem is difficult. Seeing that issues around scaling, openness, and security can be distilled down to a more fundamental problems and understanding how exactly cryptography and incentives can be employed to address those problems is where the sophistication lies. Once the problems are clearly identified, the mechanisms required to address them are elegant.

Thus in attempting to understand Saito, many study the crypographic schemes and understand them on a technical level, but still cannot truly explain what motivates the incentives therein. Most blockchain issues are framed as technical problems, but are in fact incentive-level, game-theoretic, economic problems - therefore many people study Saito with the wrong frame-of-mind.

This page hopes to explain the incentive-level issues which lead to market failures in Proof of Work, Proof of Stake and other non-Saito blockchains. The technical solutions may be easy to understand, but the economic motivations informing those solutions are key to a holistic understanding of Saito and blockchain generally.

## <div id="fr"> Free Rider Problem </div>

* A [video](https://youtu.be/XJiE8TrwW2A) overview on the Free Rider Problem, its relationship to blockchain, and Saito's solution is also available.

Free Rider Problems occur between the funding of a non-excludable good (one that everyone can enjoy) and the benefit of that good. Consider a group dedicated to removing litter at a free nature-park: all park-goers enjoy the benefit of a cleaner park, but only those donating time or money to the group have to pay for it. Everyone else is allowed to 'free-ride' off the expense of the maintainers.

> *Markets need to control the distribution of benefits to induce people to pay for them. If you're producing something that everyone can enjoy, you'll have difficulty convincing someone to pay you to cover the cost.*
> [Saito FAQs](https://saitofaqs.com/faq/how-does-saito-solve-the-free-rider-problem)

The classic solution to this problem is to *privatize* the once public good - to exclude access to its benefits in order to force payment from those seeking access to the good. But this solution is inadequate for goods which can't be restricted from public use, or which have open access as a founding principle: like blockchain.

### Blockchain Incentives

One of the key innovations in Bitcoin was that the act of securing the longest chain by mining atop it was not to be restricted to any authorized party, but to be a responsibility available to and rewarding to anyone; this is crucial for the incorruptibility of the network.

Likewise, any user wishing to send transactions need only to propagate that data to a node, or set of nodes, capable of mining it into a block - at least that was the vision. In theory and in practice, the collection of fee-paying transactions in PoW and PoS results in a Free Rider Problem.

Miners who wish to make money off of transaction fees must possess those transactions within their mempools before they begin mining. Since it can't be known who will produce the block, transactions must be sent to an arbitrary and large set of miners if they are likely to be included as soon as possible.

Because nodes or other services which collect and transmit transactions *do not know* who the next miner will be, they *must* send their transactions and the right to earn their fees to all miners; the nodes who actually route fees to the block producers are unable to earn those fees. The block producers (miners, stakers) are Free Riders atop transaction-routing nodes, because transaction relayers have no choice but to send to all of them to remain competitive.

<!--
Similar dynamics apply to any blockchain which cannot cryptographically certify and share claims on transactions fees, including all manner of Proof-of-Stake chains as well as  more exotic consensus mechanisms. Speeding up some aspect of consensus *technically* cannot solve the Free Rider Problem, which is an incentive-level roadbloack to scaling.
-->

In order for transaction collection to happen at scale on a PoW or PoS blockchain, the infrastructure which collects transactions must privatize that service in order to ensure they receive payment. This results in large nodes capable of choosing how rewards are distributed - both users and block producers become reliant upon them; this is a grave omen for security and openness, as the largest private firm in the network now has their finger on how the nodes providing security can earn.

### Sub-optimal Outcomes
<br>
<figure>
  <img src="/raspi4-btc.jpg" alt="An image of a small computer (Raspberry Pi) running a Bitcoin Node.">
  <figcaption style="opacity: 80%; text-align: center;"> Bitcoin Nodes are not powerful - image is under <a href="https://github.com/kdmukai/raspi4_bitcoin_node_tutorial?tab=MIT-1-ov-file#readme">MIT License</a> </figcaption>
</figure>

Different blockchains cope with the Free Rider Problem in different ways. Bitcoin very famously chooses to forgoe scaling so as to risk no compromises in the ability of interested volunteers to run nodes which verify the chain and route transactions to miners. Because the miners are expected to free-ride off of these nodes for the network to function, the chain has chosen to remain small in order to keep allowing low powered computers fulfill this task without compensation.

<br>
<div style="display: flex; justify-content: center;">
<figure>
  <img src="/cons-node-service.png" alt="Alt: What are the cons of using a Node Service? By using a node service you are centralizing the infrastructure aspect of your product. For this reason, projects that hold decentralization to the upmost importance might prefer self-hosting nodes rather than outsourcing to a 3rd party. Read more about the benefits of running your own node. -- from ethereum.org">
  <figcaption style="opacity: 80%; text-align: center;"> Ethereum recognizes danger in node infrastructure privatization - from <a href="https://ethereum.org/developers/docs/nodes-and-clients/nodes-as-a-service#cons-of-using-a-node-service">ethereum.org</a> </figcaption>
</figure>
</div>

Ethereum is a great example of the opposite tradeoff. In pushing the Free-Rider Problem towards its natural conclusion, crucial network infrastructure tends towards private control and centralization. The flagship example is the API node service [Infura](https://youtu.be/fJGuxcEvats) which is majorly responsible for serving applications both in service of developers and users. The massive userbase which the wallet Metamask serves primarily [routes through](https://support.metamask.io/hc/en-us/articles/4417315392795-What-is-Infura-and-why-does-MetaMask-use-it) Infura.

Infura and similar node providers serve more than just Ethereum. Dozens of chains with the ambition to scale their blockchain like or past Ethereum quickly outpace what independent full nodes are able to provide and fall-back to private solutions like Infura. This dynamic concentrates power and profit to private companies which can [censor](https://cryptoslate.com/metamask-blocks-ethereum-transactions-in-several-jurisdictions-citing-compliance-issues/), and [spy on](https://cointelegraph.com/news/metamask-will-start-collecting-user-ip-addresses) users.

So despite the fact that block producers in PoW and PoS are fairly compensated by following consensus rules, the free-riding dynamic involved in running the infrastructure is left neglected by consensus. It is not possible for nodes who route transactions into the network to secure any rewards from those transactions, thus it is necessary for traditional blockchains to accept restriction of network access in exchange for increased bandwidth, or to never increase bandwidth.

The users sending the transaction and the relay nodes propagating them into the network share the same incentive: deliver it to a block producer as quickly as possible. The user simply wants fast service, but the relay node needs to outcompete other relay nodes handling that transaction.

### Saito Fixes The Free Rider Problem

Recall the dilemma transaction-serving nodes face: in order to serve their users well (get transactions included in next block) they must distribute transactions to as many potential block producers as possible, but in order to profit from those fees, they must restrict access to that transaction data; they must privatize. Since block producers are necessary to fulfill the service, most node providers choose to privatize access to user-facing service instead.

In Saito there is no such dilemma. Nodes which share transactions do not risk the block producer who picks them up 'stealing' it from them - instead, the nodes with earlier access to the transactions become *entitled* to larger shares of the fee and compete with other early nodes to route the version of the transaction with their claim on it first. The incentives become aligned: nodes are both rewarded for collecting **and** sharing transactions.

The mechanism which solves the Free Rider Problem is **Routing Work**. A transaction carries a chain of digital signatures demarking how much fee each relay is due and how quickly each relay can produce the next block.

<br>
<div style="display: flex; justify-content: center; width: 100%;">
 <figure style="width: 56%; margin: auto;">
    <img style="width: 100%;" src="/routing-work-v3.png" alt="Diagram showing how transaction routing leads to block production then rewards in Saito.">
 </figure>
</div>

Because public-facing relay nodes are no longer doing free work for block producers, the infrastructure of the network which connects users to the blockchain is not required to restrict access in order to profit. The fees in the transaction pay their way into blocks through every hop, thanks to cryptography and consensus.

What users value and what nodes value in Saito is the same. Users want fast transaction confirmation (and security), and relay nodes secure the network and earn fees by getting their version of a transaction into a block before a competing routing node does. Because consensus nodes and users have the same incentive, **fees pay for what users actually value and optimizing rewards means optimizing user experience**.

The **practical benefits** which stem from this fundamental shift in incentives are profound:

* Security and scale are paid for from a single fee.
* Fee/byte is optimized in favor of cheaper service.
* Money spent on the network directly benefits users, rather than just serving to enrich large holders (stakers) or number crunchers (miners).



### Attributions:

<p id="prisoner"> By cmglee, http://github.com/emojione/emojione/graphs/contributors, http://github.com/twitter/twemoji#committers-and-contributors - This vector image includes elements from this file:, CC BY-SA 4.0, https://commons.wikimedia.org/w/index.php?curid=140014761 </p>

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