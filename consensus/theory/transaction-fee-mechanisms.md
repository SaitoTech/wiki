---
title: Transaction Fee Mechanisms
description: 
published: true
date: 2025-11-25T13:30:25.287Z
tags: 
editor: markdown
dateCreated: 2025-11-25T09:50:59.671Z
---

# Transaction Fee Mechanisms (TFMs)

### Relevant Papers

- [Foundations of Transaction Fee Mechanism Design](https://arxiv.org/pdf/2111.03151.pdf) — Hao Chung, Elaine Shi (2021)

- [Transaction Fee Mechanism Design](https://arxiv.org/pdf/2106.01340.pdf) — Tim Roughgarden (2021)

- [Transaction Fee Mechanism Design in a Post-MEV World](https://arxiv.org/pdf/2307.01686.pdf) — Maryam Bahrani, Pranav Garimidi, Tim Roughgarden (2023)

- [Maximizing Miner Revenue in Transaction Fee Mechanism Design](https://arxiv.org/pdf/2302.12895.pdf) — Hao Chung (2023)

- [Collusion-Resilience in Transaction Fee Mechanism Design](https://arxiv.org/pdf/2402.09321.pdf) — Hao Chung, Tim Roughgarden, Elaine Shi (2024)

- [Barriers to Collusion-resistant Transaction Fee Mechanisms](https://arxiv.org/abs/2402.08564) - Yotam Gafnim, Aviv Yaish (2024)

A school of primarily American academics, led by Elaine Shi (Cornell) and Tim Roughgarden (Columbia), has produced a series of papers arguing that incentive-compatible blockchains, or “transaction fee mechanisms,” cannot be designed under certain formal assumptions.

Mixing concepts from computer science and implementation theory, this literature is relevant to Saito Consensus for two reasons. The first is that several of its stated impossibility results directly contradict the guarantees of the Saito protocol. Second, the terminology introduced in these works -- most prominently UIC, MIC, side-contract-proofness, and OCA-proofness -- has become influential in industry discussions and is frequently treated as though it aligns with standard implementation theory.

As this page explains, these papers do not provide grounds for general claims about what is possible in distributed consensus. The issue is not the mathematical correctness of their theorems within their formal models; it is that the models themselves have three systemic problems that prevent their conclusions from generalizing and, in several cases, from holding even within their own restricted settings.

- **misunderstanding of implementation theory:** both in its foundational requirements for preference revelation, and its use of terms like incentive-compatibility in ways that depart significantly from their standard meaning in economics;

- **misuse of the Revelation Principle:** invocation of the Revelation Principle without satisfying the conditions required for its use, typically through pruning or restricting off-equilibrium behaviors; and

- **dimensional misspecification:** a general class of modelling issues that stem from treating block production sometimes as a single-parameter allocation problem, and sometimes as a multi-dimensional optimization problem.

In the remainder of this page, we cover these errors briefly.

## 1. Misunderstanding of Implementation Theory

In implementation theory, a mechanism cannot be incentive-compatible if participants do not have the ability to express the preferences that a mechanism needs in order to choose a desired outcome. And if the scope of preference revelation is restricted what remains is not an implementation problem --  but an equilibrium analysis inside an artificially constrained game.

The TFM papers study exactly such an artificially constrained game. When analyzing user strategies, they assume miners behave honestly; when analyzing miner strategies, they assume users behave honestly. By cleaving the strategic space in this way, the model excludes the possibility of the complex strategic interactions that can arise when both sides respond strategically to deviations by the other. And this removes precisely the dynamics that, in many mechanisms, makes truthful preference revelation mutually reinforcing -- where deviations are deterred not by structural limitations but by the treat of credible reactions from the opposing party.

By removing the possibility that strong deterrents can be created in such "off-equilibrium" paths, the TFM literature departs fundamentally from the structural requirements of implementation theory, which require analysis beings with the specification of a **social choice rule** that defines the outcomes a mechanism is intended to implement. The TFM papers do not define such a rule. Without an SCR, there is no basis for evaluating whether revealed preferences are truthful, or know if undesirable outcomes in off-equilibrium paths might deter undesirable action in one-sided games. And because these requirements are not satisfied, the tools of implementation theory -- such as Myerson’s Lemma, Maskin monotonicity, and the Revelation Principle -- cannot be applied even in theory, let alone used to make general statements about the impossibility of designing incentive compatible mechanisms.

---

## 2. Misuse of the Revelation Principle

Even if the TFM papers satisfied the informational requirements of implementation theory -- which they do not -- their use of the Revelation Principle to generalize their results would still be incorrect. The Revelation Principle states that if some outcome can be implemented by **any** mechanism, then there exists a **direct mechanism** in which agents truthfully report their preferences and the same outcome is achieved. But for this to work the direct mechanism must preserve the full strategic environment of the original game.

The TFM papers do not follow this requirement, invoking the Revelation Principle but then doing the opposite of what it requires by **shrinking the strategy space rather than preserving it**. Actions that acknowledged to be feasible and affect outcomes in the real game -- such as inserting fake transactions, or colluding with counterparties -- are removed entirely from the strategy space. The messages that agents might send in these spaces consequently disappear, and with them the potential for counterparties to balance with a suitably deterrent response.

As a result, while these papers invoke the Revelation Principle to generate a simplified game form, the game they generate thus differs in significant ways. Because the reduction changes the set of actions permitted in the mechanism, it also changes the set of possible outcomes, and thus set of implementable equilibria and destroys the equivalence the Revelation Principle is meant to guarantee.

In short, even if we were to assume that the Revelation Principle applies -- which it does not for the reasons outlined in Section 1 -- the reduction performed in the TFM papers to generate a simplified direct equivalent for analysis would still be invalid because it **changes the strategic environment rather than preserving it**. A mechanism derived from such a reduction cannot be used to make claims about what is implementable in the original environment, let alone justify the assumption that only VCG-style auctions could possibly achieve incentive compatible outcomes in the original environment. The connection between the game analyzed and the mechanisms they claim to reflect is severed by the reduction itself.

## 3. Dimensional Misspecification

A third problem in the TFM literature is that when users are asked to reveal their private preferences with the mechanism, they are invited to share only a single number: their bid representing their private valuation for “blockspace.” Yet when these model explain why users might behave strategically, they assert the existence of additional attributes -- concerns over timing, ordering, MEV exposure, or the potential benefits to be gained from colluding with miners or other users. These considerations imply that the set of relevant preferences is inherently multi-dimensional.

The TFM model alternates between acknowledging a multi-dimensional reality and suppressing it in the interests of methodological simplificy. Yet in genuinely multi-dimensional environments, classical single-parameter results such as monotonicity assumptions or Myerson’s Lemma do not apply. A single scalar bid cannot encode complex multidimensional preferences, and no single-parameter direct mechanism can support truthful revelation of desired trade-offs between them.

The consequences of this modelling failure become evident once these papers attempts to use VCG as the benchmark for “ideal” blockchains, as VCG mechanisms are well-defined only in environments where agents explicitly communicate all dimensions of utility that affect our desired allocations. By suppressing the relevation of all but one dimension of preference, while leaving other relevant preferences strategically relevant but unexpressed, these papers create an unoptimizable game where implementability is theoretically undefined.

**In short, while the authors of these papers are making laudable attempts to bridge the gap between computer science and economics, none of the impossibility results produced in the domain to date apply implementation theory with the degree of rigour needed to make substantive claims about whether.**

More problematically, we observe very directly that in Saito Consensus incentive compatibility is achieved in part through the existence of punitive outcomes that punish defectors in off-equilibrium paths, as bid-shading by users is punished by the threat of producers purchasing blockspace for use in collusive trades with users involing off-chain payments.

The solution to the problem these papers seek to understand lies, ironically, in the part of the strategy space they forbid their readers from considering.