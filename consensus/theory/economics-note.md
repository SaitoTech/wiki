---
title: Saito Consensus - Broadcast Strategy and Messaging Costs
description: 
published: true
date: 2025-12-03T13:46:04.672Z
tags: 
editor: markdown
dateCreated: 2025-12-03T07:25:55.513Z
---

# Saito Economics Note

The puzzle is straightforward: if agents can freely misreport in an informationally-decentralized mechanism, then incentive compatibility should not be possible, and no mechanism should be able to implement efficient outcomes.

The purpose of this note is to explain how Saito Consensus constructs a  welfare-efficient informationally decentralized mechanism, starting with the observation that impossibility results are driven by an assumption Saito violates: the expectation of costless messaging within the mechanism.


## Section 1: The Impossibility Results Problem

The underlying source of the impossibility results that drive conventional wisdom in implementation theory is a specific modeling assumption: that agents cannot face higher costs for sending messages that induce deviations from welfare-optimal outcomes.

This assumption is so deeply embedded in implementation theory that for decades it attracted virtually no scrutiny. Perhaps driven by a tendency to analogize communication to ordinary speech, Hurwicz (1972) embedded it in his seminal paper when conceptualizing all statements as equally cheap to express. Maskin’s work on Nash implementation then cemented it by abstracting away communication costs completely, assuming agents could send any messages, message spaces were unrestricted, and all messages were equally easy to transmit.

Myerson’s development of the Revelation Principle then pushed the assumption further out of sight.  By showing that any implementable indirect mechanism could be represented as a direct mechanism in which agents simply report their types, Myerson re-centered the study of incentive compatibility on the study of direct mechanisms, in which all messages take the form of type reports, and nothing in the formalism distinguishes one message from another or allows their costs to differ.

Although indirect mechanisms remained known that could not be reduced to direct mechanisms under the Revelation Principle, because their incentives were not describable entirely through type reports, they were often regarded as being shaped by forces that were not easily quantifiable and called for formalization. But as soon as any element of such an indirect mechanism became amenable to formalization, it was necessarily incorporated into a type space, which had the effect of forcing it into a model that assumed costless speech.

In this way, the Revelation Principle created a quiet gravitational well. Because it could only observe variables in mechanisms compatible with the requirements of Myerson-Maskin, and because such mechanisms could not manipulate cost of messaging, the framework effectively blinded theorists to the possibility that agents' preferences could endogenously affect the cost of communicating within the mechanism itself.

This blind spot was reinforced as similar assumptions proved analytically useful in driving meaningful discoveries independently across several economic and computational subfields. In bilateral trade, the Myerson–Satterthwaite theorem analyzes environments where agents can misstate valuations without facing any penalty for doing so. In strategic communication, Crawford–Sobel model all messages as costless and commitment‑free, ensuring that only coarse partitions of information can be credibly conveyed. And in distributed consensus theory, impossibility results such as Bracha-Toueg rely on symmetry assumptions that treat all proposals as equally feasible to issue, preventing the protocol from distinguishing cooperative from adversarial messaging patterns.

In all of these papers, mechanisms are modeled as having frictionless messages that carry no commitments, impose no costs, and do not alter continuation payoffs. Once this is recognized, the impossibility results they produce become clear artifacts of this modeling choice. Yet nothing in informational decentralization itself requires communication to be costless. The symmetry and frictionlessness of the message space are assumptions of the canonical models, not necessities of the environment.

And it is this assumption that Saito violates, by introducing endogenous message costs that create deviation externalities. While the mechanism permits welfare-improving trades to occur, it forces all such trades to reduce the agent’s probability of receiving a conditional refund, causing a cascading loss that only minimized if agents shift toward proposals consistent with efficient play. In the next section we outline how this is possible in theory.

## Section 3: Asymmetry through Broadcast Strategy

The basic idea behind Saito's solution is simple: when a mechanism can make an agent’s **continuation value** -- their expected future purchasing power -- depend on the content of their proposals, messages stop being costless and the symmetry that drives classical impossibility results disappears.

### 3.1 Technical Requirements

Implementing broadcast strategy requires three structural changes to a mechanism. The way in which bidders broadcast messages must affect their utility, the mechanism must be able to observe their choices, and it must condition continuation value on its observation. Three techniques enable this in Saito:

**(a) Portfolio Bids**

