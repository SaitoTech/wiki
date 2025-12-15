---
title: Saito and the Revelation Principle
description: Why Saito is not convertible to a direct mechanism under the Revelation Principle
published: true
date: 2025-12-15T10:02:44.215Z
tags: 
editor: markdown
dateCreated: 2025-12-15T09:14:18.734Z
---

# Why the Revelation Principle Does Not Apply to Saito

Many impossibility results in mechanism design rely on the Revelation Principle, introduced by Roger Myerson in his foundational work on mechanism design (Myerson, 1979; 1981). Informally, the Revelation Principle states that for a broad class of mechanisms, any outcome that can be implemented through techniques that ask participants to take actions within the mechanism can also be implemented by a direct mechanism -- one in which participants simply report their preferences truthfully and the mechanism computes the outcome.

In situations where the Revelation Principle can be used to draw equivalence between direct and indirect mechanisms, the technique has allowed has allowed economists to prove the general impossibility of achieving certain outcomes involving efficiency, incentive compatibility, and welfare—optimality. This is important as while mechanisms that cannot be converted to direct mechanisms under the Revelation Principle are rare, they do exist and are not subject to many common impossibility results.

As such, since the non-convertibility of Saito under the Revelation Principle is a valuable property of the mechanism, this page explains specifically why Saito operates outside the domain in which the Revelation Principle applies. Readers should note that the claim is not that the Revelation Principle is incorrect, but that its assumptions do not hold in the setting in which Saito operates, and thus revelation-based reductions are not possible with routing mechanisms. 

## Pillar 1: Time is Endogenous, Variable, and Payoff-Relevant

Whereas in other mechanisms time is fixed by the mechanism in advance, in Saito the speed of block production and the rates at which time can be traded-off for other forms of utility depend on the choices and routing strategies made by all participants in the system. This makes time simultaneously:

- a utility (faster vs. slower inclusion),
- a cost (tradable for more blockspace, collusion utility)
- a feasibility constraint (which outcomes are possible at all).

While participants may form expectations about how various routing and bidding strategies affect their own speed-of-inclusion, the mechanism does not supply a stable, exogenous quantity of time that it can ask users to value as a common external reference. Instead:

 - the supply of time provided by the mechanism depends on the strategic behavior of other participants (the interdependent valuations problem)
- participants cannot declare a well-defined for other forms of utility, since these can be purchased by sacrificing a good of unknown supply and endogenously-determined value.

This undermines the applicability of the Revelation Principle, as the Revelation Principle assumes users are reporting well-defined preferences for specific amounts of utility that must exist prior to their strategic interaction in the mechanism. When the supply of time and other forms of utility are manipulable endogenously by the mechanism in the way that Saito does, this assumption fails.

These limitations are well recognized in the mechanism design literature in seminal works discussing implementation in the presence of interdependent values (Maskin, 1992; Dasgupta and Maskin, 2000; Bergemann and Morris), dynamic mechanism design (Bergemann and Välimäki), and costly communication (Renou and Tomala). Saito operates in exactly this class of fluid environment where the assumptions required for the Revelation Principle do not hold.


## Pillar 2: Actions Replace Reports; Preferences Are Expressed by Exclusion

In Saito, users do not communicate preferences by reporting them.
They indicate their comparative preferences for certain forms of utility over others by taking actions that exclude the possibility of making other choices.

This occurs specifically through the broadcast strategies that users make, which:

- limit who sees a transaction,
- exclude potential competitors and bundles,
- and make certain combinations of allocations impossible.

For example:

Distributing transactions publicly invites competition and faster inclusion, but sacrifices the ability to trade certain forms of collusion goods at the prevailing exchange rate that private broadcast imposes on those sets of time-dependent trades. Conversely, routing sacrifices speed for collusion utility.

Once a routing decision is made, the alternatives that were not chosen cannot be recovered or reported later. Strategies that a direct mechanism might observe to be dominated are no longer possible, as players cannot switch to prefer a form of utility they have excluded through their bidding and broadcast strategies. Preferences are therefore revealed through irreversible action, not declaration.

Further complicating matters is that some payoff-relevant information in Saito is valuable precisely because it is not revealed: the mechanism can observe the outcomes of activities (the existence of a specific transaction in a specific mempool) but not the intentions or strategic intent motivating this signal. And some of the most important information in Saito is only visible in its absence:

 - who did not receive a transaction
 - which competitors never had the opportunity to respond
 - which routing paths were never opened

These absences shape outcomes but they leave no observable trace that a mechanism can condition on, and -- together with the problems above -- block the Revelation Principle from working, given its assumption that:

 - agents can costlessly report preferences,
 - reports do not affect feasibility,
 - the mechanism can observe all payoff-relevant information.

Saito Consensus violates all three of these requirements:

- routing expresses irreversible opportunity-cost
- routing changes the feasible set of outcomes
- absence of evidence is not evidence of absence

As a result, replacing routing with direct reporting necessarily changes the incentive structure of the network and the set of outcomes that any direct mechanism could find implementable, which breaks the equivalent of the direct mechanism required for the correct functioning of the Revelation Principle.

These failures are documented to break the Revelation Principle in economic studies of costly-communication and constrained message spaces and costly communication (Renou and Tomala), in models where strategic actions precede or replace reporting (Maskin, 1992; Dasgupta and Maskin, 2000), and in the literature on limited observability (Attar et al, 2025), which show that indirect mechanisms characterized by the kinds of privacy embedded in routing decisions can make equilibria implementable which are impossible to implement with full and truthful reporting of all agent preferences. 

Pillar 3: Infinite Combinatorial Complexity of Preferences

Saito involves multiple interacting goods:

blockspace,

time-to-inclusion,

privacy,

collusion opportunities,

continuation value,

risk and uncertainty.

These goods are not quasilinear, trade off against one another, and include time as a continuously variable dimension. A participant’s “preference” is therefore not a single value, but a preference map over infinitely many combinations of goods, timing, and routing outcomes.

Applying the Revelation Principle would require participants to report this entire preference map. Such reports would be:

infinite-dimensional in theory,

impossible to elicit in practice,

and unverifiable by the mechanism.

This limitation is well known in mechanism design: direct revelation breaks down with non-quasilinear utilities, multi-dimensional goods, and continuous choice spaces. Saito simply operates in that region.

Summary

The Revelation Principle is a powerful tool, but it applies only when its assumptions hold. In Saito they do not, because:

Time is endogenous, variable, and payoff-relevant.

Preferences are expressed through costly, feasibility-altering actions, including privacy-preserving exclusion.

Preferences are infinitely multi-dimensional and cannot be fully reported.

These features place Saito outside the class of mechanisms to which revelation-based impossibility results apply. This is not a novel claim about the Revelation Principle itself, but a recognition—supported by existing academic work—that its scope does not include mechanisms with endogenous feasibility, costly action-based signaling, privacy, and continuous multi-dimensional trade-offs.