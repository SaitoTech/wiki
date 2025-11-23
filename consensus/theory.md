---
title: Theory and Research - Saito Consensus
description: 
published: true
date: 2025-11-23T17:53:34.810Z
tags: 
editor: markdown
dateCreated: 2025-11-23T15:28:21.939Z
---

# Theory & Research — Saito Consensus

This page is intended as a concise, discipline-neutral introduction to **Saito Consensus** for readers with training in mechanism design, economics, or distributed systems. It exists to provide a clean map of the intellectual claims, and an understanding where Saito is and is not bound by standard impossibility results.

The rest of this page contains four sections: (1) a short description of what is theoretically new in Saito—namely, its use of asymmetrically costly state transitions; (2) a brief explanation of the classical impossibility claims in economics and computer science that assume such asymmetry cannot exist; (3) a compact account of how Saito makes the solution possible in spite of those claims; and (4) a guide to the subpages that examine specific results in more depth, showing where Saito relaxes their assumptions or avoids being bound by them entirely.


## #1. What is New (asymmetrical costs)

Saito changes the economics of permissionless consensus by making **harmful state transitions more expensive to propose than honest ones**. Concretely, the protocol ties the cost of proposing a block to how efficiently a node has collected fees. Because more efficiently funded blocks cost less to extend, the network naturally converges on a longest chain built from these blocks.

This creates a persistent cost asymmetry: to orphan an honest block, attackers must cover the efficiency gap between their own fee-collection work and that of the honest block they are trying to orphan. Doing so requires attackers to spend their own money to produce blocks and subject it to a payout lottery that returns value only in expectation, not deterministically.

This single structural change shifts the set of profitable deviations and opens a class of implementable outcomes that are infeasible under symmetric-cost models such as standard POW and POS mechanisms. 


## #2. Classic Impossibility Claims

Existing impossibility results in both distributed systems and economics rely on a set of background assumptions that are almost never questioned — including the assumption that **asymmetrically costly state transitions cannot be implemented in a permissionless setting.**

Saito not only relaxes this assumption, but the technical changes that allow it to do so (the addition of cryptographically-signed routing paths to informationally decentralized mechanism) put it in direct tension with two additional assumptions that are also taken as axiomatic in much of the literature. These three assumptions are:

- **Symmetric proposal costs:** most models treat the cost of proposing a block or state transition or publishing another equilibrium-affecting message as identical in expectation between adversarial and honest nodes.

- **Unobservable Contribution:** traditional models assume the mechanism cannot observe or verify which agents performed value-creating actions, and therefore cannot condition costs or rewards on those actions.

- **Exogenous Feasibility:** models assume that the feasibility and cost of proposing a state transition are fixed and independent of the topology or efficiency of the message-passing substrate.

In computer science these assumptions underlie many standard results in distributed systems and mechanism design. Bracha–Toueg (1985) uses the assumption to assert maximum theoretical tolerance of distributed systems to adversraial actors, Dwork–Lynch–Stockmeyer (1988) uses it for partial synchrony assumptions in symmetric-cost models, while Babaioff et al. (2012) explicitly declare a topological impossibility claim in a paper on routing payouts.

In economics, the parallel assumption appears in the mainstream mechanism design literature. Beginning with Hurwicz (1972) and developed through Myerson, Maskin, and Holmström, the Revelation Principle is built on the premise that all messages are costless to send, and any mechanism that claims to implement an outcome must tolerate the existence of unverifiable and cost-free misreports.


The impossibility results that follow in both fields flow directly from this assumption, and merit revisiting exactly because Saito relaxes (1) and (2) in a way that invalidates the reductive step used in their impossibility claims, allowing different implementability claims in Saito-class mechanisms.

---

## #3. Technical Implementation

What exactly is new about Saito-class mechanisms, at the level of mechanism primitives, that creates the asymmetry described in Section 1 and justifies relaxing the assumptions imposed on us in Section 2? Several factors predominate:

1. **Routing signatures and observable forwarding.** Every transaction carries a cryptographic record of its forwarding path. The protocol can therefore verify, for each node, its observable contribution to the collection of fee-bearing transactions for eventual burning and resurrection through the costly payout lottery.

2. **Routing-work accounting.** Fees are decomposed into position-weighted routing work. These weights can be used in isolation or summed to create variable ratios that diverge as routing paths increase in length. The growing divergence between the cost of proposing blocks (regulated by the former) and the expected payout (regulated by the latter) is exploited to impose losses on deviating agents in off-equilibrium paths. Costs become higher and guaranteed while refunds are lower (in expectation) and uncertain.

3. **Topology Drives Feasibility.** Saito creates an endogenous, monotonic, mechanism-level ordering over routing paths that makes inefficient (or sybil-inflated) paths strictly dominated because unnecessary message-passing raises costs faster than they raise expected reward.

