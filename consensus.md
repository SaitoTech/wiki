---
title: Saito Consensus Mechanism
description: Consensus Mechanism
published: true
date: 2023-06-29T01:14:49.606Z
tags: 
editor: markdown
dateCreated: 2022-02-17T10:09:00.217Z
---

# Saito Consensus

This page offers a straight-forward description of how Saito Consensus works. Separate pages explaining how Saito eliminates common [attack vectors](/consensus/attack-vectors), a brief [math paper](/consensus/math) on cost-of-attack properties and [open proposals](/consensus/proposals) on technical implementation. You may also be interested in the [economic problems](/consensus/economics) Saito Consensus solves and [critical videos](/consensus/videos) covering the mechanism.

## 1. PRODUCING BLOCKS

When users send transactions into the network they add a cryptographic routing signature that specifies the first-hop node(s) to which they are sending their transaction(s). First-hop nodes add similar routing signatures as they propagate those transactions to their peers. Whichever version of the transaction is included in a block will have a chain of routing signatures unique to the path it took to reach the block producer.

The blockchain maintains a "difficulty" for block production that must be met by including a set amount of routing work in the block. Blocks which do not contain this amount of routing work are invalid according to consensus.

The amount of routing work in a block is the aggregate amount of "routing work" available for the block producer in each individual transaction in the block. This is calculated as the value of the transaction fee halved by each subsequent hop beyond the first that the transaction has taken to reach the block producer. Transactions without a valid routing path connecting the sender and block producer provide no routing work. It is also possible to simply specify that block producers may not include transactions that do not contain a valid routing path.

## 2. THE PAYMENT LOTTERY

When a block is produced all of the fees in the block are collected into a network treasury rather than paid out to block producers as is common in other designs. The following mechanism describes how to safely recover those fees and distribute them to participants in the network.

Each block contains a implicit proof-of-work challenge. When a block is produced miners start hashing to find a valid solution ("golden ticket"). This computational puzzle works similarly to that in Bitcoin, save that the mechanism is designed so that solutions cannot be forged or stolen in-transit.

If a golden ticket for block N is included in block N+1, the network issues two payouts: the first to the miner that found the solution and the second to a random node in the routing network. The amount of the mining payout is 50% of the fees included in the previous block. The amount of the router payout is 50% of the fees included in the previous block.

This process repeats block by block as Saito charges nodes (in burned fees) for the right to produce blocks and then again (in energy costs) for the right to unburn and distribute the payments.



## 3. SECURE ROUTER SELECTION

Saito Consensus rewards routing nodes based on their ability to propagate transactions towards successful block producers in as few hops as possible. A single transaction may take many paths throughout the network into the mempools of different nodes, and each hop diminishes the 'work' which is required for block production by half, starting with the base fee.

The winning routing node is selected using the hashing puzzle solution from the Golden Ticket which is required to release rewards. That number is used to select a transaction from the previous block with each transaction's chance of selection being proportional to its share of fees contributed to the block. The random number which selected the transaction is then hashed again to select a random node from the routing path of that transaction. Each node in the routing path has a chance of winning this proportional to its share of the aggregate routing work held by all members of that routing path.

The "Classic Saito" design targets a difficulty where the network can produce one golden ticket every two blocks on average and is secure at the cost of deflation from unsolved blocks.

Saito's routing reward scheme is [provably](https://github.com/SaitoTech/papers/blob/main/sybil/A_Simple_Proof_of_Sybil_Proof_Lancashire-Parris_2023.pdf) Sybil Proof - any routing node which self-clones to gain a larger share of routing-work for a given transaction also reduces by half the ability for that transaction to contribute towards the valid block production work threshold. In order to remain competitive for block production with a node at the same depth who chooses not to Sybil, the self-cloning node must produce their own transaction to supplement the reduced block work; the math works out that this strategy is strictly less profitable.

### Basic Proof of Sybil Proof

In each block, half the total fee reward $F$ is paid to routing nodes, and the other half split between staking UTXOs and the miner who discovered the solution which selects the winning router. The reward for the winning router is thus $F \over 2$.

The expected value for any given node is the value of the potential reward $F \over 2$ multiplied by the sum of probabilities that the node is selected in the routing path of the chosen transaction. 

The expected value is for any node $X$ is: 

$$ v(X) =\text{routing reward} \times \sum(\text{tx fee share} \times \text{tx routing work share})$$
Such that the sum enumerates over every transaction in the block. Transactions where a node has a routing work share of zero add zero expected value.

Consider a transaction pays $f$ fee, and is given to *node* $A$ who then propagates it to *node* $B$. If $B$ is honest, then he will not increase his share of routing work in the transaction by sending it to another address he controls - if $B$ Sybils, he will. The following demonstrates the expected returns of both $A$ and $B$ when $B$ is honest, then when decides to Sybil.

