---
title: Transaction Fee Mechanisms
description: 
published: true
date: 2025-11-25T09:50:59.671Z
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

- **misuse of standard terminology:** use of terms like incentive-compatibility that depart significantly from the meaning of standard implementation-theoretic concepts in economics, yet used as if they are interchangeable;

- **misuse of the Revelation Principle:** invocation of the Revelation Principle without satisfying the conditions required for its use, typically through pruning or restricting off-equilibrium behaviors; and

- **dimensional misspecification:** a general class of modelling issues that stem from treating block production sometimes as a single-parameter allocation problem, and sometimes as a multi-dimensional optimization problem.

In the remainder of this page, we cover these errors briefly.


### 1. Conceptual Misalignment


### 2. Misuse of the Revelation Principle


### 3. Conflicting Modelling Assumptions












The first major problem involves the assumption that the transaction fee is a scalar value that reflects only the bidder’s private valuation for blockspace. This is clearly incorrect. Transaction fees are non-scalar values that express a joint preference over a multi-dimensional bundle of utility: they can be adjusted to buy more or less blockspace, faster or slower inclusion, and/or to secure off-chain benefits (“collusion goods”) that peers may provide in return for exclusive access to the transaction.

Because transaction fees are non-scalar in practice, they lack the property of monotonicity these models assert they must have as a pre-requisite for proving it is impossible to achieve incentive compatibility generally. The impossibility results therefore fail on straightforward grounds of model misspecification: they do not accurately capture the mechanisms they claim to analyze.

Worse, while these papers explicitly acknowledge that other types of utility exist (such as incentives to collude) their models never ask agents to reveal their valuations for these additional forms of utility as required by implementation theory. This pushes these papers beyond misspecification and into open contradiction: they invoke the framework for incentive compatibility provided by Maskin (2002) without following its most basic requirements for truthful preference revelation.

Even if we overlook this problem and agree to treat the transaction fee as a scalar value that can at least theoretically reflect the truthful valuation that users have for blockspace, the security-levels and amount of blockspace provided by any TFM clearly change based on the strategies chosen by agents within the mechanism. This means the amount of utility available for purchase through the mechanism cannot be known in advance, and we have the classic problem of "interdependent valuations" under which it is not possible to make any assumptions about the truthfulness of even a scalar fee.

A second and more subtle flaw is the assumption that block producers can faithfully implement incentive-compatible protocols without needing to reveal their own private preferences to those protocols. This contradiction ("faithful implementation" without "faithful revelation") is overlooked by these models, which then make matters worse by explicitly forbidding producers from including self-generated transaction in blocks. This restriction violates the requirement that we do not prohibit agents from revealing preferences to the mechanism.

On a closing note, we observe that all of the TFM papers to date also fail to properly specify the social choice rule with which they desire incentive compatibility. While the authors of most papers implicitly adopt the rule of the Vickrey auction ("efficient allocation") none seem aware that this social choice rule cannot be implemented in a two-sided mechanism where supply as well as demand-side pressures must come into equilibrium.
   
   A school of academics led by Tim Roughgarden (Columbia) and Elaine Shi (Cornell) argue it is impossible to build incentive-compatible blockchains. Saito Consensus provides a direct counter-example, exposing several fundamental problems with the assumptions underlying these papers in the process.

The first major problem involves the assumption that the transaction fee is a scalar value that reflects only the bidder’s private valuation for blockspace. This is clearly incorrect. Transaction fees are non-scalar values that express a joint preference over a multi-dimensional bundle of utility: they can be adjusted to buy more or less blockspace, faster or slower inclusion, and/or to secure off-chain benefits (“collusion goods”) that peers may provide in return for exclusive access to the transaction.

Because transaction fees are non-scalar in practice, they lack the property of monotonicity these models assert they must have as a pre-requisite for proving it is impossible to achieve incentive compatibility generally. The impossibility results therefore fail on straightforward grounds of model misspecification: they do not accurately capture the mechanisms they claim to analyze.

Worse, while these papers explicitly acknowledge that other types of utility exist (such as incentives to collude) their models never ask agents to reveal their valuations for these additional forms of utility as required by implementation theory. This pushes these papers beyond misspecification and into open contradiction: they invoke the framework for incentive compatibility provided by Maskin (2002) without following its most basic requirements for truthful preference revelation.

Even if we overlook this problem and agree to treat the transaction fee as a scalar value that can at least theoretically reflect the truthful valuation that users have for blockspace, the security-levels and amount of blockspace provided by any TFM clearly change based on the strategies chosen by agents within the mechanism. This means the amount of utility available for purchase through the mechanism cannot be known in advance, and we have the classic problem of "interdependent valuations" under which it is not possible to make any assumptions about the truthfulness of even a scalar fee.

A second and more subtle flaw is the assumption that block producers can faithfully implement incentive-compatible protocols without needing to reveal their own private preferences to those protocols. This contradiction ("faithful implementation" without "faithful revelation") is overlooked by these models, which then make matters worse by explicitly forbidding producers from including self-generated transaction in blocks. This restriction violates the requirement that we do not prohibit agents from revealing preferences to the mechanism.

On a closing note, we observe that all of the TFM papers to date also fail to properly specify the social choice rule with which they desire incentive compatibility. While the authors of most papers implicitly adopt the rule of the Vickrey auction ("efficient allocation") none seem aware that this social choice rule cannot be implemented in a two-sided mechanism where supply as well as demand-side pressures must come into equilibrium.

- improper generalization under the Revelation Principle
- 
- improper reduction under Maskin
- use of single-parameter model to study multi-parameter game

