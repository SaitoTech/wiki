---
title: Transaction Fee Mechanisms
description: 
published: true
date: 2025-12-07T06:12:40.419Z
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

A line of academic work, led by Elaine Shi (Cornell) and Tim Roughgarden (Columbia), has produced a series of papers arguing that incentive-compatible blockchains, or “transaction fee mechanisms,” cannot be designed under certain formal assumptions.

Mixing concepts from computer science and implementation theory, this literature is relevant to Saito Consensus for two reasons. The first is that several of its stated impossibility results directly contradict the guarantees of the Saito protocol. Second, the terminology introduced in these works -- most prominently UIC, MIC, side-contract-proofness, and OCA-proofness -- has become influential in industry and is frequently treated as though it aligns with implementation theory.

As this page explains, these papers do not provide grounds for general claims about what is possible in distributed consensus. The issue is not the mathematical correctness of their theorems within their formal models; it is that the models themselves have three systemic problems that prevent their conclusions from holding even within their own restricted settings.

- **off-equilibrium path exclusion:**  pruning strategically-relevant deviations through which mechanisms often enforce honest behavior via credible deterrence;

- **improper reduction:** altering the strategic environment when invoking the Revelation Principle to produce a direct mechanism that is not strategically equivalent to the original game;

- **dimensional collapse:** shifting between single-parameter and multi-dimensional assumptions when connecting underlying agent preferences to in-mechanism behavior.

In the remainder of this page, we cover these errors briefly.

## 1. Off-Equilibrium Path Exclusion

The TFM papers attempt to study incentive compatibility within the confines of an artificially constrained game. When analyzing user strategies, they assume miner honesty; when analyzing miner strategies, they assume user honesty. By cleaving the strategy space in this way, their model excludes the possibility that both sides may respond in strategically complex ways that punish deviations by the other.

This ommission is consequential, as it excludes the possibility of mechanisms that deliver incentive compatibility not through structural constraints on agent behavior but through the threat of credible punishments from opposing parties.


## 2. Improper Reduction

The Revelation Principle states that if some outcome can be implemented by **any** mechanism, then there exists a **direct mechanism** equivalent in which the same set of feasible outcomes are achieved.

For this to work the direct mechanism must preserve the full strategic environment of the original game. The model must be able to implement all successful as well as unsuccessful equilibria defined by the original model.

The TFM papers fail this requirement, invoking the Revelation Principle in a manner that **shrinks the strategy space rather than preserves it**. Actions that are acknowledged to be feasible and affect outcomes in the real mechanism -- such as the insertion of fake transactions in blocks, or side-contract payments from users to miners -- are removed entirely from the strategy space in the reduced mechanism.

As a result, while these papers invoke the Revelation Principle to generate a simplified game form, the game form generated shows a change in the set of possible outcomes, and thus in the set of implementable equilibria. This shift breaks the equivalence the Revelation Principle is meant to guarantee, and which provides the basis for generalizing impossibility results back from the reduced-game to the original environment and full-form mechanism.

## 3. Dimensional Collapse

The TFM papers typically ask users to share their private valuations for “blockspace” with the mechanism as their form of truthful preference revelation. Yet additional forms of utility -- preferences for timing, transaction ordering, MEV protection, or even the benefits of collusion -- are acknowledged as factors that affect strategic behavior.

This vacillation between acknowledging a multi-dimensional reality and suppressing it introduces internal contradictions. Classical single-parameter assumptions are needed to ensure monotonicity assumptions or apply Myerson’s Lemma. But unrevealed preferences are needed to justify agent preferences for off-equilibrium deviations.


## Summary

Although the TFM literature adopts the language of incentive compatibility, the way it models incentive compatibility and collusion-resilience is not aligned with the formal requirements of economic theory.

The differences break the conditions that Hurwicz, Maskin, and Myerson establish for studying the implementability of social choice rules. As a result, foundational results like the Revelation Principle cannot be invoked to generalize about implementability. What remains is simply an analysis of equilibrium behavior inside a specific mechanism with restricted message spaces.

