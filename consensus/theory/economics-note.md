---
title: Untitled Page
description: 
published: true
date: 2025-12-03T07:25:55.513Z
tags: 
editor: markdown
dateCreated: 2025-12-03T07:25:55.513Z
---

# Saito Economics Note

This note explains how Saito Consensus constructs an informationally decentralized mechanism that implements a welfare-efficient social choice rule, despite standard economic intuition suggesting this is not possible. 


## Section 1: The Underlying Problem

The puzzle is straightforward: if agents can freely misreport in an informationally-decentralized mechanism, then incentive compatibility should not be possible, and no mechanism should be able to implement efficient outcomes.

The purpose this note is to isolate the modeling assumption that produces these impossibility results: that agents cannot face higher costs for sending messages that induce deviations from welfare-optimal outcomes. Under this assumption, deviations are cheap and efficient implementation becomes impossible.

Saito breaks this assumption by introducing endogenous message costs that create deviation externalities. The mechanism permits welfare-improving trades to occur, but forces trades that deviate from the welfare-efficient allocation to reduce the agent’s probability of receiving a conditional refund by more than they gain through the trade. This loss of expected income lowers continuation value and discourages deviation. Rational agents shift toward proposals consistent with efficient play.

The remainder of this paper explains how this transforms the incentive environment: the feasible deviation set collapses, profitable misreports disappear, and the strategic configurations that drive classical impossibility results cannot be sustained in equilibrium.

## Section 2: Standard Impossibility Results

Standard impossibility results across economics and distributed decision‑making share a common premise: messages are assumed to be costless, and agents are assumed to face no differential cost for proposing outcomes that deviate from welfare‑efficient allocations. 

This assumption is so deeply embedded in implementation theory that for decades it attracted virtually no scrutiny. Perhaps driven by a tendency to analogize communication to ordinary speech, Hurwicz (1972) embedded it in his seminal paper on mechanism design when he described all statements as equally cheap to express. Maskin’s work on Nash implementation then carried it forward by abstracting away communications completely, assuming agents could send any messages, message spaces were unrestricted, and all messages were equally easy to transmit.

As Maskin’s abstraction took hold, Myerson’s articulation of the Revelation Principle pushed the assumption even further out of sight.  By showing that any implementable indirect mechanism could be represented as a direct one in which agents simply report their types, Myerson recentered the study of incentive compatibility on the study of direct mechanisms, in which all messages take the  form of type reports, and nothing in the formalism distinguishes one message from another or allows their costs to differ.

While indirect mechanisms that could not be reduced to direct mechanisms under the Revelation Principle remained known, because their incentives were not describable entirely through type reports, they were often regarded as being shaped by factors not easily quantifiable within the direct-mechanism framework. The industry assumed that formalization was scientifically desirable. But as soon as any element of an indirect mechanism became amenable to formalization, it was necessarily incorporated into a type space, which had the effect of forcing it into a model that required costless speech.

In this way, the Revelation Principle created a quiet gravitational well. It could only study mechanisms if their assumptions were compatible with the requirements of Myerson-Maskin, but those requirements foreclosed the possibility of finding a solution with a structurally mediated cost of communication within the mechanism itself. 

It is striking how consistently this same assumption reappears in other important results. In bilateral trade, the Myerson–Satterthwaite theorem presumes that agents can misstate valuations without facing any penalty for doing so. In strategic communication, Crawford–Sobel model all messages as costless and commitment‑free, which ensures that only coarse partitions of information can be credibly conveyed. And in distributed consensus theory, impossibility results such as Bracha-Toueg depend on the assumption that agents can issue multiple inconsistent proposals at no personal cost, making it impossible to prevent strategic forking or to force convergence on a single consistent state.

Across these domains, mechanisms are modeled as passive recipients of frictionless messages that carry no commitments, impose no costs, and do not alter continuation payoffs. Once this is recognized, the impossibility results can be seen as artifacts of this shared modeling choice. The key point is that nothing in informational decentralization itself requires communication to be costless. The symmetry and frictionlessness of the message space are assumptions of the canonical models, not necessities of the environment.

