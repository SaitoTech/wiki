---
title: Saito Consensus - Broadcast Strategy and Messaging Costs
description: 
published: true
date: 2025-12-03T16:50:07.336Z
tags: 
editor: markdown
dateCreated: 2025-12-03T07:25:55.513Z
---

# Saito Economics Note

The puzzle is straightforward: if agents can freely misreport preferences in an informationally decentralized mechanism, incentive compatibility should be impossible and no mechanism should implement efficient outcomes. Yet Saito Consensus does exactly this. How?

## Section 1: The Impossibility Results

The impossibility results that dominate implementation theory rest on a specific modeling assumption: that agents do not face higher costs for sending messages that induce deviations from welfare-optimal outcomes.

This assumption became entrenched early. Hurwicz (1972) treated all statements as equally cheap to express; Maskin then abstracted communication costs entirely; and Myerson’s Revelation Principle pushed the field toward studying direct mechanisms in which type reports are the only messages and are costless by construction. The standard framework thus only recognizes mechanisms compatible with Myerson–Maskin symmetry, creating a powerful blind spot.

The same assumption appears across foundational results in economics and computer science. Myerson–Satterthwaite assumes agents can misreport without penalty; Crawford–Sobel models all messages as costless and commitment-free; and distributed-systems impossibility results such as Bracha–Toueg treat all proposals as equally feasible. In all of these settings, messages carry no commitments, impose no costs, and do not affect continuation payoffs.

Yet there is nothing in decentralization that requires communication to be costless. And Saito's design shows it is possible to break this assumption by adding endogenous message costs that rise with the suboptimality of the message being shared. The next section explains how this is accomplished in theory.


## Section 2: Endogenous Costs

Implementing endogenous messaging costs requires three properties: (i) messaging choices must affect agent utility within the mechanism, (ii) the mechanism must observe the choices they make, and (iii) the mechanism must adjust the **continuation value** for each agent on they choices they make. Saito accomplishes this using three components:

(a) Portfolio Bids

Agents may cooperate by assembling portfolio bids -- bundles that combine multiple proposals into a single submission that competes with individual bids. Cooperation increases utility by improving the competitiveness of the joint bid, giving agents an incentive to share proposals prior to submission.

(b) Cryptographic Routing Signatures

The sharing of proposals is made visible through the use of cryptographic routing signatures which add a routing path to proposals. The chain-of-signatures make pre-submission sharing visible to the mechanism, recording who forwarded the proposal and who received it in what order.

(c) Routing Payouts / Conditional Refunds

The mechanism finally adjusts utility based on these signatures. In addition to portfolio bids having an advantage in the Dutch-clock clearing rule, a portion of the succesful bid is awarded to one participant drawn from the routing paths of the winning bid, creating an outbound payment that serves as **continuation value** for future rounds of the mechanism.

These technical components form our causal chain: portfolio bids make cooperation valuable, routing signatures make it observable, and routing payouts convert that observability into continuation value. 


## Section 3: Broadcast Strategies

Broadcast Strategies within the mechanism now permit agents to trade-off **continuation value** for other forms of utility:

- **forwarding changes payoff odds:** any transfer affecting the number of agents identifiable in any routing path changes the expected profitability of all participants, and cedes some probability of receiving the conditional refund from the sender to the receiver.

- **forwarding changes the utility bundle:** cooperation not only affects speed-of-settlment, but allows participants to engage in side-deals in exchange for bid-flow, such as extending additional private benefits ("collusion goods") in exchange for exclusive access to proposals.

- **forwarding changes the degree of competition:** the decision to share exclusively with one peer or broadcast to multiple peers affects the expected profitability of the recipients and thus their own broadcast strategies.

The message space is no longer symmetric. A three directional trade-off / trilemma is pulled into being that allows agents to trade their **continuation value** for other forms of utility. There is not only a cost paid for messaging, but it is paid in terms of the other forms of utility available through the mechanism.

### 3.3 Mechanism Overview (informal specification)

Now that we have described why the mechanism works in theory, we provide a brief informal specification of how such a mechanism can be implemented in practice.

Our mechanism manages the allocation of a potentially divisible good (blockspace) whose availability is determined endogenously each round. Agents submit proposals (transactions) that specify a non-scalar fee and which may be combined with other transactions into portfolio bids. These proposals move through a decentralized network, and the manner in which they are forwarded and bundled determines (i) the competitiveness of the resulting portfolio bid and its likelihood of successful allocation and (ii) each participant's expected claim on a conditional refund that provides continuation value.

The mechanism operates through the following components:

**1. Proposals and Utility Composition**

- Each agent submits a proposal containing a transaction with a non-scalar fee.

- Fees map into three components of utility: allocation of the divisible blockspace good (A), expected speed-of-settlement or time preference (B), and the potential for side-payments or collusion-utility (C).

- Proposals may be forwarded or submitted directly. Forwarding is optional but strategically relevant.

**2. Routing Signatures and Observable Cooperation**

- When a proposal is forwarded, the forwarding agent appends the receiver’s identity and a cryptographic authorization signature.

- The resulting routing path is immutable: nodes cannot remove or shorten paths without invalidating their ability to act upon the shared proposal.

**3. Portfolio Bids**

- Any agent may submit its own proposal as an individual bid or assemble multiple proposals into a portfolio bid.

- Portfolio bids aggregate the bid value of their constituent proposals and may include both genuine transactions and agent-generated placeholder proposals.

- The mechanism imposes no restrictions on which proposals can be bundled together, except that the submitting agent always appears as the final entry on the routing path for any proposal it submits, and once proposals have been accepted other variants cannot be accepted as the funds used in the bid are considered spent.

