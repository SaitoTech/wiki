---
title: Saito Consensus - Broadcast Strategy and Messaging Costs
description: 
published: true
date: 2025-12-04T00:06:38.003Z
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

Broadcast strategies now permit agents to trade off **continuation value** against other forms of utility inside the mechanism:

 - **Forwarding redistributes continuation value:** any change to a routing path alters each participant’s probability of receiving the conditional refund, transferring continuation value from the sender to the receiver.

 - **Forwarding alters competitive conditions:** sharing with one peer versus broadcasting to many changes the recipients’ expected payoff and their willingness to provide collusion goods (Good C).

 - **Public broadcast trades continuation value for faster inclusion:** routing a proposal to multiple recipients induces them to forward-propagate to raise their own refund share, increasing competition and improving the sender’s allocation in Good A (settlement speed).

 - **Private broadcast trades inclusion speed for collusion goods:** routing exclusively to a single peer reduces competitive pressure for fast inclusion, increasing that peer’s expected profitability and enabling exclusive side-payments (Good C).

These dynamics create a three-way trade-off among Goods A, B, and C. Every messaging choice imposes a real cost which may be assigned to whichever dimension of utility the bidder values least at the margin. The message space is therefore no longer symmetric.


## Section 4. Welfare Efficient Outcomes

The mechanics described in Section 3 make proposals that are consistent with welfare-efficient allocations uniquely attractive to participants. In review:

**Lemma 1. All welfare-increasing trades require cooperation and therefore continuation-value sacrifice.**

A welfare-increasing trade is any reallocation among Goods A, B, and C that strictly increases an agent’s utility given their private preferences.

Under the clearing rules of the mechanism, unilateral deviations cannot improve an agent’s allocation of A or B and C (collusion goods) are unavailable. Any welfare-increasing deviation must therefore involve participation in a portfolio bid, which necessarily expands the routing path, reducing the bidder's expected claim on the routing payout / refund. Every welfare-increasing trade thus carries a built-in continuation-value cost that the agent must accept in order to receive the immediate benefit.

**Lemma 2. Profitable deviations must be welfare-increasing trades.**

Because all deviations sacrifice some dimension of utility-in-mechanism, no agent can strictly improve their payoff without engaging in a subjective welfare-increasing trade across Goods A (blockspace), B (time preference), and C (collusion-utility). A deviation is profitable if and only if the agent values the marginal gain (e.g., the collusion utility secured from private broadcast) more than the marginal loss (e.g., slower settlement from limited competition). Thus any profitable deviation must be a genuine welfare-increasing trade from the agent’s perspective.

**Lemma 3. Continuation-value losses exceed gains for all non-efficient deviations.**

Given that **continuation value** represents an agent’s ability to purchase any mix of A, B, and C in future rounds, any deviation that does not create a genuine welfare improvement imposes a strict net loss: the reduction in continuation value outweighs any short-term benefit gained from the deviation. Such deviations are irrational in intertemporal expectation.

**Theorem: Pareto-Sufficiency**

Given the mechanism’s fixed rules, observability of routing paths, and common-knowledge continuation-value incentives, the only deviations consistent with intertemporal optimization are those that correspond to genuine welfare-increasing trades. All other deviations collapse under the weight of their continuation-value losses. Hence the mechanism implements an allocation that is Pareto-sufficient: efficient given the topological structure of communication within the mechanism. Rational agents converge to proposals consistent with the welfare-efficient allocation, even under informational decentralization.


## Section 5. Conclusion

The most beneficial strategy for all participants is to maximize the gains available from cooperation with others while minimizing the losses that the need to cooperate forces on them.

When all agents follow this strategy, the longest-chain strategy ensures the most efficiently compiled (lowest in continuation loss) bundle of proposals re-inforce each other:

- welfare-increasing trades propagate forward,

- inefficient deviations collapse,

- and the mechanism drives short-term and long-term preferences into equilibrium.

The outcome that remains is the one in which all agents emergently adopt strategies consistent with the welfare-efficient allocation. Efficiency emerges not by assumption or revelation, but because the mechanism embeds the incentive gradient needed to restrict profitable deviations exclusively to genuine welfare improvements.


# Appendix - Implementation Specification

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