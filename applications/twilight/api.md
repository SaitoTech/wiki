---
title: Twilight Struggle - Custom Cards & API
description: Programming Custom Cards for Twilight Struggle in the Saito Game ENgine
published: true
date: 2026-11-05T06:01:58.064Z
tags: 
editor: markdown
dateCreated: 2026-11-04T08:53:25.750Z
---

# Twilight Struggle - Custom Cards

The Twilight Struggle module supports custom cards. These cards can be programmed to do anything an ordinary card can: add or remove influence, award victory points, change DEFCON, and modify other aspects of the game.

This page introduces the basic programming model, showing how to create simple cards that change the state of the board or ask players to make a choice that triggers a simple update. For cards that require more complicated forms of interactivity the techniques needed are covered in our page on more [advanced programming patterns](/applications/twilight/api/advanced). We also have a separate page with [examples for custom cards](/applications/twilight/api/examples).


## 1. The Twilight Struggle Game Queue

Twilight Struggle runs on a queue that handles [instructions](/applications/twilight/api/queue) on a last-in-first-out basis. When players make moves they share instructions with each other. The underlying game engine keeps moves in sync, and players then execute the same moves in the same order without the need for a central server to manage the game.

Programming custom cards in javascript mostly consists of learning how to determine which player is active and then asking them to make a move and broadcast their moves to other players. There are two ways of adding moves:


#### AUTOMATIC CARDS
```js
api.addToQueue("vp\tus\t2");
api.addToQueue("defcon\tlower");
return 1;
```

Use the function ```api.addToQueue()``` when everyone running the javascript should execute the same code. This adds instructions to the game queue that every player will execute. The final instruction (```return 1```) indicates that there is no need to halt the game and wait for another player to broadcast their own moves before the game can continue execution.

#### PLAYER-DRIVEN EXECUTION

In some situations, cards may need players to make choices, and those choices may affect how the card updates the board or game state. In this case, we let that specific player use the ```api.addMove()``` command and then ```api.endTurn()``` to broadcast those moves to all players, at which point they are added to the queue. These cards should ```return 0``` so that the engine halts until the move is received by all players. 

```js
if (api.isPlayer("us")) {

  const choice = await api.playerSelectOption([
    { id: "vp", label: "Increase US Victory Points by 1" },
    { id: "defcon", label: "Raise DEFCON by 2" }
  ]);

  if (choice === "vp") {
    api.addMove("vp\tus\t1");
  } else if (choice === "defcon") {
    api.addMove("defcon\traise");
    api.addMove("defcon\traise");
  }

  api.endTurn();

} else {
  api.updateStatus("US is playing a Custom Card!");
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

Please see our page filled with [example cards](/applications/twilight/api/examples) for practical suggestions on how to write custom cards. Put this code into the online card generator to create and share cards. The following example gives the US two victory points if it controls France. Otherwise, it gives the USSR two victory points.

```js
if (api.isControlled("us", "france")) {
  api.addToQueue("vp\tus\t2");
} else {
  api.addToQueue("vp\tussr\t2");
}
return 1;
```

This demonstrates the central pattern used by straightforward cards with non-forking execution:

1. check the game state.
2. use `if` and `else` to determine which effect should occur.
3. add the appropriate instructions to the queue.
4. `return 1` so the game continues immediately

Cards that require specific players to take action require forking execution where one of the players is invited to create and broadcast moves, while the second stops their queue and waits for their opponents move to arrive before they both continue.

```
const countries = [
  "burma",
  "cambodia",
  "indonesia",
  "laos",
  "malaysia",
  "philippines",
  "thailand",
  "vietnam"
];

const eligible = countries.filter(country =>
  api.isControlled("us", country)
);

if (eligible.length === 0) {
  api.updateStatus("No Southeast Asian countries have US influence.");
  return 1;
}

if (api.isPlayer("ussr")) {
  const country = await api.playerSelectCountry(
    "Select a Southeast Asian country to coup",
    eligible
  );

  api.addMove(`coup\tussr\t${country}`);
  api.endTurn();
  return 0;
}

return 0;
```

This demonstrates the central pattern used by simple cards that require only one player to make decisions:

1. check the game state / collect valid options
2. prompt a specific player to make a choice
3. use `addMove(command)` and then `endTurn()` to broadcast their move
4. `return 0` so all players wait for the move

It is possible to write much more advanced cards where players make decisions that manipulate the board state and then make choices based on those conditions. To continue looking into how we can program these events, please see our page on [advanced card creation](/applications/twilight/api/advanced).