#### Non-Sybil (honest) Case

The respective shares of routing work each now possess as well as the total routing work of the transaction which $B$ holds are described below:

| Fee | $A$ routing work | $B$ routing work | Total Routing Work
---|---|---|---|
$f$ | $f$ | $f \over 2$ | $3f \over{2}$

For the block containing just the single transaction in the table above, the total fees equals $F = f$, thus the probability of that transaction being chosen is $f \over{F}$$=1$, and there is only a single term for each sum of probabilities. The routing reward is ${F \over 2} = {f \over 2}$.

The *expected values*, $v(X)$, are as follows:

For *node* $A$:

$$ v(A) = ({F \over 2}) ({f \over F}) ({f \div {3f \over 2}})  = ({F \over 2})( {2f \over 3f})  = {f \over 3}$$

And for *node* $B$:

$$ v(B) = ({F \over 2}) ({f \over F}) ({ {f\over2} \div {3f \over 2}})  = ({F \over 2})( {f \over 3f})  = {f \over 6}$$

If this behavior is repeated and the parameters do not change, *node* $A$ can expect to earn $f\over3$ while *node* $B$ can expect to earn $f\over 6$.

#### Sybil Case

If *node* $B$ decides to Sybil the transaction sent to him by *node* $A$, the respective and total shares of routing work are now described by:

| Fee | $A$ routing work | $B$ routing work | $B_2$ routing work | Total Routing Work
---|---|---|---|---|
$f$ | $f$ | $f \over 2$ | $f \over 4$ | $7f \over{4}$

Crucially, *node* $B$ has also diminished his block production ability by $f \over 2$. If $B$ wants to include  this Sybilled transaction which pays him more, he must supplement his block with the routing work he destroyed when adding an extra hop ($f \over 4$) - that block looks like this:

| Fee | $A$ routing work | $B$ routing work | $B_2$ routing work | Total Routing Work
---|---|---|---|---|
$f$ | $f$ | $f \over 2$ | $f \over 4$ | $7f \over{4}$
$f \over 4$ | 0 | $f \over 4$ | 0 | $f \over 4$

The total block reward is now $F = f + {f\over 4} = {5f \over 4}$ and the routing reward is ${F \over 2} = {5f \over 8}$. The expected value for *node* $A$ is now:

$$
\begin{align}
v(A) &= ({F \over 2}) \ \ [ \ (f \div {5f \over 4} ) (f \div {7f \over 4}) + ({f \over 4} \div {5f \over 4 }) ({0 \div {f \over 2} })\ ]\\
% & = ({5f \over 8}) \  [ \ (f \div {5f \over 4} ) (f \div {7f \over 4}) + 0 \ ]\\
& = ({5f \over 8}) \  [ \ ({4f \over 5f} ) ( {4f \over 7f}) + 0 \ ]\\
 v(A) &= ({5f \over 8}) ({4 \over 5} ) ({4 \over 7})  = {2f \over 7}\\
\end{align}
$$

*Node* $B$'s expected value must take into account $B$'s unique cost in the form of the fee *node* $B$ supplemented to remain competitive with block work $-{f \over 4}$. $B$'s expected value is now:

$$
\begin{align}
v(B) &= ({F \over 2}) \ \ [ \ (f \div {5f \over 4} ) (  ( {f \over 2} + {f \over 4} )  \div {7f \over 4}) + ({f \over 4} \div {5f \over 4 }) ({{f \over 2} \div {f \over 2} })\ ] - {f \over 4}\\
%& = ({5f \over 8}) \  [ \ ( f \div {5f \over 4} ) ( {f \over 4} \div {7f \over 4}) + 1 \ ] - {f \over 4}\\
& = ({\cancel{5}f \over 8}) \  [ \ ({4f \over \cancel{5}f} ) ( {3f \over 7f}) + {1 \over \cancel{5}} \ ] - {f \over 4}\\
 v(B) &= ({f \over 8})  ({12 \over 7} + 1 ) - {f \over 4} = ({f \over 8}) ({19 \over 7}) - {f \over 4} \\ 
 &= ({19f \over 56}) - {14f \over (14(4))} = {5f \over 56}
\end{align}
$$

#### Comparing Results

For the non-Sybil (honest; $v_h$) case:

$$ v_h(A) = {f \over 3} \ \ \ ;\ \ \  v_h(B) = {f \over 6}$$

$$ v_h(A) = 0.\bar3f \ \ \ ;\ \ \  v_h(B) = 0.1\bar6f$$

When $B$ Sybils ($v_s$):

