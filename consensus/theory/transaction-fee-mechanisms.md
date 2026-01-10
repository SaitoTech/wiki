---
title: Transaction Fee Mechanisms
description: 
published: true
date: 2026-01-10T19:22:24.118Z
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

This page explains why these papers do not provide grounds for general claims about what is possible in distributed consensus. The issue is not the mathematical correctness of their theorems within their formal models; it is that the models have systemic problems that prevent them from holding even within their own restricted settings. The problems are:

- **off-equilibrium path exclusion:** the models prune strategically-relevant deviations through which mechanisms can enforce honest behavior via credible deterrence;

- **improper reduction:** the models alter the strategic environment when invoking the Revelation Principle in ways that produce a direct mechanism that is not strategically equivalent to the original game and thus not permitted under Myerson;

- **dimensional collapse:** the models shift between single-parameter and multi-dimensional assumptions in ways that drive them into internal contradiction.

## 1. Off-Equilibrium Path Exclusion

The TFM papers argue that they are permitted to prune off-equilibrium user and miner strategies in ways that are not permitted in implementation theory. When analyzing user strategies, the TFM papers assume miner honesty; when analyzing miner strategies, they assume user honesty. Cleaving the strategy space in this way excludes all mechanisms that deliver incentive compatibility through the threat of credible punishments in off-equilibrium paths.

## 2. Improper Reduction

The Revelation Principle states that if some outcome can be implemented by **any** mechanism meeting its criteria for reduction, then there exists a **direct mechanism** equivalent. The TFM papers invoke this to reduce the transaction settlement game to an abstract stylized mechanism in which users share their valuations for blockspace directly with the mechanism.

This step violates the Revelation Principle by invoking it while **shrinking the strategy space rather than preserving it**. The specific violation is that Myerson requires any direct mechanism to preserve the full strategic environment of the original game. The model must be able to implement all successful as well as unsuccessful equilibria. All preferences expressable in the full game must remain expressable in the reduced-form game.

The TFM papers fail this requirement.  Actions that are acknowledged to be feasible and strategically-relevant in the real mechanism -- such as the insertion of fake transactions by miners or side-contract payments from users to miners -- are removed entirely from the strategy space in the reduced mechanism. This error breaks the equivalence the Revelation Principle is meant to guarantee, and makes it impossible to generalize results back from the (non-)equivalent model to the original and full-form game.

## 3. Dimensional Collapse

The TFM papers ask users to share their private valuations for “blockspace” with the mechanism. Additional forms of utility -- preferences for timing, transaction ordering, MEV protection, side-payments and other benefits of collusion -- are acknowledged as factors that affect strategic behavior yet are never truthfully revealed to the mechanism.

In implementation theory, all preferences that affect implementability of the social choice rule must be truthfully revealed to a mechanism. This is not done in the TFM papers, which casually introduce previously-undisclosed preferences when and where necessary to break incentive compatibility.

This vacillation between acknowledging a multi-dimensional reality and suppressing it introduces internal contradictions. Classical single-parameter assumptions are used to ensure monotonicity assumptions or apply Myerson’s Lemma. Unrevealed preferences are then invoked to justify agent preferences for off-equilibrium deviations. This is not permitted.


## Summary

Although the TFM literature adopts the language of incentive compatibility, the way it models incentive compatibility and collusion-resilience is not aligned with the formal requirements of economics.

While there are other issues with these works, the three major problems above unambiguously break the requirements that Hurwicz, Maskin, and Myerson establish for studying the implementability of social choice rules. As such, foundational results like the Revelation Principle cannot be invoked to generalize about implementability. All that remains is an analysis of equilibrium behavior inside specific models with arbitrarily restricted message spaces.

