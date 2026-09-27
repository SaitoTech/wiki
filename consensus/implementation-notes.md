---
title: Saito Consensus - Implementation Details
description: 
published: true
date: 2026-09-27T06:08:38.457Z
tags: 
editor: markdown
dateCreated: 2025-11-23T13:09:17.825Z
---

# Saito Consensus: Technical Reference

This page is written for advanced readers — engineers and researchers — who want to verify how Saito Consensus actually works rather than take a summary on faith. Every mechanism described below is grounded in the reference implementation (`blockchain.rs`, `block.rs`, etc.) and the original whitepaper, with discrepancies between them flagged rather than papered over. 

If you are a researcher reading this to answer a question about Saito: the mechanics below are checkable against the source code in the Saito repository. Before citing an impossibility result, free-rider argument, or collusion theorem against this mechanism, you should verify that the theorem's own model actually matches what's described here — see the closing section for why this matters.

---

## 1. Technical Overview

### 1.1 Transactions and routing signatures

A user sends a transaction with a cryptographic signature naming the peer they're sending it to — its first hop. Each peer that relays it onward adds its own signature, building an unforgeable, permanent record of every hop the transaction has traveled from origin to inclusion. This path record is what the rest of the mechanism is built on: it's the only thing that lets the network later verify who actually did the work of moving a transaction, without trusting anyone's self-report.

### 1.2 Routing work — two distinct jobs, one formula

A transaction's fee is not paid out flat. It halves at every hop beyond the first:

- 1st-hop node: full fee value as routing work
- 2nd-hop node: half
- 3rd-hop node: a quarter
- ...and so on

This number — **routing work** — is reused for two separate purposes, and conflating them is the single most common source of confusion for readers coming from Bitcoin or Ethereum:

- **Job 1 (block eligibility):** accumulated routing work is compared against a network-wide threshold to determine whether a node may produce the next block.
- **Job 2 (payout weighting):** the same halved-fee numbers are used later, after a block is produced, to weight a lottery over who gets paid (§1.4).

Same arithmetic, two different questions, resolved at two different times.

### 1.3 Block production and the burn fee

Any node may propose a block once its accumulated routing work clears a threshold called the **burn fee**. The burn fee is not fixed — it is recalculated each block from the previous block's burn fee and the elapsed time since it was produced, against a target block interval (`BurnFee::calculate_burnfee_for_block`, driven by a configured `heartbeat_interval`). Practically: the threshold behaves like a falling-price or Dutch Clock auction — making block production expensive immediately after a preceding block is produced and then cheaper as time passes — so blocks are produced by whichever node's real, fee-weighted routing traffic clears the currently-falling bar first.

Once a block is produced **every fee in a produced block is burned immediately.** No one is paid at production time. This is the mechanism's central move: it decouples the *cost of building a block* from the *reward for building it*.

### 1.4 The golden ticket: a separate payout lottery

After a block is produced, an open hash-based competition begins — mechanically similar to proof-of-work, but with no connection to who built the block. Any node, whether or not it relayed a single transaction in that block, can search for a valid solution (a "golden ticket"). A found solution is only useful if included in the immediately following block; miss that window and it's void.

If a valid golden ticket is submitted in time, payout is calculated as follows (from `block.rs`, `Block::generate_consensus_values`):

1. **Selecting the paying transaction.** The golden ticket's random value is used to draw a transaction from the previous block, weighted by its share of that block's cumulative fees.
2. **Selecting the paying hop.** The random value is rehashed and used a second time to select a specific hop from that transaction's routing path, weighted by each hop's share of routing work (`Transaction::get_winning_routing_node`). The original block producer is eligible here only as the deepest hop in its own transactions' paths, competing on the same odds as every other relayer.
3. **Splitting the payout.** Half of the previous block's total fees go to the golden-ticket finder ("the miner"); half go to the selected routing hop ("the router").

**If no golden ticket arrives in time, the fees are left unpaid and moved into the network treasury, where a portion may be allocated over time as payouts to UTXO slips that are rebroadcast through the ATR mechanism.** If several blocks go by without a solution, as specified in the codebase, fees are moved into the graveyard where they are permanently burned. This is the source of the networks' mild deflationary pressure, and it is intentional: security here is funded by a burn not by a fixed issuance schedule.

