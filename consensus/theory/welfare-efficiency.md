---
title: Obstacles to Welfare Efficiency in Informationally Decentralized Mechanisms
description: 
published: true
date: 2025-11-24T19:49:02.527Z
tags: 
editor: markdown
dateCreated: 2025-11-24T19:49:02.527Z
---

## Myerson–Satterthwaite & Green–Laffont Applicability

Saito Consensus implements outcomes that are **Pareto-efficient relative to the informational and topological constraints of the network**. We have a page that [demonstrates this](/consensus/theory/welfare-efficiency), showing that the only profitable deviations available to participants correspond to welfare-improving trades.

Offering a welfare-efficient informationally decentralized mechanism is a significant claim: classical mechanism design asserts that decentralized, budget-balanced, incentive-compatible mechanisms cannot generally implement efficient outcomes. As such, the purpose of this page is to explain why these impossibility results -- particularly Myerson–Satterthwaite for bilateral trade and Green–Laffont for public goods -- **do not apply** to routing-work mechanisms like Saito.

### Relevant Papers
- Myerson & Satterthwaite (1983), *Efficient Mechanisms for Bilateral Trading*  
- Green & Laffont (1979), *Incentive and Informational Constraints in Public Goods Provision*  
- Hurwicz (1972, 1979), *On Informational Decentralization*  
- Maskin (1977, 1999), *The Revelation Principle*  
- Jackson (2001), *A Crash Course in Implementation Theory*  


## Foundational Impossibility Results

### 1. **Myerson–Satterthwaite (1983)**  

The Myerson–Satterthwaite theorem is a central negative result in economics. It studies the case of a single buyer and a single seller, each of which holds private valuations for a good and communicates with a mechanism only through costless type reports. 

Although stated for the one-buyer/one-seller case, the result extends naturally to **multi-agent** and **multi-good** environments as any large market decomposes into bilateral trades. Intuitively, if efficient decentralized exchange fails even in the simplest bilateral setting, optimality cannot be restored by adding more participants, more goods, or more complex trading structures which are themselves subject to the same underlying limitation.

Formally, Myerson-Satterthwaite claims that in a bilateral-trade environment with private values and quasilinear utilities, no mechanism can be simultaneously:

- **Bayesian incentive compatible**,  
- **ex post efficient**, and  
- **budget balanced**.

The conclusion is stark: when all strategic behavior is representable as costless misreporting within a direct-revelation mechanism, *even the simplest form of decentralized trade cannot be implemented efficiently*. This result is often taken as a benchmark for the limits of what decentralized market mechanisms can achieve under informational constraints.

### **2. Green–Laffont (1979)**  

The Green–Laffont theorem is the foundational impossibility result in economics for public-goods mechanisms. It studies environments in which agents privately value a public good and communicate only through costless reports of their valuations. The theorem shows that no mechanism can simultaneously achieve efficiency, budget balance, and strategy-proofness under these informational constraints.

Like Myerson–Satterthwaite, Green–Laffont is established in a clean and highly stylized setting, but its implications extend far beyond the minimal model. Anytime collectively optimal outcomes require joint action within the mechanism, the same informational limitations arise. For this reason, the Green–Laffont theorem is understood as placing general limits on welfare efficiency in decentralized mechanisms.

Formally, in a public-goods environment with private valuations and quasilinear utilities, no mechanism can be:

- **strategy-proof**,  
- **budget balanced**, and  
- **efficient**.

The takeaway mirrors the bilateral-trade impossibility: when mechanisms rely exclusively on costless type reports, efficient decentralized provision of a public good cannot be achieved without violating either incentive compatibility or budget balance. This result serves as the canonical benchmark for the challenges faced by decentralized systems attempting to allocate or fund shared resources, including the collective security levels required to maintain a public blockchain.


## 2. Saito Consensus is not Limited

Both the Myerson-Satterthwaite and Green-Laffont impossibility results depend on a number of structural assumptions that do not apply to Saito Consensus:

1. **direct-revelation communication**  
   Agents communicate only by sending costless reports of their private types. 

2. **Free deviations**  
   Every deviation is modeled as an alternative type report with no cost or observable consequence. 

3. **Quasilinear utilities**  
   Utility is value minus payment; non-price utility dimensions (e.g., time, routing surplus, collusion utility) are excluded.

4. **No verifiable or costly actions**  
   Mechanisms cannot condition outcomes on observable behavior in the environment.

5. **Finite-dimensional type spaces**  
   Agents have well-defined valuations over a finite set of outcomes, all of which must be reportable.

These assumptions define the narrow domain for which the impossibility results are valid. 


## 3. Saito Consensus is Outside This Domain

Routing-work mechanisms violate these assumptions in essential ways:

### **A. Saito is an indirect, action-based mechanism**  
Broadcast strategy, routing work, and block production are **actions** with observable consequences, not costless type reports.  
The mechanism operates on behavior rather than declarations, placing it squarely outside the direct-revelation environment required by the theorems.

### **B. Deviations are not free**  
Forwarding, restricting broadcast, producing blocks, and generating routing work all involve **real economic costs**.  
The deviation space in Myerson–Satterthwaite and Green–Laffont—arbitrary costless misreports—does not exist in Saito.

### **C. Preferences are multi-dimensional and non-quasilinear**  
Users value blockspace, inclusion time, and collusion utility.  
These interact nonlinearly; utility cannot be written as value minus payment.  
Thus the quasilinear domain required by both impossibility theorems is absent.

### **D. The type space is infinite-dimensional**  
Preferences over time are continuous, and preferences over collusion bundles are unbounded.  
The combinatorial space of (space × time × side-benefits) is infinite.  
Direct-revelation mechanisms cannot express these preferences.

Because these assumptions fail, the classical impossibility results simply **do not apply** to routing-work mechanisms.

---

## 4. Implication

This page does not demonstrate that Saito Consensus is welfare efficient. For a positive discussion of how routing work achieves welfare efficiency please see our page on **[Welfare-Improving Trade Lemmas](/consensus/theory/welfare-efficiency)**.

Nonetheless, it is straightforward to observe that the Myerson–Satterthwaite and Green–Laffont class of impossibility results do not bind the mechanism. The conventional wisdom -- developed from these results -- that these problems cannot be addressed in informational decentralized mechanisms is not correct.