---
title: the general grevious attack
description: 
published: true
date: 2024-11-27T05:46:55.969Z
tags: 
editor: markdown
dateCreated: 2024-11-27T05:19:30.273Z
---

# The General Grievous Attack

![general_grievous.webp](/general_grievous.webp)*Written by David Lancashire on August 21, 2024*

The opening battle in *Revenge of the Sith* involves a spectacular piece of double-intrigue by Chancellor Palpatine, who arranges his own abduction at the hands of General Grievous to create the pretext for a military escalation against the Separatists and his own ascension to Galactic Emperor. The move is also steeped in dramatic irony—the villains are attacking the Republic by running away and leaving it in peace.

This is why we use the term "General Grievous Attack" at Saito to describe the hardest variant of the 51% attack to solve—the version where the bad guys just ignore the good guys, refusing to relay their messages or even include any transactions forwarded by them that might trigger routing payouts to other nodes.

This makes the attack impossible to punish in proof-of-work and proof-of-stake mechanisms under majoritarian conditions. Our attackers are not producing fewer blocks after the attack than before. They are not processing fewer fees. And they are still producing blocks faster than their honest counterparts while controlling all the "votes" that determine who gets paid—so how can it be less profitable for them to produce blocks?

In this blog post, we'll show how "routing work" solves the General Grievous Attack. And in the spirit of generosity, we'll do it while giving our attackers a formidable 75% of all first-hop routing work, 100% of network hashpower, and 100% of the ATR payout. Other consensus mechanisms have long since collapsed. But routing work continues to function.

To see how, assume our blockchain processes $100 in fees per block. Our pre-attack payouts are as follows:

| **Routing**     | **50 USD** |
|------------------|------------|
| **Staking (ATR)**| **25 USD** |
| **Mining**       | **25 USD** |

The mining payout consumes its reward in energy costs, making the attacker's pre-attack income $62.50:

| **Routing**     | **37.5 USD** |
|------------------|-------------|
| **Staking (ATR)**| **25 USD**  |
| **Mining**       | **0 USD**   |

Right away, we can see why cooperating with honest nodes is beneficial to the attacker. Were our attacker to produce a chain with only the transaction fees they are collecting, they would lose 25% of their $75 in mining costs and earn only $56.25. But their results are even worse under the General Grievous Attack. Consider the changes:

- **Routing Payout:** Attackers collect 100% of all routing payouts, but with fee-throughput at only $75, their expected income is $37.50.
- **Mining Payout:** It still costs $25 to find a golden ticket, but mining payout has dropped to $18.75. The attacker loses $6.25 per block.
- **Staking Payout:** Censoring honest transactions gradually increases the percent of ATR payouts that flow to them. Attacker income falls.

Post-attack income is consequently:

| **Routing**     | **37.5 USD** |
|------------------|-------------|
| **Staking (ATR)**| **0–25 USD** |
| **Mining**       | **-6.25 USD** |

Attackers have gone from earning $62.50 per block to somewhere between $31.25 and $56.25. Not only is attacking irrational, but it is even provably costly in any network where infrastructure providers pay competitive rates for inbound fee-flow. And any rational users can increase this cost-of-attack further simply by withholding their transaction flow or sending it to another node.

## Advanced Commentary on Asymmetricality

Our attacker blockchain will eventually settle into a lower-fee equilibrium. Once enough golden tickets go unsolved (burning the routing payout for good), mining difficulty will drop. And as censored transactions join the ATR loop, their fees will help buffer some of the collapse in fee-throughput. But losses are suffered during the transition and borne by the attacker who proposes the blocks during this period.

Cost-of-attack can be increased further by having consensus observe and punish any drop in new fee throughput, expansion in the set of UTXO subject to rebroadcasting, or any sharp increase in aggregate routing work by simply burning a portion of the fees collected during this period before payouts are calculated. This conditional-burning is a second type of asymmetrical tax, as it does not affect honest block producers cooperating in equilibrium.

The symmetrical attacks of proof-of-work and proof-of-stake vanish. We transcend them by shifting away from "voting systems" where any majority can impose costs on any minority and towards an efficiency tax powered by a fee-unlock "flywheel" that punishes nodes who push the network into a less efficient state. All nodes will rationally spin up the flywheel if they have access to third-party fees. More fees mean more blocks for them and greater profits.

But attackers? Because attackers are deliberately orphaning efficiently-produced work, they must either spend and burn their own money to maintain the network in a state of artificial efficiency (burning their own money to avoid greater losses) or accept the cost of slowing the flywheel by letting it consign a quantifiable amount of the fees they are contributing to oblivion.

In this way, routing work achieves a quantifiable and asymmetrical cost-of-attack that punishes attackers without introducing symmetrical attack vectors on honest minority nodes. Problems unsolvable in the old system melt away in the new paradigm. When General Grievous threatens to abandon ship, the best strategic move is simply to let them go.
