---
title: Saito Consensus - Implementation Details
description: 
published: true
date: 2025-11-23T13:09:17.825Z
tags: 
editor: markdown
dateCreated: 2025-11-23T13:09:17.825Z
---

## Saito Consensus Implementation Details

The description of Saito Consensus offered as our starting point for understanding the mechanism is a "pure" version that has several drawbacks: deflation is required to maintain security in equilibrium, cash-only attacks are possible, and extremely rich attackers may try to bias lottery payouts through strategies that radically increase the amount of SAITO passing through the lottery.

These problems can be mitigated with the following modifications, which are implemented by having consensus:

* require all valid chains to contain N golden tickets over the last M blocks. This prevents cash-only attacks at the cost of letting attackers slow the network down if they are capable of driving up mining difficulty artificially and then withholding hash to slow block production.

* require block producers to affix tokens to blocks when proposing them, permitting the identification of attacker-held tokens and their slashing in the event of a social fork. This provides a deterrence to cash-only attacks.

* calculate the winner of block (N-1) as in our [description](/consensus) of consensus, but if block (N-1) did not contain a golden ticket recurse backwards to issue a router payout for the second unpaid block (N-2), while distributing the miner payout for this second block in a special ATR treasury. this prevents deflation caused by variance in the speed at which mining solutions can be found. it may theoretically make the tip block in the blockchain less stable.

* issue the funds in the ATR treasury as payments to unspent UTXO as part of the ATR mechanism described in the next section. If these unspent UTXO are well distributed (not fully controlled by the attacker), the ATR payout further increases cost-of-attack on the network as any attacker who is spending their own tokens must necessarily redirect a portion of their own wallet to any users whose transactions they are censoring.

* maintain a smoothed average of the fees included in each block over the last epoch in the block header. In the event that any router payout spikes well in excess of this average (1.5x in production) cap payout at this level. This prevents an edge-case attack on the payout lottery attackers willing to flood the network with massive amounts of their own deep-routed tokens to marginally improve their payout odds.

* affix cryptographic routing signatures to blocks to permit nodes to identify and deprioritize messages from other nodes which have been observed to violate routing policies.