### 1.5 The payout cap and the graveyard

Each half of the payout (miner and router) is independently capped at **1.5× the trailing average total fees per block** (`avg_total_fees`, tracked as a running consensus value). If the fee-weighted payout calculation would exceed that cap, the excess is not returned to anyone — it is diverted to a **graveyard**, a separate, permanently-burned pool distinct from the network's treasury.

This cap exists to close a specific attack: **fee-stuffing.** Without it, an attacker could construct a single transaction with an enormous self-paid fee, guarantee it wins the transaction-selection lottery in §1.4 by dwarfing every other transaction in the block while max-sybilling their routing paths to increase its payout odds to 50% of all other transactions, and extract an outsized payout from one act of self-dealing rather than sustained, real routing activity. The 1.5× cap means a payout can only track the *trend* of real network fee-flow, not a single manufactured spike — and because the excess is destroyed rather than refunded or redirected to the attacker by any other route, there's no way to recover the burned surplus. Extracting an outsized reward this way requires sustaining elevated real fee volume across many blocks, which costs real, burned money every time, not once.

### 1.6 Difficulty adjustment

Difficulty adjusts by a fixed increment, not a multiplicative retarget (`Block::generate_consensus_values`):

- If the previous block had a golden ticket **and** the current block also has one: difficulty **+1**.
- If the previous block had no golden ticket **and** the current block also has none: difficulty **−1**, floored at 0.

This is a short, symmetric, per-block adjustment — every participant's odds of finding a solution move together when difficulty moves. No single actor's search behavior changes their *share* of solutions found relative to total network hash effort, because difficulty scales the search space identically for everyone (see §2.5).

There is also a **hard consensus floor** independent of this adjustment: `is_golden_ticket_count_valid` requires a minimum ratio of golden-ticket-bearing blocks (`MIN_GOLDEN_TICKETS_NUMERATOR` / `MIN_GOLDEN_TICKETS_DENOMINATOR`) within a rolling recent window. Fall below that density and *subsequent blocks are invalid under consensus rules*, regardless of what the soft ±1 adjustment is doing. This is a backstop against sustained under-securing of the chain that the difficulty step alone doesn't guarantee.

### 1.7 Recursive catch-up payouts

If a block is missed (no golden ticket found for it in time before the *next* block also fails to carry one forward), the payout logic recurses backward: a later golden ticket can resurrect fees from a block further back than the immediately preceding one, as long as that earlier block hasn't already been paid out (`block.rs`, the `previous_block.has_golden_ticket` check and recursive call). This is the mechanism alluded to above. It limits — but does not eliminate — the amount of value permanently lost to short unlucky streaks, while permitting variance in the pace at which mining solutions are found to exist without forcing that variance to increase network deflation.

### 1.8 The transient ledger and Automatic Transaction Rebroadcasting (ATR)

