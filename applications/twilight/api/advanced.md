---
title: Twilight Struggle - Advanced Programming Techniques
description: 
published: true
date: 2026-11-04T12:43:33.657Z
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
// first instruction on the queue is the last to run...
//
// so we call our next code block first
//
api.addToQueue("NFT_EVENT\t" + cardId + "\t1\t" + country);

//
// and then add the influence to the selected country
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

### Code Block 2 — Coup or realignment

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

### A version you can experiment with today

Until stage scheduling is permitted from NFT scripts, keep the teachable Junta decisions in **one** code tab. You will not get a true post-queue board refresh between the two choices, but you can still practice selection, placement, and branching:

```javascript
const cardId = "YOUR_CARD_ID";
const faction = context.game.player === 2 ? "us" : "ussr";

const country = await api.playerSelectCountry([
  "cuba", "mexico", "panama", "nicaragua",
  "venezuela", "brazil", "chile", "argentina"
]);

const followUp = await api.playerSelectOption([
  { id: "military", label: "Plan a free coup or realignment next" },
  { id: "skip", label: "Influence only" }
]);

api.addToQueue("resolve\t" + cardId);
api.addToQueue(
  "NOTIFY\tJunta places in " + country +
  (followUp === "military"
    ? " and wants a military follow-up"
    : " only")
);
api.addToQueue("place\t" + faction + "\t" + faction + "\t" + country + "\t2");

await api.endTurn();
return 0;
```

Use the two-tab design when you are learning the staging model. Use the single-tab version when you want something you can run with today’s permissions.

---

## Reading the board before you act

Your script receives a read-only snapshot as `context.game`.

Changing properties on `context.game` does nothing to the real game. Treat it as information, not as a place to store results.

Useful questions the API can answer directly:

```javascript
api.isControlled("us", "canada")   // 1 or 0
api.whoControls("egypt")          // "us", "ussr", or ""
api.isEventActive("reformer")     // 1 when that ongoing event is active
```

### When would I need this?

- Only place influence if a country is uncontrolled
- Give a bonus if an ongoing event like Reformer is active
- Tell the player something about the current board before they choose

### Simple example

```javascript
const cardId = "YOUR_CARD_ID";
const country = await api.playerSelectCountry(["egypt", "libya", "israel"]);

if (api.whoControls(country) === "ussr") {
  api.addToQueue("NOTIFY\tCannot place into USSR-controlled " + country);
} else if (api.isEventActive("reformer") == 1) {
  api.addToQueue("place\tus\tus\t" + country + "\t1");
} else {
  api.addToQueue("place\tus\tus\t" + country + "\t2");
}

api.addToQueue("resolve\t" + cardId);
await api.endTurn();
return 0;
```

### Knowing which side you are

Prefer the seat number on the snapshot:

```javascript
const isUs = context.game.player === 2;
const isUssr = context.game.player === 1;
```

In Twilight Struggle seating, player `1` is USSR and player `2` is US.

---

## Asking the player to choose

Two helpers are available for interactive cards:

```javascript
const option = await api.playerSelectOption([
  { id: "india", label: "India" },
  { id: "pakistan", label: "Pakistan" }
]);

const country = await api.playerSelectCountry(["cuba", "mexico", "panama"]);
```

These do **not** change the board by themselves. They only wait for a HUD choice, then your script decides which instructions to enqueue.

### When would I need this?

- The card text says “choose a country”
- The player must pick between two branches
- You want a menu before placing influence

### Pattern

1. Ask the question with `await`
2. Branch on the answer
3. Queue the resulting moves
4. Call `await api.endTurn()`
5. `return 0`

```javascript
const cardId = "YOUR_CARD_ID";
const choice = await api.playerSelectOption([
  { id: "canada", label: "Canada" },
  { id: "egypt", label: "Egypt" }
]);

api.addToQueue("place\tus\tus\t" + choice + "\t2");
api.addToQueue("resolve\t" + cardId);
await api.endTurn();
return 0;
```