These three factors drive the emergence of the asymetrically-costly proposals highlighted in Section #1.

Because proposal cost depends on routing efficiency, and the longest chain is selected for efficiency, coalitions that attempt to orphan honest blocks must mimic the efficiency of the blocks they are orphaning, which requires contributing more of their own funds to blocks (and the immediately burn) than honest extenders needed to do so contribute to theirs.

The orphaning of the block also immediately refunds any burned tokens belonging to the orphaned producer triggered by that block. So orphaning not only imposes costs on attackers, but refunds costs paid by honest nodes.

And because their costs are certain but payouts fractional and probabilistic, the attackers suffer losses in expectation on a known portion of the fees-in-block. With proper design, this implicit tax can be increased to the point it outweighs any benefits the producer can gain from orphaning the honest block, creating a cost gap for attackers that holds across a wide range of resource distributions, including cases where an attacker controls a large fraction of the network.

---

## More Information:

The following section contain links to subpages that discuss the specific papers and impossibility results mentioned above, demonstrating exactly where the results apply to routing work mechanisms, and where the results do not.

**Start with Saito**
- [A Simple Proof of Sybil-Proof (Lancashire, Parris, 2023)](https://github.com/SaitoTech/papers/tree/e32c51db6aae071a41b7e481d0f5ba6cd75ec12d/sybil)
mathematical proof of sybil-proofness of the mechanism, containing the Hurwicz' "formula" for the mechanism in five succinct bullet points on its first page.

**Distributed-systems context**
- `/consensus/theory/distributed-systems.md` — precise relation to FLP, Bracha–Toueg, DLS; which model axioms we change
- `/consensus/theory/consensus-properties.md` — safety, liveness, economic finality (informal → formal)

**Mechanism-design & economics**
- `/consensus/theory/revelation-principle.md` — Foundations Note: why standard direct-mechanism reductions fail when supply and feasibility are endogenous
- `/consensus/theory/asymmetric-cost.md` — formal development of cost-asymmetry and its implementability consequences
- `/consensus/theory/collective-action.md` — free-rider and tragedy-of-the-commons framing for routing work

**Security /攻撃 revisited as economic deviations**
- `/consensus/theory/sybil-proof.md` — *A Simple Proof of Sybil-Proofness*: rigorous statement and proof sketch; assumptions and limits
- `/consensus/theory/majoritarian-attacks.md` — reframe 51% as *costless orphaning*; formal cost bounds
- `/consensus/theory/censorship.md` — ATR and incentive paths that convert censorship into an economic liability

**Supplementary & references**
- `/consensus/theory/math-appendix.md` — formal lemmas, notation, and proofs
- `/consensus/theory/bibliography.md` — selected literature (Bracha–Toueg, Dwork–Lynch–Stockmeyer, Babaioff et al., Hurwicz, Maskin, etc.)

---

## What Saito does *not* claim

To keep the academic case clean, we explicitly list limitations:

- Saito does **not** prevent all reorganizations; it prevents *costless* reorganizations (i.e., reorganizations that are not strictly more expensive than honest extension).

- Saito does **not** eliminate all coordination risks, it merely provides agents with the ability to model the cost-of-attack on the mechanism and develop strategies based on that understanding. 

- Physical-layer attacks (eclipse, long-term censorship at the ISP level) remain out of scope for the protocol alone and require network-layer defenses.

Being explicit about these limits is essential for clear assessment and for formal models.

---

## Quick path for specialists

- Mechanism designers: start with `/consensus/theory/revelation-principle.md` then read `/consensus/theory/asymmetric-cost.md`.  
- Distributed-systems theorists: start with `/consensus/theory/distributed-systems.md` then `/consensus/theory/consensus-properties.md`.  
- Crypto-economists: read `/consensus/theory/sybil-proof.md` and `/consensus/theory/majoritarian-attacks.md`.

---

## Next steps (how this section will be completed)

1. Convert each bullet above to a full subpage with formal definitions and proofs.  
2. Add a short technical appendix describing protocol primitives used in proofs (routing signatures, routing-work formula, ATR rules).  
3. Publish a self-contained Foundations Note (revelation-principle limitations) and a companion short paper summarizing the sybil-proof proof for non-specialists.

---

### References & further reading

See the bibliography page for canonical references and the technical papers linked from the subpages. Key starting points include: Babaioff et al. (*On Bitcoin and Red Balloons*), Dwork–Lynch–Stockmeyer, Bracha–Toueg, Hurwicz (revelation principle), and our sybil-proof paper.

---

*If you want, I can now draft the individual subpage for one of the following (pick one): the Foundations Note on the Revelation Principle, the Sybil-Proof proof sketch, or the Majoritarian Attacks formal page.*
