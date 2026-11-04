---
title: Twilight Struggle - Custom Cards & API
description: Programming Custom Cards for Twilight Struggle in the Saito Game ENgine
published: true
date: 2026-11-04T14:00:41.215Z
tags: 
editor: markdown
dateCreated: 2026-11-04T08:53:25.750Z
---

# Twilight Struggle - Custom Cards

The Twilight Struggle module supports custom cards. These cards can be programmed to do anything an ordinary card can: add or remove influence, award victory points, change DEFCON, and modify other aspects of the game.

This page introduces the basic programming model and shows how to create straightforward custom card effects. More advanced programming patterns are covered in our [advanced programming guide](/applications/twilight/api/advanced). Full examples in our page for [sample code for custom cards](/applications/twilight/api/examples).


## 1. The Twilight Struggle Game Queue

Twilight Struggle runs on a queue that handles [instructions](/applications/twilight/api/queue) on a last-in-first-out basis. When players make moves they share instructions with each other. The underlying game engine keeps moves in sync, and players then execute the same moves in the same order without the need for a central server to manage the game.

Programming custom cards in javascript mostly consists of learning how to determine which player is active and then asking them to make a move and broadcast their moves to other players. There are two ways of adding moves:


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


## 2. Essential Api Instructions

The following functions are available to cards through the api.* object. Functions marked by * should only be used in code that restricts execution to one player and has that player broadcast the move and then returns 0.

| Function | Description |
|---|---|
| `api.isPlayer(faction)` | Returns `true` if the player executing the NFT belongs to the specified faction (`"us"` or `"ussr"`). |
| `api.isControlled(faction, country)` | Returns `true` if the specified faction controls the country. |
| `api.whoControls(country)` | Returns the faction that currently controls the specified country. |
| `api.isEventActive(event)` | Returns `true` if the specified Twilight Struggle event is currently active. |
| `*api.playerSelectOption(options)` | Displays a selection menu in the HUD and asynchronously returns the ID of the option selected by the player. |
| `*api.playerSelectCountry(countries)` | Allows the player to select a country through the HUD and asynchronously returns the selected country. |
| `api.addToQueue(instruction)` | Adds a validated native game instruction to the game queue. |
| `*api.endTurn()` | Submits the instructions accumulated by the NFT script for processing through the normal game queue. |
| `api.updateStatus(message)` | Displays a status message to the player through the game interface. |

## 3. Essential QUEUE Instructions

| Queue Instruction | Arguments and Format | Description |
|---|---|---|
| `defcon` | `defcon\t{raise\|lower}` | Raises or lowers DEFCON by one level. |
| `vp` | `vp\t{faction}\t{amount}` | Adds victory points to the specified faction (`us` or `ussr`) by the given amount. |
| `place` | `place\t{origin}\t{faction}\t{country}\t{amount}` | Places the specified amount of influence for a faction in a country, with the origin identifying the source of the instruction. |
| `remove` | `remove\t{origin}\t{faction}\t{country}\t{amount}` | Removes the specified amount of influence for a faction from a country. |
| `milops` | `milops\t{faction}\t{amount}` | Changes the specified faction's military operations total by the given amount. |
| `stability` | `stability\t{player}\t{country}\t{amount}` | Changes the stability value of the specified country by the given amount. |
| `discard` | `discard\t{faction}\t{card_id}` | Discards the specified card for the specified faction. |
| `DEAL` | `DEAL\t1\t{player_number}\t{count}` | Deals the specified number of cards to the specified player. |
| `SAFEDEAL` | `SAFEDEAL\t1\t{player_number}\t{count}` | Deals cards using the safe-deal instruction. |
| `coup` | `coup\t{faction}\t{country}\t{operations}\t{card_id}` | Initiates a coup in the specified country for the specified faction, using the given operations value and optional card ID. |
| `realign` | `realign\t{faction}\t{country}` | Initiates a realignment roll in the specified country for the specified faction. |

For a full description of all commands that are currently supported see the full API documentation. To learn how to write custom cards that can add their own instructions to the queue for advanced features, please see our page on advanced card programming.


## 4. More Examples and Sample Code

The following example gives the US two victory points if it controls France. Otherwise, it gives the USSR two victory points.

```js
if (api.isControlled("us", "france")) {
  api.addToQueue("vp\tus\t2");
} else {
  api.addToQueue("vp\tussr\t2");
}
return 1;
```

This demonstrates the central pattern used by straightforward custom cards:

1. Check the current game state.
2. Use `if` and `else` to determine which effect should occur.
3. Add the appropriate instructions to the queue.
4. Submit the instructions.

For more complicated examples, please see our advanced programming guide and list of working examples you can use out-of-the-box.

