---
title: Twilight Struggle - Custom Cards & API
description: Programming Custom Cards for Twilight Struggle in the Saito Game ENgine
published: true
date: 2026-11-13T17:13:46.828Z
tags: 
editor: markdown
dateCreated: 2026-11-04T08:53:25.750Z
---

# Twilight Struggle - Custom Cards

Twilight Struggle custom cards can be programmed to do anything an ordinary card can: add or remove influence, award victory points, change DEFCON, adjust milops, or modify any other aspect of the game, even changing which countries are battlegrounds and their stability values.

This page explains how to create simple cards. We start with simple examples before moving on to complicated forms of interactivity in our page on more [advanced programming patterns](/applications/twilight/api/advanced). We also have a separate page with [working examples](/applications/twilight/api/examples) of how to write custom cards that perform regular tasks.


## 1. The Twilight Struggle Game Queue

Twilight Struggle runs a queue that processes [instructions](/applications/twilight/api/queue) on a last-in-first-out basis. When players make moves they share instructions with each other. The underlying game engine keeps these instructions in sync, and players then execute them in the same order without the need for a central server to manage the game.

The simplest cards add instructions directly to the queue, as in the following, which increases US VP by 2 and then lowers defcon.


#### AUTOMATIC EXECUTION
```js
api.addToQueue("vp\tus\t2");
api.addToQueue("defcon\tlower");
return 1;
```

Use the function ```api.addToQueue()``` when everyone running the javascript should execute the same code simultaneously. The final instruction (```return 1```) indicates there is no need to halt the game and wait for a player to broadcast their own moves before the game can continue execution.

**IMPORTANT**
- use `api.addToQueue()` with `return 1`
- use `api.addMove()` and `api.endTurn()` with `return 0`;


#### PLAYER-DRIVEN EXECUTION

Many cards require a specific player to make decisions. These cards should ```return 0``` so that all players will wait until the move is broadcast before continuing the game. The queue can still be used in these situations, but in this case the active player should use the ```api.addMove()``` and then ```api.endTurn()``` functions to queue and then broadcast its moves.

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


## 2. Placing Influence, Coups and Realignments

We recommend using the following coding patterns for placing influence, making coups, and triggering realignments. To place influence use the function `api.playerPlaceInfluence()`:

```
if (api.isPlayer("us")) {
  await api.playerPlaceInfluence("egypt", 2, "us");
  await api.endTurn();
}
return 0;
```

Removing influence should use the function `api.playerRemoveInfluence()`:

```
if (api.isPlayer("us")) {
  await api.playerRemoveInfluence("egypt", 3, "ussr");
  await api.endTurn();
}
return 0;
```

Realignments should use the `api.playerRealign()` function:

```
if (api.isPlayer("ussr")) {
  await api.playerRealign("canada");
  await api.endTurn();
}
return 0;
```

Coups can be added to the queue as standard moves:
  
```
if (api.isPlayer("ussr")) {
  await api.addMove("coup\tus\tmexico\t2\tjunta");
  await api.endTurn();
}
return 0;
```
  

To trigger a coup use the function `api.playerPlayCoup()`:


```
if (api.isPlayer("us")) {
  await api.playerPlaceInfluence("egypt", 2);
  await api.endTurn();
}
return 0;
```

## 3. Essential API Functions

The following functions are available to cards through the api.* object. Functions marked by * should only be used in code that restricts execution to one player and has that player broadcast the move and then returns 0.

| Function | Description |
|---|---|
| `api.isPlayer(faction)` | Returns `true` if the player executing the NFT belongs to the specified faction (`"us"` or `"ussr"`). |
| `api.isControlled(faction, country)` | Returns `true` if the specified faction controls the country. |
| `api.whoControls(country)` | Returns the faction that currently controls the specified country. |
| `api.isEventActive(event)` | Returns `true` if the specified Twilight Struggle event is currently active. |
| `*api.playerSelectOption(options)` | Displays a selection menu in the HUD and asynchronously returns the ID of the option selected by the player. |
| `*api.playerSelectCountry(countries)` | Allows the player to select a country through the HUD and asynchronously returns the selected country. |
| `api.playerRealign(country)` | Realignment attempt, must be followed by api.endTurn() |
| `api.playerPlaceInfluence(country, num, faction)` | add influence to country, must be followed by api.endTurn() |
| `api.playerRemoveInfluence(country, num, faction)` | remove influence from country, must be followed by api.endTurn() |
| `api.addToQueue(instruction)` | Adds a validated native game instruction to the game queue. |
| `*api.endTurn()` | Submits the instructions accumulated by the NFT script for processing through the normal game queue. |
| `api.updateStatus(message)` | Displays a status message to the player through the game interface. |

## 4. Essential QUEUE Instructions

| Queue Instruction | Arguments and Format | Description |
|---|---|---|
| `defcon` | `defcon\t{raise\|lower}` | raises or lowers DEFCON  |
| `vp` | `vp\t{faction}\t{amount}` | faction gains victory points |
| `milops` | `milops\t{faction}\t{amount}` | Changes the specified faction's military operations total by the given amount. |
| `stability` | `stability\t{player}\t{country}\t{amount}` | Changes the stability value of the specified country by the given amount. |
| `discard` | `discard\t{faction}\t{card_id}` | Discards the specified card for the specified faction. |
| `DEAL` | `DEAL\t1\t{player_number}\t{count}` | Deals the specified number of cards to the specified player. |
| `coup` | `coup\t{faction}\t{country}\t{operations}\t{card}` | Initiates a coup in the specified country for the specified faction, using the given operations value from card. |

See our page on Twilight Struggle queue instructions for an [exhaustive live](/applications/twilight/api/queue) of all possible instructions. Saito's TS module is a community project and it is reasonably easy to add more commands, so feel welcome to reach out if you need functionality that does not currently exist.


## 5. A Cookbook with Examples and Sample Code

We have a page filled with [examples](/applications/twilight/api/examples) of working code for various custom cards. The following example demonstrates the central pattern used by straightforward cards with non-forking execution: give the US two victory points if it controls France, or otherwise give the USSR two victory points.

```js
if (api.isControlled("us", "france")) {
  api.addToQueue("vp\tus\t2");
} else {
  api.addToQueue("vp\tussr\t2");
}
return 1;
```

For a more complicated example, some cards require specific players to take action and broadcast moves, while the second stops their queue and waits for their opponents move to arrive before they both continue.

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
}

return 0;
```

It is possible to write much more advanced cards where players make decisions that manipulate the board state and then make choices based on the outcomes of those decisions. For practical advice on programming these more complicated events, please see our page on [advanced card creation](/applications/twilight/api/advanced).