---

## Ongoing events and lasting effects

Twilight keeps “this effect is still in play” markers that your script can read with:

```javascript
api.isEventActive("nato")
api.isEventActive("marshall")
api.isEventActive("reformer")
```

### What this lets you do

Make a card behave differently depending on whether an earlier event is still active.

### What you cannot do yet from NFT scripts

There is no supported way for an NFT script to turn a custom lasting flag on or off. You can **read** existing event flags. You cannot currently create your own lasting marker from sandbox code.

So:

- Branching on Reformer / NATO / Marshall → yes
- Inventing a new lasting “Global Initiative” flag from an NFT card → not available yet

---

## Working with the queue

### The basic habit

Almost every finished card stage looks like this:

```javascript
api.addToQueue("place\tus\tus\tegypt\t2");
api.addToQueue("resolve\tYOUR_CARD_ID");
await api.endTurn();
return 0;
```

- `addToQueue` validates the instruction and records it for submission
- `endTurn` sends those instructions into the shared game
- `return 0` tells the queue processor to pause while that turn is handled

### Instructions NFT scripts may use today

- `place` — place influence
- `resolve` — finish / clear the card’s event entry
- `NOTIFY` / `notify` — show a message
- `RESOLVE`
- `ACKNOWLEDGE`

If you try to add something else, `addToQueue` throws “not permitted”.

### Why `place` feels immediate

For `place`, the acting player’s influence is applied locally right away, then the same instruction is submitted so opponents update once. The format is:

```text
place	origin	faction	country	amount
```

You can write either faction in the origin field; the game rewrites origin to the acting player’s faction for you.

---

## Common mistakes

1. **Treating a title slug or printed card number as the NFT ID**  
   The instruction needs the card’s real NFT ID in the game.

2. **Confusing the card ID with the code index**  
   The ID selects the card object. The index selects which code tab on that card to run.

3. **Calling a second code tab as a normal JavaScript function**  
   Opponents will not follow that. Later stages must be scheduled as game work.

4. **Expecting unsupported commands to work**  
   Coup, realignment, DEFCON, VP, space race, and custom lasting flags are not currently available through the NFT queue permissions.

5. **Forgetting `resolve` after a normal card play**  
   Most finished events should resolve the card they belong to.

6. **Assuming a second code tab exists when only one tab has code**  
   A single filled tab is stored as one script. Index `1` only exists when you actually created a second code tab.

7. **Editing `context.game` and expecting the board to change**  
   Use `addToQueue` for real game changes.

8. **Returning the wrong value after player input**  
   After `endTurn()`, return `0` so the queue can wait.

---

## Quick status for card authors

| Goal | Status for NFT card scripts |
|---|---|
| Several code tabs on one card | Supported in the Card Generator |
| First tab runs on normal card play | Works |
| Engine can run a later tab via `NFT_EVENT` | Supported by the engine |
| NFT script can enqueue `NFT_EVENT` | Not available yet |
| Pass `args[0]`, `args[1]`, … into a later stage | Supported when `NFT_EVENT` runs |
| Place influence | Works |
| Player menus / country selection | Works |
| Read control and ongoing events | Works |
| Create custom lasting flags | Not available yet |
| Coup / realignment / free ops from NFT scripts | Not available yet |

---

## Where to go next

- Start with a one-tab card that places influence and resolves
- Add a player choice
- Add a condition based on control or an ongoing event
- Study the Junta staging model when your card needs a decision **after** the board has changed
- Keep unsupported military or lasting-effect ideas as design notes until those permissions exist

The goal is not to memorize the engine. The goal is to recognize the pattern:

**choose → inspect the board → queue allowed instructions → end the turn → return 0**

and, for richer cards:

**stage 1 changes the board → the queue continues → stage 2 decides based on the result**