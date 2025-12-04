---
title: Saito Consensus - Broadcast Strategy and Messaging Costs
description: 
published: true
date: 2025-12-04T07:03:12.425Z
tags: 
editor: markdown
dateCreated: 2025-12-03T07:25:55.513Z
---

# Saito Economics Note

The puzzle is straightforward: if agents can freely misreport preferences in an informationally decentralized mechanism, incentive compatibility should be impossible and no mechanism should implement efficient outcomes. Yet Saito Consensus does exactly this. How?

## Section 1: The Impossibility Results

The impossibility results that dominate implementation theory rest on a specific modeling assumption: that agents do not face higher costs for sending messages that induce deviations from welfare-optimal outcomes.

This assumption became entrenched early. Hurwicz (1972) treated all statements as equally cheap to express; Maskin then abstracted communication costs entirely; and Myerson’s Revelation Principle pushed the field toward studying direct mechanisms in which type reports are the only messages and are costless by construction. The standard framework evolved to analyze mechanisms compatible with Myerson–Maskin symmetry, creating a powerful blind spot.

Other foundational results in economics and computer science have consequently reinforced the assumption. Myerson–Satterthwaite assumes agents can misreport without penalty; Crawford–Sobel models all messages as costless and commitment-free; and distributed-systems impossibility results such as Bracha–Toueg treat all proposals as equally feasible. In each of these settings, messages carry no commitments, impose no costs, and do not affect continuation payoffs.

Yet there is nothing in decentralization that requires communication to be costless. And Saito shows how to break this assumption: by adding endogenous message costs that rise with the suboptimality of the message being shared. The next section explains how these endogenous costs can be created.

## Section 2: Endogenous Costs

Implementing endogenous messaging costs requires three properties: (i) messaging choices must affect agent utility within the mechanism, (ii) the mechanism must observe the choices agents make, and (iii) the mechanism must adjust the **continuation value** for each agent dependent on they choices they make. Saito implements this in three steps:

(a) Portfolio Bids

Agents may cooperate by assembling portfolio bids -- bundles that combine multiple proposals into a joint submission that competes with individual bids. Cooperation increases utility by improving the competitiveness of the joint bid, giving agents an incentive to share proposals prior to submission.

(b) Cryptographic Routing Signatures

The sharing of proposals is made visible through the use of cryptographic routing signatures. The chain-of-signatures created by pre-submission sharing becomes visible to the mechanism in the resulting routing path, which records who forwarded which proposal to whom and who received it in what order.

(c) Routing Payouts / Conditional Refunds

The mechanism finally adjusts utility based on these signatures, awarding a portion of the succesful bid to one participant drawn from the routing paths of the winning submission, creating an outbound payment that serves as **continuation value** for future rounds of the mechanism.

These technical components form our causal chain: portfolio bids make cooperation valuable, routing signatures make it observable, and routing payouts convert that observability into a form of continuation value allocated by the mechanism.


## Section 3: Broadcast Strategies

Because every additional hop in a routing path adds another potential claimant to the conditional refund, sharing a proposal with any peer necessarily imposes a cost; it reduces the sender’s **continuation value**. Rational senders will only accept this loss if cooperating increases their utility in a more highly-valued dimension: blockspace allocation (A), settlement speed (B), or collusion utility (C) in the classic mechanism.

Broadcast strategy is the mechanism by which agents accomplish this. By choosing how widely or narrowly a proposal is distributed, agents shape the competitive environment in which portfolio bids are assembled and thereby influence both (i) the probability of fast inclusion and (ii) the expected profitability of message recipients.

Two strategies are available which optimize for different forms of utility, namely:

- **Public broadcast:** trades continuation value for faster inclusion (Good B). Routing a proposal to multiple recipients increases competition between them to include it in a portfolio bid. This gives each recipient an incentive to forward-propagate the proposal to secure a position in the routing path of the eventual winner, accelerating settlement for the sender.

- **Private broadcast:** trades continuation value for collusion utility (Good C) or increased blockspace (Good A). Routing exclusively to a single recipient minimizes competitive pressure, giving the recipient a larger expected claim on the conditional refund and enabling them to convert a portion into a private benefit offered in return for the sender.

These dynamics permit three-way trade-offs between Goods A, B, and C. This breaks the symmetry of the message space: every forwarding decision imposes a real cost, which agents justify by pursuing whichever dimension of utility yields the highest marginal gain.

This implies that any profitable deviation must involve a deliberate trade of continuation value for Good A, Good B, or Good C. We now formalize this by characterizing which deviations are feasible, which are genuinely welfare-improving, and how continuation-value losses restrict all others.


## Section 4. Welfare Efficient Outcomes

The mechanics described in Section 3 make proposals that are consistent with welfare-efficient allocations uniquely attractive to participants. In review:

**Lemma 1. All welfare-increasing trades require cooperation and therefore sacrifice continuation value.**

A welfare-increasing trade is any reallocation among Goods A, B, and C that strictly increases an agent’s utility given their private preferences.

Under the clearing rules of the mechanism, non-portfolio bids cannot adjust an agent’s allocation of A or B, while C (collusion goods) are unavailable. Any welfare-increasing deviation must therefore involve participation in a portfolio bid, which necessarily expands the routing path, reducing the bidder's expected claim on the routing payout / refund. Every welfare-increasing trade thus carries a built-in continuation-value cost that the agent must accept in order to receive the immediate benefit.

**Lemma 2. Profitable deviations must be welfare-increasing trades.**

Because all deviations sacrifice some dimension of utility-in-mechanism, no agent can strictly improve their payoff without engaging in a subjective welfare-increasing trade across Goods A (blockspace), B (time preference), and C (collusion-utility). A deviation is profitable if and only if the agent values the marginal gain (e.g., the collusion utility secured from private broadcast) more than the marginal loss. Thus any profitable deviation must be a genuine welfare-increasing trade from the agent’s perspective.

**Lemma 3. Continuation-value losses exceed gains for all non-efficient deviations.**

Given that **continuation value** represents an agent’s ability to purchase any mix of A, B, and C in future rounds, any deviation that does not create a genuine welfare improvement imposes a strict net loss: the reduction in continuation value outweighs any short-term benefit gained from the deviation. Such deviations are irrational in intertemporal expectation.

**Theorem: Pareto-Sufficiency**

Given the mechanism’s fixed rules, observability of routing paths, and common-knowledge continuation-value incentives, the only deviations consistent with intertemporal optimization are those that correspond to genuine welfare-increasing trades. All other deviations collapse under the weight of their continuation-value losses. Hence the mechanism implements an allocation that is Pareto-sufficient: efficient given the topological structure of communication within the mechanism. Rational agents converge to proposals consistent with the welfare-efficient allocation, even under informational decentralization.


## Section 5. Conclusion

The dominant strategy for all participants is to maximize the gains available from cooperation while minimizing the continuation-value losses cooperation entails. When all agents behave this way, welfare-increasing trades propagate through the mechanism, inefficient deviations collapse, and short-term and long-term preferences come into alignment.

The resulting outcome is the unique allocation in which all agents adopt proposals consistent with the welfare-efficient allocation. Efficiency emerges not from revelation or centralized information, but from an incentive gradient that restricts profitable deviations to actions that increase welfare.


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