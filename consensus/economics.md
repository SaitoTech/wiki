---
title: Incentive Misalignments in Non-Saito Blockchains
description: 
published: true
date: 2024-03-14T05:31:57.614Z
tags: 
editor: markdown
dateCreated: 2022-03-25T07:08:04.493Z
---

# Saito Economics

Those familiar with market failures and blockchain may find the [Saito Whitepaper](https://saito.io/saito-whitepaper.pdf) a more succinct guide.

<ul>
  <li>  <a style="text-decoration:none" href="#mf"> Market Failures </a> </li>
  <li>  <a style="text-decoration:none" href="#elegant"> Saito is Elegant </a> </li>
  <li>  <a style="text-decoration:none" href="#fr"> Free Rider Problem </a> </li>
  <ul>
  	<li>  <a style="text-decoration:none" href="#chainIncentivesFR"> Free Rider Incentives in Blockchain </a> </li>
    <li>  <a style="text-decoration:none" href="#outcomesFR"> Sub-optimal Outcomes of Free Riding </a> </li>
    <li>  <a style="text-decoration:none" href="#solutionFR"> Saito's Open Solution to Free Riding </a> </li>
  </ul><br>
  <li> <a style="text-decoration:none" href="#totc"> Tragedy of The Commons </a> </li>
  <ul>
  	<li>  <a style="text-decoration:none" href="#chainIncentivesTOTC"> Tragedy of The Commons Incentives in Blockchain </a> </li>
    <li>  <a style="text-decoration:none" href="#outcomesTOTC"> Sub-optimal Outcomes of The Tragedy of The Commons </a> </li>
    <li>  <a style="text-decoration:none" href="#solutionTOTC"> Saito's Open Solution to The Tragedy of The Commons </a> </li>
  </ul><br>
</ul>

## <div id="mf"> Market Failures </div>

Saito consensus primarily addresses two well studied market failures, The <a style="text-decoration:none" href="#fr"> Free Rider Problem </a>, and The <a style="text-decoration:none" href="#totc"> Tragedy of The Commons </a> - both well-founded and recognized game theoretic dilemmas; the only assumption being that self-interested actors behave rationally.

Market failures are situations in which the rational incentives of individuals leads to less prosperous outcomes for everyone. These sub-optimal outcomes are pervasive due to the extreme sensitivity of naive systems to 'defection;' few dishonest players can exploit the honesty of the group and turn the 'honest' or 'nice' strategy into a losing one.

<br>
<div style="display: flex; justify-content: center; width: 100%;">
 <figure style="width: 70%; margin: auto;">
    <img style="width: 100%;" src="/prisoners_dilemma.svg.png" alt="A chart showing the prisoner's dilemma dynamic where defection is suboptimal globally, but individually preferred.">
    <figcaption style="opacity: 80%; text-align: center;">Prisoner's Dilemma: staying silent results in less collective jailtime, but each individual has the incentive to testify in every scenario. <a href="#prisoner">Attribution</a></figcaption>
 </figure>
</div>
<br>

This dynamic is commonly referred to as a [Prisoner's Dilemma](https://en.wikipedia.org/wiki/Prisoner%27s_dilemma); the Wikipedia link lists some notable real-life examples. The standard reaction to the dilemma in the context of market failures is to privatize access to the good in order to protect against exploitation. 

**Saito exists to solve market failures in Proof of Work and Proof of Stake, without privatization of the blockchain.** Addressing these market failures is crucial for scalable, secure, sustainable and most importantly, open, blockchain.

Saito is the first and only layer-1 blockchain to address these market failures on the consensus level, thereby avoiding the tough decision between remaining open or scaling network bandwidth. Saito consensus aligns the incentives for scale and openness as a single fee-sharing mechanism, and avoids collapse via bloat through a market-based rent system.

## <div id="elegant"> Saito is Elegant </div>

The cryptographic schemes in Saito which are responsible for addressing the market failures in Proof of Work and Proof of Stake are relatively simple, certainly less complicated than many modern Proof of Stake consensus protocols; so it is natural to ask: why is Saito the first and only blockchain to address these market failures?

The answer is that merely recognizing the true nature of the problem is difficult. Seeing that issues around scaling, openness, and security can be distilled down to  more fundamental problems and understanding how exactly cryptography and incentives can be employed to address those problems is where the sophistication lies. Once the problems are clearly identified, the mechanisms required to address emerge somewhat naturally.

Thus in attempting to understand Saito, many study the cryptographic schemes and understand them on a technical level, but still cannot truly explain what motivates the incentives therein. Most blockchain issues are framed as technical problems, but are in fact incentive-level, game-theoretic, economic problems - therefore many people study Saito with the wrong frame-of-mind.

> <i>The problem with blockchain scaling is not at the network technology layer: at the time of writing, data centers around the world are im- plementing 400 Gbps network switches while 100 Gbps connections are becoming standard even in lower-tier colocation facilities... </i>
> 
> <i>...What limits network growth is the challenge of paying for the network. In the past, non-economists have waved away this limitation, claiming that as long as someone is earning money from the network they will pay all costs necessary to support it. But this is not true...</i>
> -[Saito Whitepaper](https://saito.io/saito-whitepaper.pdf)

This page hopes to explain the incentive-level issues which lead to market failures in Proof of Work, Proof of Stake and other non-Saito blockchains. The technical solutions may be easy to understand, but the economic motivations informing those solutions are key to a holistic understanding of Saito and blockchain generally.

## <div id="fr"> Free Rider Problem </div>

* A [video](https://youtu.be/XJiE8TrwW2A) overview on the Free Rider Problem, its relationship to blockchain, and Saito's solution is also available.

Free Rider Problems occur between the funding of a non-excludable good (one that everyone can enjoy) and the benefit of that good. Consider a group dedicated to removing litter at a public nature-park: everyone collectively enjoys the benefit of a cleaner park, but only those donating time or money to the group have to pay for it. Everyone else is allowed to 'free-ride' off the expense of the maintainers.

> *Markets need to control the distribution of benefits to induce people to pay for them. If you're producing something that everyone can enjoy, you'll have difficulty convincing someone to pay you to cover the cost.*
> -[Saito FAQs](https://saitofaqs.com/faq/how-does-saito-solve-the-free-rider-problem)

The classic solution to this problem is to *privatize* the once public good - to exclude access to its benefits in order to solicit appropriate payment. But this solution is inadequate for goods which can't be restricted from public use, or which have open access as a founding principle; in the case of blockchain, **the routing of fee-paying transaction towards the block producers who hoards the total fee-reward is a Free Rider Problem.**

### <div id="chainIncentivesFR"> Free Rider Incentives in Blockchain </div>

One of the key innovations in Bitcoin was that the act of securing the longest chain by mining atop it was not to be restricted to any authorized party, but to be a responsibility available to and rewarding to anyone; this is crucial for the incorruptibility of the network.

Likewise, any user wishing to send transactions need only to propagate that data to a node, or set of nodes, capable of mining it into a block - at least that was the vision. In theory and in practice, the collection of fee-paying transactions in PoW and PoS results in a Free Rider Problem, because sharing transaction data means *giving up* the ability to earn the fee.

<br>
<figure>
  <img src="/bitcoin-whitepaper-network-assumptions.png" alt="The steps to run the network are as follows:
1) New transactions are broadcast to all nodes.
2) Each node collects new transactions into a block.
3) Each node works on finding a difficult proof-of-work for its block.
4) When a node finds a proof-of-work, it broadcasts the block to all nodes.
5) Nodes accept the block only if all transactions in it are valid and not already spent.
6) Nodes express their acceptance of the block by working on creating the next block in the chain, using the hash of the accepted block as the previous hash.
Nodes always consider the longest chain to be the correct one and will keep working on extending it. If two nodes broadcast different versions of the next block simultaneously, some nodes may receive one or the other first. In that case, they work on the first one they received, but save the other branch in case it becomes longer. The tie will be broken when the next proof- of-work is found and one branch becomes longer; the nodes that were working on the other branch will then switch to the longer one.">
  <figcaption style="opacity: 80%; text-align: center;"> Nakamoto assumed transactions would be widely broadcast but did not foresee The Free Rider Problem afflicting this task - <a href="https://github.com/kdmukai/raspi4_bitcoin_node_tutorial?tab=MIT-1-ov-file#readme">Bitcoin Whitepaper</a> </figcaption>
