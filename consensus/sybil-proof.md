---
title: Sybil-Proof
description: 
published: true
date: 2023-09-24T00:33:17.625Z
tags: 
editor: markdown
dateCreated: 2023-09-12T04:54:16.592Z
---

## Proof of *Sybil-Proof*

- Read [*A Simple Proof of Sybil Proof.*](https://github.com/SaitoTech/papers/blob/main/sybil/A_Simple_Proof_of_Sybil_Proof_Lancashire-Parris_2023.pdf) for a complete and formal proof.

- Learn about [Sybils](https://wiki.saito.io/en/consensus/sybils) and how they damage permisionless networks.

> A sybil produces the block with w/ 2nd hop routing work. A non-sybil produces the block faster with 1st hop routing work. The probability of the sybil collecting payment is lower because the probability of their blocks being added to the chain is lower. <br><br>The only way a sybil can reach parity on probability is if they burn their own money, which puts their cost higher than the non-sybil. There is simply no world in which the probability of getting paid is the same for a sybil as a non-sybil ceteris paribus.
<br>-David Lancashire

As argued in *On Bitcoin and Red Ballons* [[Babaioff et al., 201]](https://arxiv.org/abs/1111.2626) the Sybil problem widely agreed to be unsolvable, since giving other block producers access to transaction fees always gives them an advantage, and allowing arbitrary claims on fees allows Sybils to earn multiple, unwarranted rewards for fake relays.

This poses a problem for blockchain networks which wish to remain open and secure against converging power at scale. If, as argued by experts in the field, Sybilling on transaction propagation is impossible to defend against, blockchain networks are doomed to fall into patterns of hoarding which reward the largest nodes in the network and introduce economic problems as they shelter transactions rather than share them - even if sharing would increase overall efficiency.

Saito proves that by reducing the work available to produce blocks with each 'hop' in a transaction's relay path, that Sybil nodes and nodes who otherwise add unnecessary 'hops' on their way to block producers are less profitable and out-compete by nodes who only add hops to reduce propagation time to block producers. The mechanism and basic mathematics of the proof are demonstrated below.

### SECURE ROUTER SELECTION

Saito Consensus rewards routing nodes based on their ability to propagate transactions towards successful block producers in as few hops as possible. A single transaction may take many paths throughout the network into the mempools of different nodes, and each hop diminishes the 'work' which is required for block production by half, starting with the base fee.

The winning routing node is selected using the hashing puzzle solution from the Golden Ticket which is required to release rewards. That number is used to select a transaction from the previous block with each transaction's chance of selection being proportional to its share of fees contributed to the block. The random number which selected the transaction is then hashed again to select a random node from the routing path of that transaction. Each node in the routing path has a chance of winning this proportional to its share of the aggregate routing work held by all members of that routing path.

The "Classic Saito" design targets a difficulty where the network can produce one golden ticket every two blocks on average and is secure at the cost of deflation from unsolved blocks.

Saito's routing reward scheme is [provably](https://github.com/SaitoTech/papers/blob/main/sybil/A_Simple_Proof_of_Sybil_Proof_Lancashire-Parris_2023.pdf) Sybil Proof, as any routing node which self-clones to gain a larger share of routing-work for a given transaction also reduces by half the ability for that transaction to contribute towards the valid block production work threshold. In order to remain competitive for block production with a node at the same depth who chooses not to Sybil, the self-cloning node must produce their own transaction to supplement the reduced block work; the math works out that this strategy is less profitable.

### Basic Proof of Sybil Proof

In each block, half the total fee reward $F$ is paid to routing nodes, and the other half split between staking UTXOs and the miner who discovered the solution which selects the winning router. The reward for the winning router is thus $F \over 2$. Note that this "playsplit" of half-and-half is not necessarily required, but is the standard parameter.

The expected value for a routing node is the value of the potential routing reward $F \over 2$ multiplied by the sum of probabilities that the node is selected in the routing path of the selected transaction; these selections are determined at random weighted by routing work.

The expected value is for any node $X$ is: 

$$ v(X) =\text{routing reward} \times \sum(\text{tx fee share} \times \text{tx routing work share})$$

The chance that a transaction from the block is the $\text{tx routing share}$, which is the value of the fee in that transaction proportional to the total fees paid in the block. Each router for the chosen transaction has a chance proportional to their routing work in the transaction's relay-path to win the $\text{routing reward}$.

The sum considers every transaction in the block. Transactions where a node has a routing work share of zero add zero expected value.

Consider a transaction pays $f$ fee, and is given to *node* $A$ who then propagates it to *node* $B$. If $B$ Sybils, then he will increase his share of routing work in the transaction by marking it with an additional address he controls - if $B$ is honest, he will not. Note that by adding an extra signature to the routing-chain, $B$ claims more of its reward without further propagation the transaction.

The following demonstrates the expected returns of both $A$ and $B$ when $B$ is honest, then when $B$ decides to Sybil:

#### Non-Sybil (honest) Case

$A$ and $B$'s respective shares of routing work as well as the total routing work of the transaction which $B$ holds (total) are described below. 

Note that $A$ is free at any time to produce a block with the version of the transaction without including $B$ and keep $f \over f$, 100%, of the work, but if $B$ wants to produce a block, he only has access to it such that $A$ is in the routing path and thus must share the work.

| Fee | $A$ routing work | $B$ routing work | Total Routing Work
---|---|---|---|
$f$ | $f \longrightarrow$ | $f \over 2$ | $3f \over{2}$

For the block containing just the single transaction in the table above, the total fees equals $F = f$, thus the probability of that transaction being chosen is $f \over{F}$$=1$, and there is only a single term for each sum of probabilities. The routing reward is ${F \over 2} = {f \over 2}$.

The *expected values* in the honest case, $v_h(X)$, are as follows:

For *node* $A$:

$$ v(A)_h = ({F \over 2}) ({f \over F}) ({f \div {3f \over 2}})  = ({F \over 2})( {2f \over 3f})  = {f \over 3}$$

And for *node* $B$:

$$ v(B)_h = ({F \over 2}) ({f \over F}) ({ {f\over2} \div {3f \over 2}})  = ({F \over 2})( {f \over 3f})  = {f \over 6}$$

If this behavior is repeated and the parameters do not change, *node* $A$ can expect to earn $f\over3$ while *node* $B$ can expect to earn $f\over 6$.

#### Sybil Case

If *node* $B$ decides to Sybil the transaction sent to him by *node* $A$, the respective and total shares of routing work are now described by:

| Fee | $A$ routing work | $B$ routing work | $B_2$ routing work | Total Routing Work
---|---|---|---|---|
$f$ | $f \longrightarrow$ | ${f \over 2} \longrightarrow$ | ${f \over 4}$ | $7f \over{4}$

Crucially, *node* $B$ has also diminished his block production ability from $f \over 2$ to $f \over 4$. If $B$ wants to include  this Sybilled transaction which pays him more, he must supplement his block with the routing work he destroyed when adding a hop ($f \over 4$) - that block looks like this:

| Fee | $A$ routing work | $B$ routing work | $B_2$ routing work | Total Routing Work
---|---|---|---|---|
$f$ | $f \longrightarrow$ | ${f \over 2} \longrightarrow$ | ${f \over 4}$ | $7f \over{4}$
$f \over 4$ | 0 | $f \over 4$ | 0 | $f \over 4$

The total block reward is now $F = f + {f\over 4} = {5f \over 4}$ and so the routing reward is ${F \over 2} = {5f \over 8}$. In the *Sybil* case, the expected values $v_s(X)$ are:

$$
v_s(A) = ({F \over 2}) ( (f \div {5f \over 4} ) (f \div {7f \over 4}) + ({f \over 4} \div {5f \over 4 }) ({0 \div {f \over 2} }) )
$$

$$
= ({5f \over 8}) ( ({4f \over 5f} ) ( {4f \over 7f}) + 0 )
$$

$$
v_s(A) = ({5f \over 8}) ({4 \over 5} ) ({4 \over 7})  = {2f \over 7}\\
$$



*Node* $B$'s expected value must take into account $B$'s unique cost in the form of the fee *node* $B$ supplemented to remain competitive with block work $-{f \over 4}$. $B$'s expected value after Sybilling is now:

$$
v_s(B) = ({F \over 2}) ( \ (f \div {5f \over 4} ) (  ( {f \over 2} + {f \over 4} )  \div {7f \over 4}) + ({f \over 4} \div {5f \over 4 }) ({{f \over 2} \div {f \over 2} })\ ) - {f \over 4}
$$

$$
= ({5f \over 8})   ( ({4f \over 5f} ) ( {3f \over 7f}) + {1 \over 5} ) - {f \over 4}
$$

$$
= ({f \over 8})  ({12 \over 7} + 1 ) - {f \over 4} = ({f \over 8}) ({19 \over 7}) - {f \over 4}
$$

$$
v(B)_x = ({19f \over 56}) - {14f \over (14(4))} = {5f \over 56}
$$


#### Comparing Results

For the non-Sybil (honest; $v_h$) case:

$$ v_h(A) = {f \over 3} \ \ \ ;\ \ \  v_h(B) = {f \over 6}$$

$$ v_h(A) = 0.\bar3f \ \ \ ;\ \ \  v_h(B) = 0.1\bar6f$$

When $B$ Sybils ($v_s$):

$$ v_s(A) = {2f \over 7} \ \ \ ;\ \ \  v_s(B) = {5f \over 56}$$

$$ v_s(A) = 0.2857f \ \ \ ;\ \ \  v_s(B) = 0.0892f$$

If $B$ chooses to Sybil, his expected value drops almost by half. $A$ also loses marginal expected value by sending to Sybils, or equivalently, any node which adds unecessary extra hops. If $A$ sees that another node $C$ can include her transactions in successful blocks at the same rate while using less hops, $A$ is incentivized to stop sending to her peers which require more hops;  the network in general sheds extractive agents offering sub-optimal routing utility.

#### Where The Loss of Value Goes

One can see that summing the expected values of the non-Sybil case results again in the total honest routing reward: ${f \over 3} + {f \over 6} = {f \over 2}$. But summing the values for the Sybilling case has a deficit: ${2f(8) \over 7(8)}  + {5f \over 56} = {21f \over 56}$. So where does the remaining ${7f\over56} = {f \over 8}$ end up?

It turns out  this is exactly the quantity of burn fee from the supplemental transaction the Sybilling node $B$ added with a fee of $f \over 4$, that is, the half of each fee which pays Golden Ticket rewards.

This additional burned fee ends up as a bonus to the mining and staking rewards (as expected value for miners and stakers), which make complimentary attacks on the Golden Ticket mechanism more expensive - routing attackers' wasted value enhances re-org security.

### Are Sybils Really Identified?

One common objection to the the claim that Saito's router reward scheme is Sybil Proof is to notice that it cannot tell the difference between Sybils adding an extra hop to extract value and honest nodes performing sub-optimally. Saito is secure against Sybils, however, precisely because it is able to identify their behavior as a generalized  form of sub-optimal routing outcomes.

This in fact makes Saito's defense against extractive behavior stronger than if it was specifically Sybil Proof, as sub-optimal outcomes which it is secure against *includes* Sybils.

* The fact that Sybils fall under a broader category of behavior in Saito than simply self-cloning does not prevent Sybils from being punished and driven out.

* This broader category of behaviors punishes sub-optimal outcomes more generally. Sybils and non-competitive nodes both extract reward without a similar provision of resources for the network.

Saito's reward scheme, more generally, is *proofed* against sub-optimal routing behavior in favor of efficient routing and block production. Sybils may not be distinct from non-competitive nodes, but as neither can extract undue rewards (and neither is desirable for an economically scalable and sustainable network), the network has security against both.


