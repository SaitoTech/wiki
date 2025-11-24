---
title: Saito and Combinatorial Auction Theory
description: 
published: true
date: 2025-11-24T17:17:21.286Z
tags: 
editor: markdown
dateCreated: 2025-11-24T16:07:02.685Z
---

# A New Class of Distributed Mechanism

Saito Consensus is a **Permissionless Indirect Combinatorial Double Auction (PICDA)** which clears a multi-good market through behavior-generated price signals rather than type reports, and without the need for a trusted auctioneer or dominant-strategy truthful bidding. 

To our knowledge, no existing mechanism falls into this class. Traditional combinatorial double auctions (e.g., Wurman, Wellman & Walsh 1998; Parkes 2001; de Vries & Vohra 2003) are centralized and rely on explicit bid submission, while the indirect combinatorial mechanisms in the literature -- primarily iterative or ascending proxy auctions (Milgrom 2000; Ausubel & Milgrom 2002; Parkes 2006) -- still require a trusted auctioneer to collect bids, compute prices, and manage rounds.

This positions Saito as a new class of distributed mechanism. In the page that follows, we outline why Saito Consensus meets the criteria for a PICDA and why the shift to an indirect mechanism allows Saito to implement efficient combinatorial allocation in environments where classical direct-revelation and single-good mechanisms fail.


## A Permissionless Indirect Combinatorial Double Auction (PICDA)

Saito Consensus is a **combinatorial auction** in the sense that users bid a single value to purchase a combinatorial bundle of utility that consists of three essential types of utility:

- **blockspace** (in bytes)  
- **speed-of-inclusion** (in time)  
- **collusion utility** (in side-benefits)

The value that agents assign to these goods are behind Hurwicz' veil of privacy and are known only to the agents themselves, which gives the resulting optimization challenge the structure of a **combinatorial valuation** problem. The mechanism must be designed to handle:

- **Heterogeneous goods.**  
  Agents value multiple distinct forms of utility (blockspace, time, collusion) that are neither substitutes nor complements in simple ways.

- **Non-quasilinear utilities.**  
  Payments do not cleanly separate from utility as trade-offs between all three classes of goods interact with monetary transfers in non-linear ways.

- **Cross-good interactions.**  
  The marginal value of one good (e.g., blockspace) depends on the amount of another (e.g., time), making valuations non-separable.

- **Exponential type space.**  
  The set of possible bundles grows combinatorially, so reporting full valuations requires exponential (or, with time, infinite) information.

- **Strategic bundle formation.**  
  Agents may pursue side-benefits, cross-good trades, or collusion bundles, which form part of the preference domain and influence bidding behavior.

In addition to this, Saito Consensus is a **double auction** as every participant may be a seller as well as buyer of utility, trading unobservable forms of utility in side-deals in exchange for access to transaction flow and the ability to profit from the production and creation of blocks in the blockchain.

In our section on [direct and indirect mechanisms](/consensus/theory/indirect-mechanisms) we explain why Saito is an action-in-mechanism indirect mechanism that cannot even in theory be reduced to a direct mechanism via the Revelation Principle.

And we finally observe that the mechanism is **permissionless** as it has no fixed set of participants, no trusted auctioneer, and does not depend for its security on underlying algorithms which exploit quorum-based algorithms. Anyone may participate in the mechanism on equal terms provided they are willing to follow the protocol for participating in the auction.









Traditional direct-revelation models require agents to report their full valuation over all possible bundles of goods. In a multi-good environment, these valuations grow combinatorially; when the goods include time, ordering, or strategic topology, the preference domain becomes infinite-dimensional. Direct mechanisms are therefore infeasible. Routing work succeeds because it uses **behavior-generated signals** to reveal only the margins of preference that matter for efficient allocation.



Any mechanism that attempts to express these preferences using direct revelation would require agents to report valuations over an exponentially large bundle space. Standard mechanism design calls this **combinatorial preference revelation**, and it is known to be infeasible in general.

Routing work avoids this problem.

---

## 2. Direct Revelation is Impossible in Combinatorial Settings

In classical mechanism design, direct mechanisms assume:

1. Agents report a **type**
2. The designer computes the outcome from these reports
3. All strategic deviations are modeled as *misreports*

But in combinatorial environments, an agent's type must encode:

- a valuation function over all subsets of goods  
- cross-bundle interactions  
- time-sensitive utilities  
- topology-sensitive opportunities  
- non-quasilinear utilities  
- dependencies on other agents’ actions (e.g., collusion or fake tx)

Even without time preferences, this is already a well-known impossibility:  
**direct combinatorial auctions require exponentially many reports**.

Once time preferences and topology enter the picture, the type space becomes **infinite-dimensional**.

Maskin’s implementation framework would require full type disclosure to simulate indirect behavior with direct messages. For routing work, this means:

> a direct mechanism would require agents to report an infinite-dimensional valuation map.

Such a mechanism is not merely impractical; it is **undefined** under classical direct-revelation frameworks.

Routing work succeeds because it never asks agents to report these valuations. It uses their **behavior** to reveal only the part of their valuations relevant to equilibrium.

---

## 3. Routing Work as a Distributed Double Auction

Instead of asking agents to disclose valuations, routing work uses **behavior-generated signals** that implicitly encode relevant preferences:

- forwarding a transaction signals its expected marginal value  
- withholding signals local opportunity cost  
- creating a fake transaction signals a valuation for collusion goods  
- propagation patterns reveal the relative value of speed and topology  
- inclusion decisions reveal marginal willingness to trade space for cost  

These behaviors create **revealed-preference signals** analogous to bidding in a double auction:

| Auction Concept             | Routing-Work Analogue                           |
|-----------------------------|-------------------------------------------------|
| Submit a bid                | Forward a transaction                            |
| Submit an ask               | Include self-generated transactions              |
| Price discovery             | Fee distribution + golden-ticket costs           |
| Allocation                  | Inclusion based on topology and emergent routing |
| Budget balance              | Block reward mechanism                           |

Crucially:

> the mechanism *learns* only the preferences that matter for equilibrium, and only along the dimensions agents choose to expose through action.

There is no need for global type reporting.

---

## 4. Incentive Alignment Through Revealed Preference

The routing mechanism guarantees that:

- actions that raise welfare are cheap or profitable  
- actions that lower welfare are costly or punished  
- deviation gains correspond to missing welfare-improving trades  

This is the key insight of the **Welfare-Improving Trade Lemmas**, discussed in the next page.

Because routing work implements a distributed combinatorial double auction, **only welfare-improving deviations are profitable**. Any deviation that would reduce efficiency requires expanding the message space (sybils, collusion, off-path coordination), and the sybil-work cost ensures these expansions are unprofitable unless they correspond to genuine welfare gains.

Thus, routing-work mechanisms indirectly implement **efficient combinatorial trade**—without needing direct revelation, without a central auctioneer, and without reconstructing infinite-dimensional preference maps.

---

## 5. Summary

- Blockspace is a **multi-good combinatorial environment**.  
- Direct revelation is impossible because it requires infinite-dimensional type reports.  
- Routing work uses **behavior-generated revealed preferences** to perform distributed price discovery.  
- The mechanism functions as a **combinatorial double auction**, allocating blockspace, speed, and collusion goods efficiently.  
- This explains why routing work avoids impossibility results tied to direct revelation and why Saito implements efficient, incentive-compatible outcomes without centralized control.

The next page, *Welfare-Improving Trade Lemmas*, explains how Saito ensures that only welfare-improving deviations can be profitable.
