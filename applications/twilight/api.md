---
title: Twilight Struggle - Custom Cards & API
description: Programming Custom Cards for Twilight Struggle in the Saito Game ENgine
published: true
date: 2026-11-04T08:53:25.750Z
tags: 
editor: markdown
dateCreated: 2026-11-04T08:53:25.750Z
---

# Twilight Struggle - Custom Cards

The Twilight Struggle module on Saito supports custom cards. A custom card can do anything an ordinary card does: add or remove influence, award victory points, change DEFCON, and modify other aspects of the game. To get started building cards visit the [Saito TS Card Generator](https://saito.io/tscardgen) module or any other node running the software.

This page introduces the basic programming model and shows how to create straightforward custom card effects. More complicated programming patterns involving asynchronous combinations are covered in our advanced programming tutorial.


## 1. The Twilight Struggle Game Queue

Twilight Struggle runs on a queue that manages game instructions. Players share instructions with each other that update the game queue and execute each instruction in the same order. The game stays in step as instructions are executed and removed from the queue one-by-one.

The queue operates on a **last-in, first-out (LIFO)** basis: the last instruction added is the first one executed. Programming cards in javascript mostly consists of learning how to add these instructions to the game queue. For example:

```js
api.addMove("vp\tus\t2");
api.addMove("defcon\tlower");
return 1;
```

The DEFCON instruction is added last, so it executes first. Order-of-execution matters when a card needs to perform several effects in a particular order. You must add the instructions in the reverse of the order in which you want them to execute.

## 2. Important:

When you are writing cards, you have to specify. Use "return 1" if you want the game to automatically continu
The basic way to create a game effect is to add an instruction with `api.addMove()`.

Here are examples of some common instruction formats.

### Add or subtract victory points

```js
// Give the US 2 victory points
api.addMove("vp\tus\t2");

// Give the USSR 3 victory points
api.addMove("vp\tussr\t3");

// Subtract 1 victory point from the US
api.addMove("vp\tus\t-1");
```

### Change DEFCON

```js
// Lower DEFCON
api.addMove("defcon\tlower");

// Raise DEFCON
api.addMove("defcon\traise");
```

### Add influence

Influence instructions identify the originating faction, the faction receiving the influence, the country, and the amount.

```js
// Example: add 2 US influence in West Germany
api.addMove("place\tus\tus\twestgermany\t2");
```

The country name must use its internal game identifier, not its display name.

**Important:** The native `place` and `remove` handlers have special handling for the client that originates the instruction. The API implementation must account for this so that the effect is applied correctly on both the originating client and the other clients. See the API reference for the distinction between instruction types.

### Remove influence

```js
// Example: remove 1 USSR influence from Cuba
api.addMove("remove\tus\tussr\tcuba\t1");
```

As with placement, use the internal country identifier.

## 3. When does the card's code run?

A custom card's script runs when its event is triggered.

The script is executed on the designated player's client. The other players do not independently execute the NFT's JavaScript. Instead, they receive and process the instructions submitted by the acting player.

This has an important consequence: **the card's script should normally make decisions for the acting player, then submit the resulting instructions to the queue.**

For example, suppose a card gives the US two victory points if the US is controlling France. The script can check the game state and decide which instruction to submit:

```js
if (api.isControlled("us", "france")) {
  api.addMove("vp\tus\t2");
} else {
  api.addMove("vp\tussr\t2");
}

api.endTurn();
```

The example illustrates the basic structure: inspect the game state, choose the appropriate effect, and submit the instructions.

The game state should be checked using the supported API functions and read-only game context described in the API reference.

## 4. Submitting the card's instructions

Once the script has added all its instructions, it calls:

```js
api.endTurn();
```

This submits the constructed instructions so that the other clients can process them.

Remember that `endTurn()` submits the instructions; it does not mean that every pending queue item or card event is automatically resolved. The card execution system also has an event-resolution step. The normal NFT event lifecycle handles this as part of completing the card.

## 5. A complete simple example

The following example gives the US two victory points if it controls France. Otherwise, it gives the USSR two victory points.

```js
if (api.isControlled("us", "france")) {
  api.addMove("vp\tus\t2");
} else {
  api.addMove("vp\tussr\t2");
}

api.endTurn();
```

This demonstrates the central pattern used by straightforward custom cards:

1. Check the current game state.
2. Use `if` and `else` to determine which effect should occur.
3. Add the appropriate instructions to the queue.
4. Submit the instructions.

## 6. What this guide does not cover

This introduction covers effects that can be determined when the card script runs and submitted as a straightforward set of queue instructions.

Some cards require more complicated behavior. For example:

- Making a second decision after seeing the result of a coup.
- Repeatedly asking a player to choose another country based on an earlier result.
- Building an event whose later effects depend on the outcome of earlier queue instructions.
- Managing complicated sequences of player interaction and queue execution.

These patterns require a more advanced understanding of the game engine and queue. They are intentionally left for the advanced programming guide.

For the initial stage, concentrate on reading the game state, choosing an effect with ordinary JavaScript, and submitting straightforward queue instructions.