In Section 3 we move on to show how Saito implements exactly such a change. By embedding cryptographic signatures in communications through the mechanism, and then using those signatures as signals which affect the distribution of a conditional refund, Saito breaks the core assumption that drives these impossibility results -- and restoring incentives for efficient implementation even in informationally decentralized settings.

## Section 3: Embedding Differential Message Costs

This section explains how Saito embeds differential message costs. The basic idea is simple: when a mechanism can make an agent’s continuation value depend on the content of their proposals, messages stop being costless and the symmetry that drives classical impossibility results disappears.

### 3.1 Technical Requirements

Implementing broadcast strategy as a mechanism design primitive requires three structural changes to the mechanism. The way in which bidders broadcast messages must affect their utility, the mechanism must be able to observe their  choices, and it must condition continuation value on its observation. Three techniques that enable this are: portfolio bids, routing signatures and routing payouts (conditional refunds).

**(a) Portfolio Bids**

To make forwarding consequential, the mechanism must first create conditions under which cooperation changes the utility an agent can obtain from the mechanism. It does this by making the composition of utility that agents receive from the mechanism contingent on how they communicate within it.

This is possible by allowing participants to  cooperate in assembling portfolio bids, group submissions that combine many smaller proposals into a larger batch which must settle at the same time. The dynamic is analogous to a factory which prioritizes larger orders: buyers who want faster service can pool their orders into a  collaborative purchase, benefiting from faster speeds otherwise unavailable to buyers at their price level. The cost of cooperating is the need for private pre-submission information-sharing, which becomes visible to the mechanism once these exchanges are marked with cryptographic routing signatures. 

**(b) Cryptographic Routing Signatures**

 The mechanism enforces visibility of these pre-submission exchanges by requiring agents to affix routing signatures when forwarding proposals. These signatures do not constrain the content of a proposal; they simply  authorize the recipient to use it when compiling a portfolio bid.

Any cryptographically secured chain-of-signatures that authorizes action-in-mechanism also serves as a verifiable record of the participants whose welfare is be affected by cooperation. As such, this minimal informational structure allows the mechanism to inspect the set of participants who are benefiting from the assembly of any portfolio bid. By inspecting the routing paths embedded in a portfolio bid, the mechanism can observe the participants involved, the order in which information flowed, and the efficiency with which they cooperated.

**(c) Routing Payouts / Conditional Refunds**

Access to this information then allows the mechanism to make this observability payoff-relevant, by leveraging the information contained in these routing paths to modify auction preference and to offer a conditional refund across the set of participants it observes to be cooperating.

Auction preference can be modified through the incorporation of Dutch Clocks and similar techniques that give collaborative bids an inherent advantage over individual bidder. The mechanism may be also structured to break ties by preferring proposals with a more efficient set of routing paths, for instance, or by modifying the required bid based on the length of the routing path needed to compile it.

A conditional refund may also be offered to any participant recorded in any routing path. While the size of the refund may vary with individual bids assembled into a portfolio bid, the degree of competition for collecting it depends entirely on the messaging strategies of participants.

These three components form a causal chain: portfolio bids create meaningful cooperative value, routing signatures make that cooperation observable, and routing payouts convert that observability into differential continuation value.

### 3.2 Broadcast Strategy

These three innovations are enough to make broadcast strategy a payoff-relevant action and a new primitive in mechanism design. Ceteris paribus, any agent who forwards a proposal to a peer creates immediate  consequences:

forwarding changes payoff odds: any transfer affecting the number of agents identifiable in the routing path changes the expected profitability of all participants in the system, and the sender loses some probability of receiving the conditional refund while the receiver gains some.

forwarding changes the utility bundle: not only through the speed-advantage the underlying mechanism offers to portfolio bids, but through the newfound ability of participates to engage in side-deals in exchange for bid-flow, such as buyers who extend additional private benefits ("collusion goods") in return for payout odds on routing paths.

forwarding changes strategic incentives: because forwarding increases the receiver’s refund eligibility and reduces the sender’s own, the sender must weigh benefits of independent submission against the long-term sacrifice in continuation value gained from participating in a cooperative bid.

