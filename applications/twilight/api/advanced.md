---
title: Twilight Struggle - Advanced Programming Techniques
description: 
published: true
date: 2026-11-04T12:21:40.168Z
tags: 
editor: markdown
dateCreated: 2026-11-04T12:21:40.168Z
---

# Advanced Programming Techniques for Twilight Struggle

This guide is for people who already know the basics of writing a card script — `api`, `context`, `addToQueue`, and `endTurn` — and want to build richer events: choices, conditions, and cards that happen in more than one stage.

You do not need to understand the game engine’s internals. You need a clear picture of how your code runs, when it can ask the player questions, and how one card can contain several separate pieces of code.

---

## What you will learn

1. What multiple **code tabs** mean on one card
2. Why a card like **Junta** needs more than one stage
3. How the shared game **queue** connects those stages
4. How to pass simple **arguments** into a later stage
5. How to read the board, check ongoing events, and offer player choices
6. What works today, and what still needs engine support

---

## One card can contain several code blocks

In the Card Generator, each **code tab** holds a separate chunk of JavaScript.

Those chunks all belong to the **same card**. They are not separate cards. They are different stages of the same NFT object.

A useful mental model:

> **One card can contain several code blocks. Each block can be invoked separately as an NFT event, using the card’s ID and the index of the code block to execute.**

| Idea | Meaning |
|---|---|
| Card identity | The card’s NFT ID in the game (the id stored with the minted card) |
| Code block | One JavaScript chunk on that card |
| Code index | Which chunk to run: `0` is the first tab, `1` is the second, and so on |

When the card is played normally as an event, the game runs the **first** usable code block (index `0`).

Later, the game can run another block on the same card by scheduling an NFT event that names:

- the same card ID, and
- a different code index

The second block is still Junta. It is not a new card and not an unrelated event. It is simply the next stage of the same programmable card.

---

## Why Junta needs two stages

Native **Junta** is a good teaching example because it naturally splits into two decisions:

1. Place 2 influence in Central or South America
2. Then decide whether to use free operations for a **coup** or a **realignment** in that region

The second decision should happen **after** the influence has been applied. The board the player sees when choosing coup or realignment should already include the new influence.

That is why a programmable Junta wants two code tabs:

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

### The sequence in human terms

1. The player plays Junta.
2. The first code block asks where to place influence.
3. The game processes that placement.
4. The second code block executes.
5. The second code block examines the updated board and asks whether to coup or realign.
6. The game processes the selected action and completes the event.

If both decisions lived in one uninterrupted script, the second choice would still be looking at the board from **before** the shared queue finished applying the placement for every player. Splitting the work into two stages lets the game finish stage 1’s board changes first.

---

## How the queue connects the stages

Your card script does not edit the live game board by reaching into internal objects. It asks the game to do work by adding instructions, then submits them with `await api.endTurn()`.

Those instructions go onto the shared **game queue**. Every player’s client processes the same queue in the same order. That is what keeps the game synchronized.

To run another code block on the same card later, the first stage schedules an instruction with this shape:

```text
NFT_EVENT	CARD_ID	CODE_INDEX	optional_arg_0	optional_arg_1	...
```

For example, to run the second code tab on a card whose NFT ID is `my-junta-card`:

```text
NFT_EVENT	my-junta-card	1
```

Or, if you also want to pass the chosen country into the second stage:

```text
NFT_EVENT	my-junta-card	1	cuba
```

When the engine reaches that instruction, it:

1. Finds the NFT object with that card ID
2. Selects the code block at the requested index
3. Prepares an `args` array for that invocation
4. Runs that code block in the sandbox
5. Removes the `NFT_EVENT` instruction itself as part of handling it

Important points:

- The second code block is **not** called as an ordinary JavaScript function by the first one.
- It is scheduled as another piece of game work.
- You do **not** need an extra instruction just to clear the NFT event. The engine removes it when it runs.
- The first code block runs as the card’s initial event.
- The second code block runs later as its own NFT event.

### Queue order in plain language

The shared queue usually works from the **end** of the list. The last instruction you add is the first one the game processes.

So if you want the story to be:

1. place influence
2. run stage 2
3. finish / resolve the card

you generally add those instructions in **reverse** order:

1. resolve
2. NFT event for stage 2
3. place

