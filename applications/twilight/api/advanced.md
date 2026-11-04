---
title: Twilight Struggle - Advanced Programming Techniques
description: 
published: true
date: 2026-11-04T13:37:11.735Z
tags: 
editor: markdown
dateCreated: 2026-11-04T12:21:40.168Z
---

# Advanced Programming Techniques for Twilight Struggle

This guide is for people who already know the basics of writing a custom Twilight Struggle. What it explains is how to build cards with richer events like Junta with choices and game changes that require more than one stage.

In this document we teach:

1. What multiple **code tabs** mean on one card
2. Why a card like **Junta** needs more than one stage
3. How the shared game **queue** connects those stages
4. How to pass simple **arguments** from stage-to-stage
5. How to read the board, check ongoing events, and offer player choices
6. What works today, and what still needs engine support


## Cards with Multiple Code Blocks

In the Card Generator, cards have create additional **code tabs** that hold a separate chunk of javascript. Those chunks allow cards to create events that will fire at different stages -- with each stage informing the game of when and how to trigger the subsequent step.

A useful mental model:

> **One card can contain several code blocks. Each block can be invoked separately as an event through the game queue. This is done by adding the NFT_EVENT instruction to the queue -- using it to tell the game engine which chunk of code to execute...**

| Idea | Meaning |
|---|---|
| card identity | The card’s unique id in the game |
| code block | One JavaScript chunk on that card |
| code index | Which chunk to run: `0` is the first tab, `1` is the second, and so on |

When a card is played normally as a event, the game runs the **first** usable code block (index `0`). That piece of code can schedule another block on the same card to run later on by adding an instruction to the queue that tells the game to execute it, providing:

- the same card ID, but
- a different code index

This second code block is still part of the card. Separating the code logic into two sequences like this allows the board to update step-by-step so that by the time the second code block is executed, every player has an updated copy of the board that reflects the earlier decision.


## Example: Junta

**Junta** is a good example because it naturally splits into two decisions:

1. Place 2 influence in Central or South America
2. Optionally choose to **coup** or **realign**

The second decision must happen **after** the influence has been applied as the first can change the conditions under which the second operates. This is why a programmable version of the card needs two code blocks:

**Code tab 1 — Place influence**

- Runs when the card is played
- Asks which country to target
- Places influence there
- Arranges for code tab 2 to run later

**Code tab 2 — Coup or realignment**

- Runs after the placement has been processed
- Looks at the updated board
- Asks whether to coup or realign
- Carries out that choice

---

## Using the Game Queue

Imagine our default code chunk asks the active player to select a country to place influence, places that influence and then submits the move to all players using the instruction `api.endTurn()`. The influence will be placed and then the game will resume with the next player's turn.

We can stop this by pushing this command onto the game queue at the start of the first code block. Once all of the subsequent commands have been processed, this instruction will tell the game engine to execute the second chunk of code:

```text
NFT_EVENT	CARD_ID	CODE_INDEX	optional_arg_0	optional_arg_1	...
```

For example, we might run the second code block on a card whose NFT ID is `my-junta-card` with:

```text
NFT_EVENT	my-junta-card	1
```

We can also pass the country into the second stage as an argument:

```text
NFT_EVENT	my-junta-card	1	cuba
```

If you use this technique to pass arguments into code blocks, you can access them within the NFT object that contains the code chunk. Inside the script, you can access these arguments as folows:

```javascript
args[0]
args[1]
args[2]
// ...
```

These instructions can be chained from code block to code block. For example, the second code block could in theory add another call to NFT_EVENT asking for yet a third code block associated with the card to run as follows:

```text
NFT_EVENT	my-junta-card	2	cuba	coup
```

The gives the code in the THIRD code block:

```javascript
args[0] // "cuba"
args[1] // "coup"
```

If no arguments are provided, `args` is an empty array.

## How about an Example:

### Code Block 1 — Ask Player to Place Influence