However, a careful technical reading of these papers reveals a common structural issue in their modeling and reductions: they treat a miner/block producer’s choice-set as a single private scalar (blockspace) and reduce the environment to a single-parameter auction in which deviations are “cheap” scalar reports. Real block production, by contrast, is a **multi-dimensional production problem**: the producer simultaneously chooses real inclusion capacity, whether and how many fake/collusive transactions to insert, and how to monetize or structure time-priority. Because fake/collusive transactions are themselves actions that change the realized supply curve, they ought to be part of the type and action space — not “cheap reports.” When the producer’s feasible deviations change the production plan (not just a single report), the standard single-parameter implementation arguments (monotonicity + payment identity, direct revelation reductions) do not apply.  

This introduction therefore acknowledges the mathematical correctness of the impossibility theorems *within their stated models*, but it also flags a systematic modeling error: **applying single-parameter implementability conditions to an environment that is inherently multi-parameter**. The result is impossibility conclusions that do not necessarily generalize to more realistic models where collusion, fake transactions, and time-priority are represented as strategic goods.

---

# References

> Notes:
- [Redesigning Bitcoin’s Fee Market](https://arxiv.org/abs/1709.08881) — Ron Lavi, Or Sattath, Aviv Zohar (2017)

- [Transaction Fee Mechanism Design](https://arxiv.org/pdf/2106.01340.pdf) — Tim Roughgarden (2021)

- [Foundations of Transaction Fee Mechanism Design](https://arxiv.org/pdf/2111.03151.pdf) — Hao Chung, Elaine Shi (2021/2022)

- [MEV and Auction Design](https://arxiv.org/pdf/2106.01357.pdf) — A. Avarikioti, A. Chitra, T. Daian, B. Fanti, et al. (2021–2022)

- [Transaction Fee Mechanism Design in a Post-MEV World](https://arxiv.org/pdf/2307.01686.pdf) — Maryam Bahrani, Pranav Garimidi, Tim Roughgarden (2023)

- [Maximizing Miner Revenue in Transaction Fee Mechanism Design](https://arxiv.org/pdf/2302.12895.pdf) — Hao Chung (2023)

- [Collusion-Resilience in Transaction Fee Mechanism Design](https://arxiv.org/pdf/2402.09321.pdf) — Hao Chung, Tim Roughgarden, Elaine Shi (2024)

- [Tiered Mechanisms for Blockchain Transaction Fees](https://www.research.ed.ac.uk/files/455492846/KiayiasEtalMARBLE2024TieredMechanismsForBlockchain.pdf) — Aggelos Kiayias et al. (2024)

- [Transaction Pricing Mechanism Design and Assessment for Blockchain](https://www.sciencedirect.com/science/article/pii/S2667295221000349/pdfft) — Z. Wang et al. (2022)

- [Multi-side Incentive Compatible Transaction Fee Mechanism](https://www.sciencedirect.com/science/article/pii/S0045790623004743/pdfft) — X. Liu et al. (2024)


---

# Short, dispassionate summary of the technical claim across these works

- **What the papers prove (within their models).** Under the standard TFM model — with finite block size, static one-shot auctions, a revelation-style bidding space, and the miner treated as an auctioneer with the ability to inject fake bids but where the mechanism’s message space is modeled as single-parameter — no non-trivial mechanism simultaneously satisfies (i) user incentive compatibility (UIC), (ii) miner incentive compatibility (MIC), and (iii) a strong form of miner-user collusion-resilience (variously stated as 1-SCP, c-SCP, OCA-proofness, or global SCP). Several theorems (Chung & Shi; Chung–Roughgarden–Shi; Roughgarden) formalize these impossibilities and show that any TFM satisfying these constraints must be trivial (zero confirmed transactions or zero miner revenue) under the stated assumptions.

- **The shared modeling reduction.** These impossibility proofs typically rely on two key modeling choices: (1) blockspace is represented as a scalar, single-parameter good; and (2) producer deviations are represented as cheap scalar reports or as injections that do not alter the underlying production technology or the structure of feasible states. With these reductions in place, implementation-theory machinery (monotonicity conditions, Myerson-style payment identities, and revelation-principle arguments) are used to derive contradictions.

- **Why that reduction is problematic for generalization.** In real blockchains the miner/block producer controls **a multi-dimensional production plan**: genuine inclusion capacity, insertion (or withholding) of fake/collusive transactions, ordering/time-priority choices, and strategic bundling. These choices change the realized supply curve and hence the mapping from reported bids to outcomes in ways that cannot be represented as a unidimensional scalar misreport. When the producer’s deviations amount to changing the production plan (which can be costly and produce different feasible states), the canonical single-parameter implementability conditions no longer apply automatically. Therefore the impossibility theorems correctly rule out mechanisms *within their formal model*, but **they do not by themselves settle feasibility in richer, multi-parameter models that include collusive/fake transactions and time-priority as endogenous strategic goods**.

---

If you’d like, next steps I can take immediately (pick one):

- (A) Expand the bibliography to include the adjacent Budish / credible-auction / HFT literature and add precise DOIs;  
- (B) Verify and replace any remaining ambiguous or weakly-sourced entries above (I can fetch canonical arXiv/DOI pages for each and normalize citation metadata); or  
- (C) Draft the full TFM “impossibility” page using the introduction above and structured sections that (i) summarize each paper’s model and theorem, (ii) expose the common reduction, and (iii) propose corrected modeling primitives and alternative positive constructions.

Which would you like me to do next?
