---
title: Twilight Struggle - Advanced Programming Techniques
description: 
published: true
date: 2026-11-05T06:57:59.341Z
tags: 
editor: markdown
dateCreated: 2026-11-04T12:21:40.168Z
---

# Twilight Struggle Advanced Card Programming

This guide explains how to build more advanced cards where players make changes to the board state and then act after those changes have been made. We need to use these techniques to implement cards like Junta where early choices affect which actions are available in later ones.

What you will find here:

1. Custom Cards can have multiple **code tabs** or **code boxes**
2. Why a card like **Junta** needs more than one such tab/box
3. Using the game **queue** to organize these in sequence
4. Passing simple **arguments** from step-to-step
5. More details on reading the board, checking ongoing events, and giving players interactive choices

## Cards with Multiple Code Blocks

In the Card Generator you can add additional **code tabs** that hold a separate chunk of javascript. The first tab contains the default code that will run when the event is fired. The other tabs are "events" that can be triggered by adding them to the game queue.

If you are creating a card { title: "Wargames II", number: 124 } and you create 3 additional tabs, you can schedule those tabs for execution by pushing them to the queue in your main tab:

```
if (isPlayer("us")) {
  api.addMove("NFT_EVENT\twargames-ii\t3");
  api.addMove("NFT_EVENT\twargames-ii\t2");
  api.addMove("NFT_EVENT\twargames-ii\t1");
  api.endTurn();
}
return 0;
```

This implementation exploits the built-in support Saito provides for NFTs. The NFT_EVENT code looks for the object in `this.game.options.nfts` that claims to have the id of `wargames-ii` and executes the codebox. Note that code boxes are indexed from 0, so the above code triggers the 2nd, then 3rd, then 4th codebox in turn.

We can queue these events in the first box, or have them branch, with the second tab adding execution for the third if needed, etc. In the Twilight Struggle module, the ID of the card is the slug() of its title and a hyphen and then the card number provided. 

When a card is played normally as a event, the game runs the **first** usable code block (index `0`). That piece of code can schedule another block on the same card to run later on by adding an instruction to the queue that tells the game to execute it, providing:


## Example: Junta

**Junta** is a good example because it naturally splits into two decisions:

1. Place 2 influence in Central or South America
2. Optionally choose to **coup** or **realign**

The second choice must happen **after** the influence has been applied as the first choice we give the player affects the set of eligible countries and the conditions under which the second operates. This is why a programmable version of the card needs two code blocks:

**Code tab 1 — Place influence**

- runs immediately when the card is evented
- asks player to add 2 influence to target country
- places influence there
- and asks the game engine to execute the second code box

**Code tab 2 — Coup or realignment**

- triggered after the game queue resumes
- looks at the updated board, collects targets for action
- asks the player what to do
- add those instructions to the game queue

---

## Want to Pass Values between Stages?

It is possible to send information between stages in two ways. The easiest is to add the information to the game queue when adding the instruction. This can be done by adding additional (tab-separated) arguments at the end of the queue command:

```text
api.addmove(`NFT_EVENT\t${CARD_ID}\t${CODE_IDX}\t${ARG1}\t${ARG2}`);
```

If you use this technique to pass arguments into code blocks, you can access them within the NFT object that contains the code chunk. Inside the script, you can access these arguments as folows:

```javascript
args[0]
args[1]
args[2]
// ...
```

If no arguments are provided, `args` is an empty array.

## Pracitcal Example:

### Code Block 1 — Ask Eventing Player to Place Influence


```javascript
const cardId = "junta-ii-150";

if (api.isPlayer(api.returnEventingPlayer()) {

  const faction = context.game.player === 2 ? "us" : "ussr";

  const targets = [
    "mexico", "guatemala", "elsalvador", "honduras", "nicaragua",
    "costarica", "panama", "cuba", "haiti", "dominicanrepublic",
    "venezuela", "colombia", "ecuador", "peru", "chile",
    "bolivia", "argentina", "paraguay", "uruguay", "brazil"
  ];

  const country = await api.playerSelectCountry(targets);

  //
  // so call the next code block first
  //
  api.addMove("NFT_EVENT\t" + "junta-ii-150 + "\t1\t" + country);

  //
  // then add the influence to the selected country
  //
  api.addMove("place\t" + faction + "\t" + faction + "\t" + country + "\t2");

  //
  // broadcast the information to other players
  //
  await api.endTurn();

}

//
// everyone waits to continue
//
return 0;
```

### Code Block 2 — Picking Back Up

```javascript
const cardId = "junta-ii-150";

if (api.isPlayer(api.returnEventingPlayer()) {

  const faction = context.game.player === 2 ? "us" : "ussr";
  const country = args[0];

  const choice = await api.playerSelectOption([
    { id: "coup", label: "Coup" },
    { id: "skip", label: "Skip military action" }
  ]);

  if (choice === "skip") {
    api.addMove("NOTIFY\tJunta skips the free military action");
    await api.endTurn();
    return 0;
  }

  api.addToQueue("NOTIFY\tJunta triggers a coup in " + country);

  await api.endTurn();
}

return 0;
```

A complete implementation of Junta would of course provide options for realignments. Most of the features that the game manipulates map to specific instructions that can be added to the game queue. You can find the full list in the code or on our reference page for queue instructions.

## Reading the Board / State

Your script receives a read-only snapshot as `context.game`. Changing properties on `context.game` inside your script does nothing to the real game, but you can use it to check the current value of almost anything the game tracks. Examples include the following, but you can see our full list on the page documenting [queue instructions](/applications/twilight/api/queue):

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

A few simple functions also exist on the api.* object to simplify the most common checks:

```javascript
api.isControlled("us", "canada")   // 1 or 0
api.whoControls("egypt")           // "us", "ussr", or ""
api.isEventActive("reformer")      // 1 when that ongoing event is active
```

This last instruction can be used to check if other events have triggered, allowing cards to create permanent effects that other cards can check. Developers can create such permanent effects using `api.setEvent(cardname, active)` to turn events on or off, using 1 (turn on) 0 (turn off) as the second value.


### Simple example

```javascript
if (api.isPlayer(api.returnActivePlayer()) {
    if (api.isEventActive("reformer") == 1) {
      ...
    } else {
      ...
    }
    await api.endTurn();
}
return 0;
```


## Asking the Player to Choose:

Two helpers are available for asking the players to take action. The first shows them a list of labelled options and asks them to select one. The value that is returned is the `id` of the choice selected.

```javascript
let player_choice = await api.playerSelectOption([
  { id: "india", label: "India" },
  { id: "pakistan", label: "Pakistan" }
]);
```

You can also ask players to click on the board to select a country:

```
let player_choice = await api.playerSelectCountry(["cuba", "mexico", "panama"]);
```

## Troubleshooting

Saito is a community project that evolves and adds features as players contribute and the underlying game engine develops. If you are interested in developing or adding new features, please feel welcome to get in touch.