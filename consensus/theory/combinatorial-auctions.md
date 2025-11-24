---
title: Saito and Combinatorial Auction Theory
description: 
published: true
date: 2025-11-24T18:55:53.637Z
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

Readers interested in the protocol-level details should consult our simplified network description at [/consensus]. Below we provide a more abstract explanation of how Saito manages the combinatorial allocation problem. It does this by creating a three-way trilemma between blockspace, time and collusion utility, and allowing agents to navigate it by tweaking their: (i) **broadcast strategy** and (ii) **bidding choice**.

### starting with a Dutch Clock Auction...

Saito Consensus uses an iterating Dutch clock auction to regulate block production. The cost of producing a block adjusts to keep production constant in equilibrium, which  means the *burn fee* variable that determines the price of block production acts as a continuous market price for transaction inclusion over time.

Any user who requires immediate fulfillment can always pay the current price and obtain inclusion directly by producing a block themselves. Users who prefer cheaper inclusion or leveraging their bid to secure collusion utility must instead enter the portfolio-bidding process, and navigate a trilemma that the mechanism creates between all three classes of utility through their choice of broadcast and bidding behavior.

### creates the essential trilemma...

The *burn fee* locks the price of space/time for agents who have no desire for collusion utility, cooperating with other agents to compile a competitive bid opens the possibility of collusion, as the routing payout (refund) offered by the mechanism is transferred in expectation to the node that submits the winning portfolio.

Saito manages this by making **broadcast strategy** a strategic choice within the mechanism. When users seek to cooperate in the submission of portfolio bids, multi-broadcast ensures forward propagation through the sybil-proof properties of the mechanism, ensuring any bid reaches the maximum number of nodes as quickly as possible.

More restricted distribution is necessary for the purchase of "collusion utility" as reducing competition for collection of the fee is necessary to afford the producer a higher marginal profitability in expectation, which is needed to rationally justify the provision of additional forms of collusion utility in return.

This creates a three-way tradeoff (trilemma) where the sybil-proof properties of the mechanism turn broadcast strategy into an observable indicator of preference for collusion goods. More importantly, because every form of utility can be traded-off against any other, at any arbitrary fee level, agents have strategies to granularly optimize their welfare:

- More Space
Agents can accept slower confirmation in expectation, or shift a larger portion of their fee to public broadcast strategy.

- Faster Inclusion
Agents can reduce the size of their transactions, or ask colluding producers to divest a portion of their surplus to self-generate routing work and speed up their production of blocks, trading some collusion utility for faster-inclusion.

- More Side-Benefits
Reducing the size of the transaction or shifting to private broadcast increases the profitability of the block producer, enabling more side-benefits.

## 4. Incentive Alignment Through Revealed Preference

The fact that changes to bidding and broadcast strategy increases welfare for users in expectation allows routing mechanism to guarantee in expectation that:

- actions that raise welfare are cheap or profitable  
- actions that lower welfare are costly or punished  
- deviation gains correspond to missing welfare-improving trades

Thus, routing-work mechanisms indirectly implement **efficient combinatorial trade**—without needing direct revelation, without a central auctioneer, and without reconstructing infinite-dimensional preference maps.