$$ v_s(A) = {2f \over 7} \ \ \ ;\ \ \  v_s(B) = {5f \over 56}$$

$$ v_s(A) = 0.2857f \ \ \ ;\ \ \  v_s(B) = 0.0892f$$

If $B$ chooses to Sybil, his expected value drops almost by half. $A$ also loses marginal expected value by sending to Sybils, or equivalently, any node which adds unecessary extra hops. If $A$ sees that another node $C$ can include her transactions with the same success rate using less hops on average, $A$ is incentivized to stop sending to her peers which require more hops.

#### Where The Loss of Value Goes

Since the total expected value between nodes $A$ and $B$ has dropped when Sybilling occurs, it is a natural question: where does the extra money go? One can see that summing the expected values of the non-Sybil case results again in the total honest routing reward: ${f \over 3} + {f \over 6} = {f \over 2}$.

But summing the values for the Sybilling case has a deficit: ${2f(8) \over 7(8)}  + {5f \over 56} = {21f \over 56}$. So where does the remaining ${7f\over56} = {f \over 8}$ end up? It turns out  this is exactly the burn fee from the supplemental transaction the Sybilling node $B$ added with a fee of $f \over 4$. 

This additional burned fee ends up as a bonus to the mining and staking rewards (the expected value of miners and stakers), which make complimentary attacks on the Golden Ticket mechanism more expensive - attackers' wasted value goes towards security.





## 4. IMPROVING THE BASE MECHANISM

To prevent attackers gaming the lottery mechanism, we have consensus maintain a smoothed average of the fees included over the last epoch. In the event that the block reward is seriously in excess of this smoothed average (current target 1.25) the payment for both miner and router is capped at the target and the excess portion is burned for good.

To avoid deflation we introduce recursive payouts. Whenever a golden ticket is included in block N+1 we issue the payouts for block N as described above. If block N did not contain a golden ticket, we recurse to block N-1 and use our golden ticket to select a winning routing node for that black. This process can be repeated for all previously unpaid blocks, but it is preferable not to recurse more than two blocks back if difficulty is targeting 1 solution every 2 blocks.

Saito adds a payout to the UXTO holders in the network that is processed during the course of ATR processing (see below). This payout is funded by fees intended for the "mining payout" which is left uncollected in recursive block payouts described above.

## 5. AUTOMATIC TRANSACTION REBROADCASTING (ATR)

Saito divides the blockchain into "epochs" of N blocks. If the latest block is 500,000 and N is 100,000 blocks, then the current epoch streches from block 400,001 onwards.

Once a block falls out of the current epoch, its unspent transaction outputs (UTXO) are invalid by consensus rules. Any UTXO from that block which meet rebroadcast criteria must be re-included by the producer of the next block in the form of an "automatic transaction rebroadcasting" (ATR) transaction. These ATR transactions include the original transaction as embedded data, but provide new UTXO spendable by the original address.

The criteria for rebroadcasting is not only that the UTXO is still unspent, but that the UTXO itself contains enough tokens to pay a rebroadcasting fee. This rebroadcasting fee should be equal to or greater than the average fee per byte paid by new transactions over the previous epoch. The UTXO may also be issued a payout as described in the section above, where the earnings are proportional to the UTXO's share of the unspent tokens circulating around the blockchain.

The new UTXO may be greater to or less than the value of the previous UTXO, with the exact balance determined by market forces rather than hardcoded by developers. In addition to the economic and security benefits of the ATR payout, we note that permanent data storage becomes possible through this mechanism.

## 6. ADVANCED SAITO

Additional mechanisms that increase network robustness include: 

Creating wrap-around spam resistance to block flooding attacks by requiring all valid chains to contain N golden tickets over the last M blocks, such that forks are considered invalid unless they meet minimal hashing conditions.

Routing and congestion policies which leverage block-level signatures and allow nodes to police their peers to ensure that their peers are following sensible routing policies and not spamming the network or relaying malicious blocks.

Requirements for block producers to provide stake (making tokens unspendable for X blocks) when producing blocks, increasing the cost of some kinds of work-reuse and spamming attacks. Slashing these locked-up tokens is possible in some situations if the same tokens are staked for blocks within a set depth of each other.


### APPENDIX I: SAITO TERMINOLOGY

**Paysplit:** a variable between 0 and 1 that determines the percentage of the block reward that is allocated to mining nodes.

**Powsplit:** a variable between 0 and 1 that determines the target percentage of blocks solved through golden tickets.

**Golden Ticket:** a transaction from a miner containing a valid solution to the computational lottery puzzle embodied in the previous block hash.

**Genesis Period:** the length of the epoch in number of blocks.