</figure>

[On Bitcoin and Red Balloons](https://arxiv.org/abs/1111.2626) famously and correctly identifies this problem within blockchains which existed at the time. However, it incorrectly proports that "there are no reward schemes in which information propagation and no self-cloning is a dominant strategy - " (skipping ahead) this conclusion is proven incorrect using Saito consensus in [A Simple Proof of Sybil Proof](https://github.com/SaitoTech/papers/blob/main/sybil/A_Simple_Proof_of_Sybil_Proof_Lancashire-Parris_2023.pdf).

Miners who wish to make money off of transaction fees must possess those transactions within their mempools before they begin mining. Since it can't be known who will produce the block, transactions must be sent to an arbitrary and large set of miners if they are likely to be included as quickly as possible.

Because nodes or other services which collect and transmit transactions *do not know* who the next miner will be, they *must* send their transactions and the right to earn their fees to all miners; the nodes who actually route fees to the block producers are unable to earn those fees. The block producers (miners, stakers) are Free Riders atop transaction-routing nodes, because transaction relayers have no choice but to give up these transactions if they are to remain useful to their users.

<!--
Similar dynamics apply to any blockchain which cannot cryptographically certify and share claims on transactions fees, including all manner of Proof-of-Stake chains as well as  more exotic consensus mechanisms. Speeding up some aspect of consensus *technically* cannot solve the Free Rider Problem, which is an incentive-level roadbloack to scaling.
-->

In order for transaction collection to happen at scale on a PoW or PoS blockchain, the infrastructure which collects transactions must privatize that service in order to ensure they receive payment. This payment is either an additional cost users must pay, or it detracts from the 'security budget;' i.e. the fees which grant the blockchain economic security against consensus attacks.

This inadvertent privatization can turn large portions of a blockchain network into a [permissioned system](https://cryptopotato.com/ethereum-censorship-concerns-raised-as-block-builders-comply-with-ofac-sanctions/), but the other option is to remain a non-scalable chain. The debates around "scale versus decentralization" can be more precisely framed as tradeoffs around an unaddressed Free Rider Problem.

<!-- This results in large nodes capable of choosing how rewards are distributed - both users and block producers become reliant upon them; this is a grave omen for security and openness, as the largest private firm in the network now has their finger on how the nodes providing security can earn. -->

### <div id="outcomesFR"> Sub-optimal Outcomes of Free Riding </div>
<br>
<figure>
  <img src="/raspi4-btc.jpg" alt="An image of a small computer (Raspberry Pi) running a Bitcoin Node.">
  <figcaption style="opacity: 80%; text-align: center;"> Bitcoin Nodes are not powerful - image is under <a href="https://github.com/kdmukai/raspi4_bitcoin_node_tutorial?tab=MIT-1-ov-file#readme">MIT License</a> </figcaption>
</figure>

Different blockchains cope with the Free Rider Problem in different ways. Bitcoin very famously chooses to forgo scaling in order to ensure unpaid, low-powered nodes can and will route transactions to miners. Because the miners are expected to free-ride off of these nodes for the network to function, the chain has chosen to remain small with the hopes that volunteers will continue to perform this task without compensation.

Ethereum is a great example of the opposite tradeoff. In pushing the Free-Rider Problem towards its natural conclusion, crucial network infrastructure tends towards private control and centralization.

<br>
<div style="display: flex; justify-content: center;">
<figure>
  <img src="/cons-node-service.png" alt="Alt: What are the cons of using a Node Service? By using a node service you are centralizing the infrastructure aspect of your product. For this reason, projects that hold decentralization to the upmost importance might prefer self-hosting nodes rather than outsourcing to a 3rd party. Read more about the benefits of running your own node. -- from ethereum.org">
  <figcaption style="opacity: 80%; text-align: center;"> Ethereum recognizes danger in node infrastructure privatization, but can't stop it - from <a href="https://ethereum.org/developers/docs/nodes-and-clients/nodes-as-a-service#cons-of-using-a-node-service">ethereum.org</a> </figcaption>
</figure>
</div>

The flagship example is the API node service [Infura](https://youtu.be/fJGuxcEvats) which is majorly responsible for serving applications both in service of developers and users. The massive userbase of the Metamask wallet is primarily [routed through](https://support.metamask.io/hc/en-us/articles/4417315392795-What-is-Infura-and-why-does-MetaMask-use-it) [and dependent](https://decrypt.co/98457/metamask-ethereum-apps-down-infura-outage) on Infura, not to mention the prolific share of 'decentralized' applications reliant on it. Note that Infura and other node providers mainly run their infrastructure atop even more centralized operations like AWS.

Infura and similar node providers serve more than just Ethereum. Dozens of chains with the ambition to scale their blockchain like or past Ethereum quickly outpace what independent full nodes are able to provide and fall-back to private solutions like Infura. This dynamic concentrates power and profit to private companies which can [censor](https://cryptoslate.com/metamask-blocks-ethereum-transactions-in-several-jurisdictions-citing-compliance-issues/), and [spy on](https://cointelegraph.com/news/metamask-will-start-collecting-user-ip-addresses) users, and which take security from the underlying blockchain to instead finance closed revenue streams.

Private operations running blockchain nodes isn't the issue, but their lack of accountability towards the blockchains they serve is. Whereas mining and staking have built-in punishment for nodes who misbehave, censor, or perform sub-optimally, the typical dynamics of monopoly are the rules that apply to node services whose work is so disconnected from consensus.

<!--
The users sending the transaction and the relay nodes propagating them into the network share the same incentive: deliver it to a block producer as quickly as possible. The user simply wants fast service, but the relay node needs to outcompete other relay nodes handling that transaction. -->

### <div id="solutionFR"> Saito's *Open* Solution to Free Riding </div>

Recall the dilemma transaction-serving nodes face: in order to serve their users well (get transactions included in next block) they must distribute transactions to as many potential block producers as possible, but in order to profit from those fees, they must restrict access to that transaction data; they must privatize. Since block producers are necessary to fulfill the service, most node providers choose to privatize access to user-facing service instead.

In Saito there is no such dilemma. Nodes which share transactions do not risk the block producer who picks them up 'stealing' it from them - instead, the nodes with earlier access to the transactions become *entitled* to larger shares of the fee and compete with other early nodes to route the version of the transaction with their claim on it first. The incentives become aligned: nodes are both rewarded for collecting **and** sharing transactions.

The mechanism which solves the Free Rider Problem is **Routing Work**. A transaction carries a chain of digital signatures demarking how much fee each relay is due and how quickly each relay can produce the next block.

<br>
<div style="display: flex; justify-content: center; width: 100%;">
 <figure style="width: 56%; margin: auto;">
    <img style="width: 100%;" src="/routing-work-v3.png" alt="Diagram showing how transaction routing leads to block production then rewards in Saito.">
 </figure>
</div>

Because public-facing relay nodes are no longer doing free work for block producers, the infrastructure of the network which connects users to the blockchain is not required to restrict access in order to profit, thus the network layer can be funded **without defunding security**. This means scale and security are not mutually exclusive, they are in fact the same metric in Saito - therefore, Saito proves the blockchain trilemma does not exist.

What users value and what nodes value in Saito is the same. Users want fast transaction confirmation (and security), and relay nodes secure the network and earn fees by getting their version of a transaction into a block before a competing routing node does. Because consensus nodes and users have the same incentive, **fees pay for what users actually value and optimizing rewards means optimizing user experience**.

The **practical benefits** which stem from this fundamental shift in incentives are profound:

* Security and scale are paid for from a single fee.
* Fee/byte is optimized in favor of cheaper service.
* Money spent on the network directly benefits users, rather than just serving to enrich large holders (stakers) or number crunchers (miners).
* The security mechanism involved ends up also solving the 51% attack.

## <div id="totc"> The Tragedy of The Commons </div>

![totc-comic.jpg](/totc-comic.jpg)

The Tragedy of the Commons (TOTC) occurs when a valuable, publicly-accessible resource (non-excludable good), is quickly depleted as competing or self-interested actors race to consume it. The classic example is a public field which farmers compete to freely feed their livestock until it is barren.

The comic above shows a more abstract version, where the quality of public air is degraded in order to increase production; the cost of a degradation in air quality is paid by everyone equally, rather than solely the polluters. When the air quality is so poor that people are too sick to work, the resource may be considered fully consumed.

Despite the fact that the depletion results in a situation where everyone collectively is worse off, each individual during the process has a rational incentive to continue consuming the resource, and to do so with greater effort than others. As with Free Riding, the classical solution to the problem is to relegate control over that consumption to a private interest.

### <div id="chainIncentiveTOTC"> Blockchain Incentives </div>

The Tragedy of The Commons in blockchain is more similar to the pollution example, since long-term storage burdens can be incurred on blockchain for a one-time price:

> <i>The tragedy-of-the-commons issue is created by the existence of the permanent ledger, which encourages nodes to accept payment today for work that can be offloaded to others tomorrow. This incentive leads to bloated blockchains and more subtly to transaction mis-pricing, as users can pay fees that do not reflect the true cost of their transaction to the overall network.</i>
> -[Saito Whitepaper](https://saito.io/saito-whitepaper.pdf)

There are a couple ways rational profit-seeking nodes will end up exploiting the storage commitments of more 'loyal' nodes. The first is a node which produces blocks, earns fees, but does not bother to validate or even hold historic transactions. For blockchains with large blocks, it may be costly for *anyone* to validate a block, and the job may end up pushed to just a few nodes who copy each other's work.

The second way long-term nodes can be exploited by short term interests is from nodes who come online during a surge of high demand in order to earn the fees of that surge. The massive influx of new transactions will pay the nodes as soon as they are added, and when the surge subsides, those nodes will take their profits and leave the data for everyone else to hold and maintain.

### <div id="outcomesTOTC"> Sub-optimal Outcomes </div>

The more subtle version of both of these issues is blockchain bloat: the network slowly accumulates data past what it can support without expenditure; when nodes begin spending more money on storage, it leads to *new* transactions paying the debt of storage incurred by the old ones.

Even if hardware storage prices continue to decrease, without a sound economic model to price blockchain storage, fees will either be higher than necessary or too low to support existing infrastructure. A true market solution will render lower user fees as storage costs decrease - not simply maintain some set level of efficiency.

Arweave is one project based entirely around storage, and which uses an economic model which attempts to predict the longterm price dynamics of digital storage. Not only will this lead to mismatches between the real cost of storage and the model's assumed cost, but if the model needs to ever be adjusted then it will again require developers making decisions about incentives and how node operators are paid.

<br>
<div style="display: flex; justify-content: center; width: 100%;">
 <figure style="width: 90%; margin: auto;">
    <img src="/arweave-storage-estimates.png" alt="Defining the Kryder+ Rate
In practice, the Arweave network utilizes a modification of the raw Kryder rate, which we will refer to as the Kryder+ rate in this document. The Kryder+ rate includes not just raw data storage, but also the other factors that are required in order to keep a network like Arweave online: replications, electricity, and operational costs. Each of these, we note, is affected by the same underlying decay in storage costs:
    Replications: Each new replica of the dataset inherits the same declining storage costs as the first.
    Power Usage: Changes in data density and reliability (the factors that most prominently effect the Kryder rate) are rarely, if ever, accompanied by increases in power usage. Subsequently, as storage mediums increase in capacity, the relative energy cost of storing a given quantity of data declines, too.
    Operational Expenses: As with power usage, as the efficiency of individual digital storage mediums increases, the number of devices needed to store a piece of data (and thus, the operational overhead to maintain them) declines.
In the present version of the Arweave network (2.5.3), 45 replicas of the dataset are targeted in the Kryder+ rate (defined here), along with a 2x storage overhead for operational and power expenses (see here)..">
   <figcaption style="opacity: 80%; text-align: center;"> Arweave makes broad estimates about storage cost into the future and uses those estimates to assume costs - from <a href="https://arwiki.wiki/#/en/endowment-simulation">ArWiki</a> </figcaption>
 </figure>
</div>

Arweave is not alone in relying on developers to attempt to predict storage costs for the chain. Most big-block chains make even less rigurous assumptions: namely, that since storage costs decrease over time that accurately pricing it isn't an issue. This is common in big-block forks of Bitcoin.

But even more ambitious chains at least do recognize that continually adding permanent data is not sustainable. The solution for them is to *not use the blockchain* - literally, their answer is to push transactions onto less secure and more centralized layers 2, 3 and above. Because it is assumed there are no solutions to deal with this problem on the layer 1, most smart contract chains believe that most data shouldn't enjoy the benefits of the layer 1.

And again, holding the uber conservative side of the spectrum is Bitcoin. Bitcoin hopes that by keeping blocks very small, any economic problems which occur out of a model which leads to a Tragedy of The Commons Problem will be insignificant. It's as if Bitcoin is saying - without a solution to this problem, we will not scale. Saito identifies the problem and poses a solution.

### <div id="solutionTOTC"> Saito's Solution to The Tragedy of The Commons </div>

In Saito, not only is the price of storage accurately adjusted automatically and in real-time, but transactions by default pay for the minimum amount of storage required, rather than paying for the maximum (forever). This is because transactions in Saito are allowed to expire after their epoch, but if they have a live balance, they must be rebroadcast into a fresh block such that the UTXO set only relies on blocks from the past, while also paying a fee.

<br>
<div style="display: flex; justify-content: center; width: 100%;">
 <figure style="width: 56%; margin: auto;">
    <img style="width: 100%;" src="/atr-v2.png" alt="A diagram showing Saito ATR mechanism in action in three steps.">
 </figure>
</div>
<br>

Hence the name: *Automatic Transcation Rebroadcasting* (ATR). Once any unspent transaction is *N* blocks old, it must be rebroadcast and will automatically pay a fee from its balance when it is. If the transaction does not have sufficient funds to pay the fee, then it is removed from storage and nodes are no longer responsible for it. The fee paid is a positive multiple of the average fee paid over the transactions lifespan.

This benefits users and full nodes equally. Because a node cannot produce a valid block without including all transactions which must be rebroadcast, a node cannot produce blocks until it *truly* becomes a full node and is holding the full UTXO set and the blocks which validate that set. This makes Data-Availability a default incentive for Saito.

Because full nodes are now paid for holding transactions, they do not care if data sticks around forever, because it will also pay them forever. On the flipside, users are no longer required to pay upfront fees which assume that data *will be around forver.* Because transactions can be removed, user fees only need to pay to add data - if it sticks around for rebroadcasting, it will pay for storage later.

This is a massive boon for use of the blockchain as a messaging layer. Posting data on any chain which does not have ATR means paying upfront for forever-storage costs. On Saito, transactions only need to pay for their first epoch when they are added, which means greatly reduced transaction fees and a greater ability to use the blockchain to transmit messages universally around the globe - making Saito an ideal PKI network.

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