That way, when the game works through the list, placement happens first, stage 2 happens next, and resolve happens last.

---

## Passing arguments into a later stage

When an NFT event runs a code block, the engine prepares a simple array called `args` for that invocation.

Inside the script you can read:

```javascript
args[0]
args[1]
args[2]
// ...
```

Those values come from the optional fields after the code index in the instruction.

Example:

```text
NFT_EVENT	my-junta-card	1	cuba	coup
```

gives the second code block:

```javascript
args[0] // "cuba"
args[1] // "coup"
```

If no extra fields are provided, `args` is an empty array.

This is a simple way to hand information from one stage to the next — for example, the country chosen in stage 1.

When the card is first played as a normal event, stage 1 usually has no special arguments. Arguments become useful when a later stage is invoked through `NFT_EVENT`.

---

## Junta example: two code tabs

The examples below are a **hypothetical programmable Junta**. They are inspired by the real card’s two-step decision, adapted to the programmable-card API.

> **What works today, and what does not**
>
> - Choosing a country and placing influence with `place` works.
> - Asking the player a menu question works in the card’s initial event.
> - Reading control / ongoing events works.
> - NFT scripts **cannot currently enqueue** `NFT_EVENT`, so one code tab cannot yet schedule another from sandbox code.
> - NFT scripts **cannot currently enqueue** coup, realignment, or free-ops instructions.
> - When the engine does run an `NFT_EVENT`, it currently executes that code on every client. Interactive HUD choices in a later stage may need additional player-routing support before they behave like a normal card play.
>
> The multi-stage structure below is the right authoring model. Lines that are not permitted yet are marked clearly. Do not treat those marked lines as working code today.

Replace `YOUR_CARD_ID` with the card’s real NFT ID in the game.

### Code tab 1 — Place influence

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

// Finish the card after later stages.
api.addToQueue("resolve\t" + cardId);

// Intended: run code tab 2 after placement is processed.
// Not available yet from NFT scripts:
// api.addToQueue("NFT_EVENT\t" + cardId + "\t1\t" + country);

// Place last so the shared queue processes placement first.
api.addToQueue("place\t" + faction + "\t" + faction + "\t" + country + "\t2");

await api.endTurn();
return 0;
```

**What this stage is doing**

1. Figures out whether the acting player is US or USSR
2. Asks which Central / South American country to target
3. Prepares to finish the card with `resolve`
4. Would schedule code tab `1` and pass the chosen country as `args[0]`
5. Places 2 influence in the chosen country
6. Submits the turn and returns `0` so the queue can wait for that submission

### Code tab 2 — Coup or realignment

```javascript
const cardId = "YOUR_CARD_ID";
const faction = context.game.player === 2 ? "us" : "ussr";
const country = args[0];

if (!country) {
  api.addToQueue("NOTIFY\tJunta stage 2 is missing its target country");
  await api.endTurn();
  return 0;
}

const controller = api.whoControls(country);
api.addToQueue(
  "NOTIFY\tJunta reviews " + country +
  (controller ? " (controlled by " + controller + ")" : " (uncontrolled)")
);

const choice = await api.playerSelectOption([
  { id: "coup", label: "Coup" },
  { id: "realign", label: "Realignment" },
  { id: "skip", label: "Skip military action" }
]);

if (choice === "skip") {
  api.addToQueue("NOTIFY\tJunta skips the free military action");
  await api.endTurn();
  return 0;
}

// Intended: spend free ops on a coup or realignment in Central / South America.
// Not available yet from NFT scripts:
// api.addToQueue("ops\t" + faction + "\t" + cardId + "\t2");
// or a dedicated coup / realign instruction, once permitted

api.addToQueue(
  "NOTIFY\tJunta would now " + choice +
  " in Central or South America (military follow-up not yet available to NFT cards)"
);

await api.endTurn();
return 0;
```

**What this stage is doing**

1. Reads the country passed from stage 1 through `args[0]`
2. Inspects the **current** board with `api.whoControls`
3. Asks the player whether to coup, realign, or skip
4. Reports the intended military follow-up

Once NFT scripts can schedule `NFT_EVENT` and enqueue military instructions, this is the stage that should carry out the free coup / realignment after the influence is already on the board.

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