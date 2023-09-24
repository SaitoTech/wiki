---
title: Golden Tickets
description: 
published: true
date: 2023-09-24T00:41:36.542Z
tags: 
editor: markdown
dateCreated: 2023-09-23T14:24:05.626Z
---

## Golden Tickets

### Intro

In Saito, Golden Ticket transactions are proofs-of-work which reference the previous block and are used to unlock that block's rewards, and the rewards of all preceding blocks since the last valid Golden Ticket.

Golden Tickets appear to solve two problems:

1. Securely selecting a winning router from a block.
2. Preventing fee-recycling attacks.

From a more general perspective, either of these problems are the same: there must exist an objective cost to determining where the rewards from a block will end up, otherwise block producers may costleslly manipulate the selection method to exploit the blockchain. This is the problem Golden Tickets solve.

### Security

If random numbers sourced from blocks chose the winner, block producers would reshuffle transactions until they produced a block which paid them, and early hop routers who do not produce blocks would never get paid. This is known as a *Grinding Attack,* and prevents methods of selecting winners where block producers are allowed to choose the inputs which determine the winner.

Likewise, if fee rewards were allowed to be unlocked costleslly, attackers could easily spend their own tokens to produce blocks and earn back their own fees, allowing them to produce such blocks indefinitely. This is a fee-recycling attack. By forcing the unlocking of funds to bear a cost, honest nodes who earn fees from users will end up in profit while nodes who use their own money to create fee-flow must lock half of it behind a costly proof-of-work.

Instead of a proof of work being required to produce a valid block, a proof of work exists in a Golden Ticket transaction and references the previous block. Block producers lose the ability to influence where the fees end up without paying, giving routers who were not involved in composing the blocks a fair shot at the routing reward.

The incentive for producing Golden Tickets is half the fee reward (the only reward in Saito) of the previous block. This Golden Ticket is required for unlocking of funds for routing nodes, because it is a costly and economically secure way to produce a valid random number which can be used to choose the winning router the other half of fee rewards will go to.

### Long-Range Attacks

In addition to providing an economically secure random number, the proofs of work required to unlock rewards forces an attacker who tries to use previously spent tokens to create a malicious fork (a long-range attack) to also spend energy to unlock those tokens and re-use them for new blocks. Even in the worst-case scenario where the attacker can convince honest miners to unlock the tokens, the attacker only gets back half each time, and quickly runs out of the capital needed to sustain the attack.

- For more information regarding Saito's economic security, consult the [attack vectors](https://wiki.saito.io/en/consensus/attack-vectors) page.