With these three dynamics in play, forwarding becomes a choice about how to compete in the mechanism not merely whether to send information. The consequences of these choices are immediately strategically relevant.

Some forwarding choices increase continuation value; others dilute it. Private broadcast makes collusion more rational at the cost of slower bid submission. Public broadcast sacrifices collusion utility for speed as more participants have the ability to assemble competitive bids, reducing the expected profitability of any particular one, and thus their willing to pay for bid-flow by offering private benefits in return.

A three directional trade-off / trilemma is pulled into being that creates a directional incentive structure absent from classical models. The message space is no longer symmetric. And with broadcast strategy now affecting both cost and utility across multiple dimensions,  the "cheap talk" assumption supporting the impossibility results discussed in Section 2 collapses on the most fundamental level.


## 4. The Emergence of Efficient Implementation

The structural changes described in Section 3 do more than eliminate the “cheap talk” assumption required by the impossibility results in Section 2. They also make proposals that are consistent with welfare-efficient allocations uniquely attractive to participants.

In this section, we show why this is the case: why all profitable deviations must take the form of cooperative portfolio bids, and how the internal trade-offs portfolio bids invite users to manage make the welfare-efficient equilibrium uniquely stable.

### 4.1 All Efficient Improvements Require Portfolio Bids

Any profitable deviation must improve an agent’s expected allocation; it must correspond to a welfare-increasing trade. Yet under the settlement rules of the mechanism, unilateral bids cannot improve an agent’s allocation: the only way to secure a more favorable outcome is through the  construction of portfolio bids.

As we explained in Section 3, the availability of different broadcast strategies allow participants to propose granular trade-offs between the three classes of goods managed by the mechanism:

- Good A: the item under auction

- Good B: time preference

- Good C: collusion-utility

Yet these benefits are not free, since any participant who participates in a portfolio bid reduces their continuation value by sacrificing a claim on the routing payout.

Thus, every welfare-increasing deviation necessarily involves an internal sacrifice: agents can improve their utility only by accepting a reduction in their future continuation value. Deviations that do not improve immediate utility by enough to offset  expected future losses are loss-making and irrational in expectation.

This means that all profitable deviations must take the form of welfare-increasing trades, and all such welfare-increasing trades require agents to expose themselves to reduced continuation value as the cost of cooperation. The point of optimal consumption is thus when 

### 4.2 Broadcast Strategy Optimizes Against Time

Because cooperation improves current utility but reduces continuation value, rational agents must balance **short-term gains** in Goods A, Good B, and Good C. against long-term losses in their ability to purchase those same goods at arbitrary points in the future.

In other mechanisms this trade-off becomes insolvable. But with routing work it can be efficiently priced within the mechanism itself, since the time-preference dynamics that govern the consumption of all goods can be manipulated directly within the mechanism through the trade-offs portfolio bids allow agents to propose between all competing forms of utility, balancing:

- **immediate time-preference** (internal to portfolio bids), and

- **future continuation value** (external through continuation payouts)

Because broadcast strategy mediates both present and future time-preference, it becomes the optimizing tool agents use to navigate and optimize  trade-offs. Trade-offs can be managed within the current bid or within the portfolio-construction game, as each agent broadcasts proposals in the manner that maximizes their combined current-utility and continuation-value payoff. Portfolio bids that maximize expected welfare survive; inefficient deviations do not.

### 4.3 Efficiency Emerges as the Unique Equilibrium

The net effect is that the most beneficial strategy for all participants is to maximize the gains from cooperative portfolio bids while minimizing their continuation-value losses. This strategy uniquely navigates the trade-off between short-term utility composition and long-term continuation value.

When all agents follow this strategy:

- welfare-increasing trades propagate forward,

- inefficient deviations collapse,

- and the mechanism drives short-term and long-term time preference into equilibrium.

The equilibrium that remains is the one in which all rational agents forward and adopt proposals consistent with the welfare-efficient allocation. Efficiency emerges not by assumption or revelation, but because the mechanism embeds the incentive gradient needed to restrict profitable deviations exclusively to genuine welfare improvements.

The result is that efficient implementation becomes achievable even under informational decentralization.



