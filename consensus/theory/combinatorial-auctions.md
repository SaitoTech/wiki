---
title: Saito and Combinatorial Auction Theory
description: 
published: true
date: 2025-11-24T17:46:48.592Z
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

## The Solution Requires Indirect, Action-Based Mechanisms

The significance of Saito Consensus as an indirect mechanism becomes more obvious once the limitations of direct mechanisms in combinatorially.

Once blockchains are understood as offering users a bundle of heterogeneous goods, it becomes clear that no direct mechanism can elicit the full valuation information required to implement an efficient allocation. A direct mechanism would need each agent to report its valuation over every possible bundle of (blockspace × time × collusion) utility. Because the number of bundles grows combinatorially -- and because preferences over time and side-benefits are continuous and unbounded -- the type space is infinite.

Indirect mechanisms handle infinite preference spaces gracefully, by filtering the set of revelant preferences prior to revelation. This is why Hurwicz (1972. 1979) explicitly allows actions with observable consequences to be treated as signals in a message space.

Jackson (2001) similarly notes that indirect mechanisms rely on *behavioral strategies* rather than type reports, and points out that the equilibrium behavior of participants “encodes” the private information relevant to the social choice rule being implemented, which can be high-dimensional. In auction theory, this idea also appears in the interpretation of bidding as a form of revealed preference: Milgrom and Weber (1982) show that ascending auctions elicit marginal valuations through sequences of observable bids, while Parkes (2001, 2006) and Ausubel and Milgrom (2002) generalize this insight to iterative and proxy-based combinatorial auctions in which actions, rather than full type reports, provide the mechanism with the information needed to handle allocation.

The same principle is in play in Saito Consensus. Instead of asking users to report an exponentially large preference map covering their valuations for all possible bundles of blockspace, time, and collusion goods, the mechanism turns **broadcast strategy** into an action-in-mechanism that affects allocation outcomes. Users with different valuations will prefer different broadcast strategies, which signal: how urgently they desire inclusion and whether they are using their bid in a collusive side-deal that involves the delivery of potentially unobservable forms of utility.

Broadcast strategy combines with bidding strategy to allow Saito to function as a revealed-preference mechanism. Agents do not communicate their types directly; instead, they choose broadcast strategies that are optimal given their private valuations, and the mechanism infers only the information necessary for allocation from the resulting network-level observables. This aligns precisely with the role of actions in indirect mechanism design as articulated by Hurwicz and formalized in modern implementation theory: when full type revelation is impossible, the mechanism must structure incentives such that *behavioral signals* substitute for explicit reports.

## Technical Implementation

Readers interested in the technical implementation of Saito Consensus should view our simplified description of [how the network works](/consensus). This section provides a brief explanation of how Saito Consensus manages combinatorial optimization in the presence of only two information signals: broadcast and bidding strategies.

Observe first that the "burn fee" adjusts in equilibrium to create a market price for blockspace/time that allows users to optimize their bidding strategies for those two forms of utility. The non-stop iterating Dutch Clock Auction that regulates block production allows users to optimize their bids only within a single block, but ad infinitum over the life of the chain itself.

Much like a "posted price" model, the market price for blockspace can be calculated on a per byte basis. Users who desire faster or slower inclusion can adjust their bids appropriately and only take action if they believe that fulfillment is rational in expectation.





. While the mechanism can only promise fulfillment of inclusion **in expectation** that is enough to achieve incentive compatibility as strategies are preferred in expectation.






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