**4. Clearing Rule via a Dutch Clock**

- The mechanism maintains an endogenous “difficulty” or burn fee that adjusts to target a desired block production interval.

- A candidate bundle (individual or portfolio) clears when the cumulative “routing work” it contains exceeds the current difficulty threshold.

- Routing work is computed as the fee of each proposal, halved once per hop beyond the first in its routing path, and aggregated across all proposals in the bundle.

- Faster clearing requires higher cumulative fees or more efficient cooperation; ineffective cooperation increases the routing-work discount.

**5. Conditional Refund and Continuation Value**

- In each successfully cleared bundle, 50% of all proposal fees are destroyed, and 50% form a conditional refund pool.

- A costly lottery selects one proposal, weighted by its fee’s contribution to the bundle, and then selects one participant from that proposal’s routing path, with each weighted by their proportional contribution to the proposal’s cumulative routing work.

- The selected participant receives the entire conditional refund.

**6. Validity, Observability, and Permissionlessness**

- The mechanism observes the full routing path of every proposal and the full composition of every portfolio bid.

- Invalid or inconsistent routing paths render both the proposal and any bundle containing it invalid.

- A simple longest-chain rule selects among competing bundles.

## Section 4. The Rationality of Efficient Implementation

The mechanics described in Section 3 do more than eliminate the possibility of “cheap talk” reports required by conventional impossibility results. They also make proposals that are consistent with welfare-efficient allocations uniquely attractive to participants.

To understand why, we define a welfare-increasing trade as any reallocation among Goods A, B, and C that strictly increases an agent’s utility according to their own preferences. We then show that all profitable deviations within the mechanism must take the form of a cooperative portfolio bid. We offer this argument as a series of lemmas leading to a general result:

For clarity, 

**Lemma 1. All welfare-increasing trades require cooperation and therefore continuation-value sacrifice.**

Under the clearing rules of the mechanism, unilateral deviations cannot improve an agent’s allocation of A or B. Any welfare-increasing deviation must therefore involve participation in a portfolio bid, which necessarily expands or modifies the routing path. This expansion dilutes the agent’s continuation value, defined as the expected future purchasing power derived from refund eligibility. Every welfare-increasing trade thus carries a built-in continuation-value cost that the agent must accept in order to receive the immediate benefit.

**Lemma 2. Profitable deviations must be welfare-increasing trades.**

Because deviations necessarily sacrifice some dimension of utility-in-mechanism, no agent can strictly improve their payoff without engaging in a subjective welfare-increasing trade across Goods A (blockspace), B (time preference), and C (collusion-utility). A deviation is profitable if and only if the agent values the marginal gain (e.g., the collusion utility secured from private broadcast) more than the marginal loss in the other goods (e.g., slower settlement). Thus any profitable deviation must correspond to a genuine welfare-increasing trade from the agent’s perspective.

**Lemma 3. Continuation-value losses exceed gains for all non-efficient deviations.**

Continuation value represents an agent’s ability to purchase any mix of A, B, and C in future rounds of the iterating auction. Routing-work dilution reduces this continuation value proportionally. As a result, any deviation that does not create a genuine welfare improvement imposes a strict net loss: the reduction in continuation value outweighs any short-term benefit gained from the deviation. Such deviations are irrational in intertemporal expectation.

**Theorem. Pareto-Sufficient Efficient Implementation.**

Given the mechanism’s fixed rules, observability of routing paths, and common-knowledge continuation-value incentives, the only deviations consistent with intertemporal optimization are those that correspond to genuine welfare-increasing trades. All other deviations collapse under the weight of their continuation-value losses. Hence the mechanism implements an allocation that is Pareto-sufficient: efficient given the topological structure of communication within the mechanism, rational agents converge to proposals consistent with the welfare-efficient allocation, even under informational decentralization.

NOTE: efficiency can be improved from the *Pareto sufficient* baseline if agents use the opportunity to publish information on their pricing and availability of collusion goods via the inclusion of proposals as a form of price broadcasting.

For an intuitive understanding of how optimization is possible, note that because cooperation improves current utility but reduces continuation value, rational agents must balance **short-term gains** in Goods A, Good B, and Good C. against **long-term losses** in their ability to purchase those same goods in the future.

In other mechanisms this trade-off becomes insolvable because there is no way to optimize consumption across multiple time-frames. But with routing work long-term time-preference can be manipulated directly within the mechanism through the trade-offs portfolio bids allow agents to construct between Good A and Good C.

Granular forms of optimization are possible because agents who trade Good B for Good A or Good C, are delaying their consumption of utility in the same way that they would by collecting a refund for use in a later round in the iterating auction. Trade-offs between all goods become possible to optimize within the current bid or within the iterated game. In this environment, portfolio bids that maximize expected welfare survive; since optimizing within each round of the auction is equivalent in expectation to optimizing across multiple rounds.

## Section 5. Stability Through Incentives

The most beneficial strategy for all participants is to maximize the gains available from cooperating with other agents while minimizing the losses that the need to cooperate forces on them.

When all agents follow this strategy:

- welfare-increasing trades propagate forward,

- inefficient deviations collapse,

- and the mechanism drives short-term and long-term time preference into equilibrium.

The outcome that remains is the one in which all agents forward and adopt proposals consistent with the welfare-efficient allocation. Efficiency emerges not by assumption or revelation, but because the mechanism embeds the incentive gradient needed to restrict profitable deviations exclusively to genuine welfare improvements.

