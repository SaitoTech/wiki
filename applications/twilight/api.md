---
title: Twilight Struggle - Custom Cards & API
description: Programming Custom Cards for Twilight Struggle in the Saito Game ENgine
published: true
date: 2026-11-04T10:25:16.581Z
tags: 
editor: markdown
dateCreated: 2026-11-04T08:53:25.750Z
---

# Twilight Struggle - Custom Cards

The Twilight Struggle module supports custom cards. These cards can be programmed to do anything an ordinary card can: add or remove influence, award victory points, change DEFCON, and modify other aspects of the game.

This page introduces the basic programming model and shows how to create straightforward custom card effects. More complicated programming patterns involving asynchronous combinations are covered in our advanced programming tutorial.


## 1. The Twilight Struggle Game Queue

Twilight Struggle runs on a queue that manages game instructions. When players make moves they share instructions with each other that are added to this queue. All playesr then execute the same moves in the same order while the game stays in sync as instructions are executed and removed from the queue.

The queue operates on a **last-in, first-out (LIFO)** basis: the last instruction added is the first one executed. Programming cards in javascript mostly consists of learning how to add these instructions to the game queue. There are two ways of adding moves:


#### SHARED EXECUTION
```js
api.queueMove("vp\tus\t2");
api.queueMove("defcon\tlower");
return 1;
```

Use the function ```api.queueMove()``` when everyone running the javascript should take the same action. This adds moves to the game queue of everyone running the code and does not require any player to broadcast the moves. The final instruction (```return 1```) indicates that there is no need to wait for a player to broadcast instructions before the game queue can continue executing its next instruction.

#### CONDITIONAL EXECUTION

In some situations, only certain players may need to add instructions, or the code may ask some players to make choices which affect which instructions are added to the queue. In this case, add the ```api.addMove()``` command and then ```api.endTurn()``` to broadcast. The code should then ```return 0``` so that it halts until the move is received by all players. 

```js
if (api.isPlayer("us")) {

  const choice = await api.playerSelectOption([
    { id: "vp", label: "Increase US Victory Points by 1" },
    { id: "defcon", label: "Raise DEFCON by 2" }
  ]);

  if (choice === "vp") {
    api.addToQueue("vp\tus\t1");
  } else if (choice === "defcon") {
    api.addToQueue("defcon\traise");
    api.addToQueue("defcon\traise");
  }

  api.endTurn();

} else {
  api.updateStatus("US is choosing a Custom Card option!");
}

return 0;
  ```

For help creating more advanced cards, we recommend our page on advanced card programming. This includes information on how to create permanent events, how to write cards that create new instructions which can be run on the queue and more.


## 2. Basic QUEUE Api

### Victory Points

```js
// Give the US 2 victory points
api.addMove("vp\tus\t2");

// Give the USSR 3 victory points
api.addMove("vp\tussr\t3");

// Subtract 1 victory point from the US
api.addMove("vp\tus\t-1");
```

### DEFCON

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