```javascript
const cardId = "YOUR_CARD_ID";
const faction = context.game.player === 2 ? "us" : "ussr";

const targets = [
  "mexico", "guatemala", "elsalvador", "honduras", "nicaragua",
  "costarica", "panama", "cuba", "haiti", "dominicanrepublic",
  "venezuela", "colombia", "ecuador", "peru", "chile",
  "bolivia", "argentina", "paraguay", "uruguay", "brazil"
];

const country = await api.playerSelectCountry(targets);

//
// first instruction added is last to run...
//
// so call the next code block first
//
api.add("NFT_EVENT\t" + cardId + "\t1\t" + country);

//
// then add the influence to the selected country
//
api.addToQueue("place\t" + faction + "\t" + faction + "\t" + country + "\t2");

//
// broadcast the information to other players
//
await api.endTurn();

//
// don't forget to return 0
//
return 0;
```

### Code Block 2 — Coup or Skip

```javascript
const cardId = "YOUR_CARD_ID";
const faction = context.game.player === 2 ? "us" : "ussr";
const country = args[0];

const choice = await api.playerSelectOption([
  { id: "coup", label: "Coup" },
  { id: "skip", label: "Skip military action" }
]);

if (choice === "skip") {
  api.addToQueue("NOTIFY\tJunta skips the free military action");
  await api.endTurn();
  return 0;
}

api.addToQueue(
  "NOTIFY\tJunta triggers a  now " + choice +
  " in Central or South America (military follow-up not yet available to NFT cards)"
);

await api.endTurn();
return 0;
```


## Reading the Board / State

Your script receives a read-only snapshot as `context.game`. Changing properties on `context.game` does nothing to the real game, but you can check the value of almost anything the game tracks:

```
// which turn is it?
const turn = context.game.turn;

// which round of play is this?
const round = context.game.round;

// how many victory points does each side have?
const vp = context.game.vp;

// what is the current DEFCON level?
const defcon = context.game.defcon;

// how much influence does Italy have?
const influence = context.game.countries["italy"];

// what events are active?
const events = context.game.events;
```

Functions exist to simplify the most common checks:

```javascript
api.isControlled("us", "canada")   // 1 or 0
api.whoControls("egypt")          // "us", "ussr", or ""
api.isEventActive("reformer")     // 1 when that ongoing event is active
```

### Simple example

```javascript
const cardId = "YOUR_CARD_ID";
if (api.isPlayer(api.returnActivePlayer()) {

    const country = await api.playerSelectCountry(["egypt", "libya", "israel"]);

    if (api.isEventActive("reformer") == 1) {
        api.addMove("place\tus\tus\t" + country + "\t2");
    } else {
        api.addMove("place\tus\tus\t" + country + "\t1");
    }

    await api.endTurn();
}
return 0;
```


## Asking the player to choose

Two helpers are available for interactive cards:

```javascript
const option = await api.playerSelectOption([
  { id: "india", label: "India" },
  { id: "pakistan", label: "Pakistan" }
]);

const country = await api.playerSelectCountry(["cuba", "mexico", "panama"]);
```

These do **not** change the board by themselves. They offer whatever player is executing that javascript a menu and ask them to choose between the options, returning the value provided in the ```id``` field.

### When would I need this?

- The card text says “choose a country”
- The player must pick between two branches
- You want a menu before placing influence

### Pattern

1. identify the player that needs to respond
2. use an if/else branch so only that player executes #3 and #4
3. use the answer with api.addMove()
4. Call `await api.endTurn()`
5. `return 0`

--- 

## Permanent Effects / Events

Twilight keeps “this effect is still in play” markers that your script can read:

```javascript
api.isEventActive("nato")
api.isEventActive("marshall")
api.isEventActive("reformer")
```

### What this lets you do

Make a card behave differently depending on whether an earlier event is still active. If you need to set events or remove them, use the functions:

```
api.setActiveEvent("my-custom-event")
api.removeActiveEvent("my-custom-event");
```

## Troubleshooting

Saito is a community project. Many devs and players congregate around RedSquare. Feel welcome to post questions or suggestions there.