The mechanism first creates conditions under which cooperation changes the utility an agent receives from the mechanism. This is done by allowing participants to cooperate in assembling portfolio bids, group submissions that combine many smaller proposals into a larger bundle which competes with non-cooperative bids.

The dynamic is analogous to a factory which prioritizes larger orders: buyers who want faster service can pool their orders to benefit from faster speeds otherwise unavailable to buyers at their price level. This creates a need for participants to share messages prior to submitting orders, an informational process which can become made visible to the mechanism using cryptographic routing signatures. 

**(b) Cryptographic Routing Signatures**

The mechanism enforces visibility of portfolio bids by requiring agents to affix routing signatures when forwarding proposals. These signatures do not constrain the content of a proposal; they simply authorize the recipient to include it when compiling a portfolio bid.

Any cryptographic chain-of-signatures that authorizes action-in-mechanism also serves as a verifiable record of the authorized players. As such, this minimal informational structure makes collaboration visible to the mechanism itself, which can observe the participants involved, the order in which they acted, and the efficiency with which they cooperated directly from the routing paths themselves.

**(c) Routing Payouts / Conditional Refunds**

Access to this information then allows the mechanism to modify utility, by using the information contained in these routing paths to adjust auction preference, and to offer a conditional refund whose payout varies in expectation based on the contents of those paths.

Auction preference can be modified through the use of Dutch Clocks that give collaborative bids an inherent advantage in meeting bidding targets over individual bidders. The mechanism may be also break ties by preferring proposals with a more efficient set of routing paths, or by modifying the group-bid based on the length of routing path needed to assemble it.

A conditional refund may also be offered to any participant recorded in any routing path. While the size of the refund may vary based on other factors, the degree of competition for collecting such a payout depends entirely on the messaging strategies of participants. Cooperating bring benefits, but also increases competition for payouts.

### 3.2 Broadcast Strategy

These three components form a causal chain: portfolio bids create meaningful cooperative value, routing signatures make that cooperation observable, and routing payouts convert that observability into differential continuation value. This is sufficient to make broadcast strategy a payoff-relevant action:

- **forwarding changes payoff odds:** any transfer affecting the number of agents identifiable in the routing path changes the expected profitability of all participants in the system, and the sender loses some probability of receiving the conditional refund while the receiver gains some.

- **forwarding changes the utility bundle:** not only through the speed-advantage the underlying mechanism offers to portfolio bids, but through the newfound ability of participates to engage in side-deals in exchange for bid-flow, such as buyers who extend additional private benefits ("collusion goods") in return for payout odds on routing paths.

- **forwarding changes strategic incentives:** because forwarding increases the receiver’s refund eligibility and reduces the sender’s own, the sender must weigh benefits of independent submission against the long-term sacrifice in continuation value gained from participating in a cooperative bid.

With these three dynamics, choosing to cooperate with other agents becomes a strategic choice. Some choices increase continuation value; others dilute it. The degree of competition for the inputs to creating portfolio bids also changes the supply-side calculus of those providing utility within the mechanism. Private broadcast reduces competition, slowing inclusion but making side-deals more profitable. Public broadcast sacrifices collusion utility as more participants compete to assemble portfolio bids.

A three directional trade-off / trilemma is pulled into being that creates a directional incentive structure absent from classical models. The message space is no longer symmetric. The cost of making any proposal must be expressed in terms of which other form of in-mechanism utility the bidder wishes to sacrifice. And with broadcast strategy now affecting cost and utility across multiple dimensions, the "cheap talk" assumption supporting the impossibility results in Section 2 collapses on the most fundamental level.

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

To understand why, we define a welfare-increasing trade as any reallocation among Goods A, B, and C that strictly increases an agent’s utility according to their own preferences. We then observe that all profitable deviations within the mechanism must take the form of cooperative portfolio bids. We can offer this argument as a series of lemmas leading to a general result:

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

Whatever strategy maximizes short-term gains against long-term losses while permitting granular trade-offs against time-preference in both domains uniquely navigates the trade-off.

When all agents follow this strategy:

- welfare-increasing trades propagate forward,

- inefficient deviations collapse,

- and the mechanism drives short-term and long-term time preference into equilibrium.

The equilibrium that remains is the one in which all agents forward and adopt proposals consistent with the welfare-efficient allocation. Efficiency emerges not by assumption or revelation, but because the mechanism embeds the incentive gradient needed to restrict profitable deviations exclusively to genuine welfare improvements.