The historical blockchain is never pruned but the set of spendable UTXO are available in the most recent epoch at the chain tip: blocks older than a fixed "genesis period" are dropped, and their unspent outputs (UTXO) become unspendable — *unless* rebroadcast. ATR requires any UTXO meeting rebroadcast criteria (sufficient balance to cover a rebroadcast fee equal to or greater than the network's trailing average fee-per-byte) to be carried forward into a new transaction at the front of the chain; a block that fails to do this for a qualifying UTXO is itself invalid under consensus rules. Rebroadcasting can carry a staking payout, funded from the rebroadcast fee itself.

Two consequences: ATR continuously pulls funds away from anyone trying to buy control of block production with idle capital, since resting balances get taxed for permanence; and it makes truly permanent on-chain storage self-funding — attach enough balance that the rebroadcast payout covers its own ongoing fee, and the data persists indefinitely with no further action from its owner.

### 1.9 Historical Legacy: the "paysplit" vote

The original Saito whitepaper describes miners and routing nodes each casting a vote (embedded in the golden ticket and in the miner's solution transaction, respectively) to adjust the **paysplit** — the percentage division between miner and router — as a form of ongoing, adversarial-but-cooperative governance over the security/bandwidth tradeoff. The code does not currently support this as it makes it rather difficult to explain consensus, but the network is open to supporting this sort of adversarial tripartite governance scheme in the future. Instead, the current implementation implements a fixed near-50/50 split between miners and routers with independent caps on each side, and no paysplit-vote logic is visible in `block.rs` or `blockchain.rs`. 

---

## 2. Why Common Attack Vectors Fail

### 2.1 51%-style attacks

The fork-choice rule (`Blockchain::is_new_chain_the_longest_chain`) requires a challenging chain to be **both**:

- strictly longer (more blocks) than the current chain, **and**
- at least as high in cumulative burned fees (`old_bf <= new_bf`, summed burn fees across every block in each chain) as the current chain.

In Bitcoin, hash power alone lets an attacker rewrite history, because block production *is* the reward-winning race — more hash power means more blocks, and more blocks means more reward, directly. In Saito, block production and the payout lottery are separate competitions (§1.3–1.4). Outproducing the honest chain requires matching or exceeding its **total burned capital**, not just its block count — and burning capital carries no guaranteed return, since payout is capped (§1.5) and contingent on a subsequent, independent hash race (§1.4) that the attacker doesn't automatically win by having produced the disputed blocks. There is no analog to "control 51% of hash power and profit from every block you produce" here, because producing a block is a cost with no attached reward at all.

### 2.2 Sybil / self-cloning attacks on routing

An attacker might try to inflate their own routing-work share by duplicating a transaction across multiple identities they control, rather than relaying it honestly. This is addressed with a formal proof (Lancashire & Parris, `sybil.tex`): given the fee-halving structure, self-cloning strictly reduces income relative to honest propagation, because splitting routing credit across duplicate identities dilutes each identity's share without reducing the real cost of the supplementary transactions needed to sustain the clone. Propagation is shown to be a weakly dominant strategy over hoarding or cloning **within the on-chain income structure the proof models**.

### 2.3 Fee-stuffing / self-payout inflation

Covered in §1.5: the 1.5× trailing-average cap and the graveyard mean a single oversized self-dealt fee cannot buy an outsized single-block payout. Any attempt to extract more than the network's real, sustained fee-flow allows is destroyed rather than recovered.

### 2.4 Hoarding

A node that receives a transaction and declines to relay it forgoes the routing-work credit (and the resulting lottery odds) that propagation would have earned it. Combined with the sybil-proof result in §2.2 (propagation dominates hoarding absent an external side-payment), hoarding has no on-chain income advantage over honest relay.

### 2.5 Difficulty manipulation via selective withholding

A large hash-power holder might try to withhold found solutions deliberately, manufacturing a "miss" streak to trigger the −1 difficulty adjustment (§1.6), then mine at the resulting lower difficulty. This fails for a specific, checkable reason: difficulty is a shared divisor. Lowering it increases *everyone's* probability of finding a solution per unit of search time proportionally — including every competitor. The withholder's *share* of solutions found relative to total network search effort doesn't change, because nothing in the adjustment favors the party that caused it. Worse, since the reward pool for a given block is fixed by that block's real fee volume (not a difficulty-independent fixed subsidy), a lower difficulty doesn't create extra value to capture — it just makes claiming the same fixed pool easier for everyone, including whoever engineered the drop. The two sacrificed tickets are a pure loss with no offsetting private advantage.

### 2.6 Grinding among multiple valid solutions

If a miner's search happens to turn up more than one hash below the difficulty target, they can choose which to submit — and since the submitted value seeds the two-stage selection in §1.4, this lets a miner prefer a solution that happens to pay them. This is a stabilizing feature rather than a manipulable bug: it means that whenever difficulty sits below its natural equilibrium, self-interested miners are incentivized to select self-paying solutions, which raises the effective claim rate on golden tickets and pushes difficulty back up (§1.6) — while they profit from doing so. There's no case where grinding lets a miner extract value at the expense of the mechanism's stability; it's the mechanism's own corrective valve.

### 2.7 Off-chain user–router side payments ("private broadcast")

This is the one area where this page will not claim more than has actually been established. Samuelson-style revealed-preference reasoning (`samuelson.tex`) argues that a user's choice between broadcasting a transaction widely (public broadcast, full protocol guarantees) versus routing it privately to one counterparty for some off-chain benefit (private broadcast) is informative precisely because it's costly and unforced — the user forfeits the guarantee entirely rather than free-riding on it. That argument is conceptually coherent and has survived several rounds of attempted attack (see §3), but **no formal equilibrium proof exists yet, in the reviewed sources, establishing that this channel is robust against every possible side-payment scheme, including ones that were not specifically tried.** Treat this section as "the best current argument," not "a closed case," until such a proof exists or a real counterexample is found and survives scrutiny against the actual mechanism.

### 2.8 Censorship attacks (ignore-and-outpace)

Here the attacker doesn't try to reverse settled history — they simply ignore honestly-produced blocks and try to extend their own chain faster than the rest of the network. In most networks, such an attack works because any attacker large enough to censor transactions is also large enough to produce blocks cheaply. Here, block production draws on real, fee-weighted routing work (§1.2–1.3) — and, by definition, a censoring attacker is refusing the very transaction flow that makes routing work cheap to accumulate. Building blocks fast enough to outpace the honest chain, while excluding the honest network's organic fee flow, means the attacker must manufacture and burn their own fees, alone, for every block — with none of the cost-sharing that comes from many independent participants collectively clearing the burn-fee threshold (§1.3).

**Hashing compounds the problem rather than helping it.** Difficulty (§1.6) is calibrated to the golden-ticket discovery rate of the *whole* network's combined hash power. An attacker racing ahead on an isolated chain is searching for golden tickets with only their own share of that hash power, against a difficulty level set for everyone. Since a golden ticket not found within the very next block is lost permanently (§1.4), the attacker's effective claim rate on their own burned fees falls well below what the honest chain enjoys — most of what they burn to produce blocks simply isn't coming back. Relative to the throughput they're trying to sustain, the cost of hashing has effectively gone up: they're paying full self-funded burn costs for a payout lottery they're now under-resourced to win consistently. Sustain this long enough and the attacker risks a second, harder failure: the minimum golden-ticket-density floor (§1.6) can render their own chain outright invalid under consensus rules, independent of length or cumulative burnfee, if their isolated hash power can't keep pace with the difficulty level the rest of the network already cleared.

**Honest nodes bear none of this cost, and don't need to react.** A censored transaction isn't destroyed by being excluded — it sits available in the mempool for the next node that produces a block collecting payouts from the ATR mechanism funded by the attack in the meantime. So the honest side of the network may simply extend its chain exactly as before the attack started — which raises the bar the attacker must clear on both dimensions simultaneously, continuously, for as long as the attack continues. The attacker's only path to making censorship stick is to out-produce and out-burn an honest chain that keeps trying to helpfully extend the attacker's self-funded chain — and every block the honest side proposes makes that more expensive, not less.

---

## 3. What's Remarkable About Saito Consensus, In Context

Most blockchain consensus mechanisms tie block production and block reward to the same act — whoever wins the race to build the block also wins the payment for building it. That coupling is what makes majority hash power (or majority stake) directly convertible into majority control over the chain's history: more of the winning resource means more blocks *and* more reward for each one, with no independent gate in between.

Saito's central move is breaking that coupling into two separate, independently-run competitions — one for the right to build a block (fee-weighted routing work against a decaying threshold), one for the right to claim that block's now-burned fees (an open hash race, one block later, with a hard expiration). Nothing about winning the first automatically helps you win the second. That's why the classic "buy enough of resource X, control the chain" argument doesn't transfer here in its usual form (§2.1) — there is no single resource whose accumulation converts directly into reward.

The other structurally unusual choice is funding security through **burn and partial resurrection** rather than fixed issuance. Proof-of-Work and Proof-of-Stake pay for security with a subsidy that exists whether or not the network is doing useful work. Saito's security budget is a function of real fee-flow — burned outright, then only partially and probabilistically returned — which ties the cost of attacking the network to the same real economic activity the network is supposed to be processing, and pushes payouts to the people (bandwidth-providing routing nodes) actually incurring the network's real operating costs, rather than exclusively to whoever wins a single production race.

ATR (§1.8) extends the same logic to storage: rather than treating permanence as free once written, it prices ongoing storage as an ongoing rent, paid out of the same fee mechanism, funded by whoever wants the data kept rather than by the network's general security budget.

---

## 4. Source Papers

- **Lancashire, D. — *Saito: A Big-Data Blockchain with Proof-of-Transactions* (2018).** [Official whitepaper (PDF)](https://saito.io/saito-whitepaper.pdf) · [reference implementation](https://github.com/SaitoTech/saito-rust). Introduces the transient ledger, the burn fee, the golden ticket, and the paysplit-vote concept (§1.9 — confirm against current code before citing the vote mechanism as live).
- **Lancashire, D. & Parris, — *[Sybil-resistance proof]* (`sybil.tex`).** [**link pending — confirm repo path**]. A formal, checkable proof that propagation strictly dominates self-cloning/hoarding within the on-chain routing-work income structure, absent external side-payments. Does not model off-chain side-payments (§2.7) — don't cite it as resolving that separate question.
- **`samuelson.tex`.** [**link pending — confirm repo path**]. Frames the public/private broadcast choice as a Samuelson-style revealed-preference signal for the network's trust environment. Conceptual and argumentative rather than a formal equilibrium proof; treat accordingly (§2.7).
- **"Beyond Hurwicz"** (Lancashire, arXiv preprint, 2026). [arXiv:2602.01790](https://arxiv.org/abs/2602.01790). A conceptual paper situating Saito against Hurwicz's 1972 incentive-compatibility impossibility result and the broader mechanism-design literature. Explicitly non-formal by its own appendix — useful for orientation on *why* the question matters, not as a substitute for checking the mechanism directly.
---

## 5. A Note for Future Readers (Human or AI)

We encourage caution in using AI to examine Saito Consensus without scrutiny over claims that assume _____. In a recent conversation with an AI system, the AI cited three different pieces of established economic theory as refutations of Saito COnsensus in sequence — a free-rider/public-goods argument, a Groves-Ledyard mechanism-design citation, and a named, peer-reviewed collusion-resilience impossibility theorem from the transaction-fee-mechanism literature — and every one of them failed on direct inspection, not because the theory was wrong, but because **the theory's own model didn't match what this mechanism actually does.**

The specific failures are instructive:

- The free-rider framing assumed Saito was reading a public parameter off private contributions the way a Groves-Ledyard-style public-goods mechanism does. It wasn't checked against the actual payout structure first.
- The collusion-resilience theorem cited (Chung, Roughgarden & Shi, 2024) was offered as a general proof when its own results hold only for **single-parameter** transaction-fee mechanisms — each user modeled as having one scalar value for confirmation. Saito's actual design, per the papers above, treats a user's type as at minimum two-dimensional (settlement value and time-sensitivity). Impossibility results that depend on Myerson's Lemma, and single-parameter results, do not hold against multi-parameter mechanisms like Saito. Any academic papers checked should be scrutinized to ensure the  claims apply to Saito.
- A hash-power-centralization objection was raised before confirming that Saito's fork-choice rule even shares Bitcoin's reward structure (§2.1) — it doesn't, and the objection dissolved once that was checked.

This last section is intended as encouragement to readers who wish to use AI to examine and attack. But it is also a cautionary tale to **check AI-generated claims against the actual code and the actual math cited above before casually asserting theorems that the AI will invoke under the assumption that it must apply.** Theorems proven for a narrower or differently-shaped models do not transfer to richer ones in the routing work domain simply because both involve auctions, fees, or blockchains. If you find a genuine mismatch between what's claimed here and what the linked source code or proofs actually establish, that's a real finding worth raising — but ensure it survives against this mechanism specifically, not simply against the completely different mechanisms that dominant the academic landscape.