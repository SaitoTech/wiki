---
title: Twilight Struggle - Custom Cards - Example Code
description: 
published: true
date: 2026-11-13T16:13:38.768Z
tags: 
editor: markdown
dateCreated: 2026-11-04T14:10:51.790Z
---

# Programmable Card Examples

The following examples show how to implement common actions and can be copy-and-pasted into the code section of the card generator and tested live. The examples are intended to start simple and get more complicated as they move along.

---

### 1. Allende

```javascript
api.addMove("place\tussr\tussr\tchile\t2");
api.addMove("NOTIFY\tUSSR places 2 in Chile");
return 1;
```

---

### 2. US/Japan Alliance

```javascript
const us = Number(context.game.countries.japan.us) || 0;
const ussr = Number(context.game.countries.japan.ussr) || 0;
const needed = ussr + 4 - us;

if (needed > 0) {
  api.addToQueue("place\tus\tus\tjapan\t" + needed);
  api.addToQueue("NOTIFY\tUS/Japan: +" + needed + " in Japan");
}

return 1;
```

---

### 3. Fidel

```javascript
const us = Number(context.game.countries.cuba.us) || 0;
const ussr = Number(context.game.countries.cuba.ussr) || 0;

if (us > 0) {
  api.addMove("remove\tussr\tus\tcuba\t" + us);  
}
api.addMove("place\tussr\tussr\tcuba\t" + (3 - ussr));
return 1;
```

---

### 5. Duck and Cover

```javascript
const defcon = Number(context.game.state && context.game.state.defcon) || 5;
const vp = Math.max(0, 5 - (defcon - 1));

api.addToQueue("defcon\tlower");
api.addToQueue("vp\tus\t" + vp);
api.addToQueue("NOTIFY\tDuck and Cover: DEFCON falls, US gains " + vp + " VP");
return 1;
```

---

### 6. One Small Step

```javascript
const faction = api.returnEventingPlayer();
const usTrack = Number(context.game.state.space_race_us) || 0;
const ussrTrack = Number(context.game.state.space_race_ussr) || 0;
const behind = faction === "us" ? usTrack < ussrTrack : ussrTrack < usTrack;

if (behind) {
  api.advanceSpaceRace(faction, true); // skip bonus
  api.advanceSpaceRace(faction);
}
return 1;
```

---

### 7. Arms Race

```javascript
const faction = api.returnEventingPlayer();
const state = context.game.state || {};
const myOps = Number(faction === "us" ? context.game.state.milops_us : context.game.state.milops_ussr) || 0;
const theirOps = Number(faction === "us" ? context.game.state.milops_ussr : context.game.state.milops_us) || 0;
const defcon = Number(context.game.state.defcon) || 0;

let bonus = 0;
if (myOps > theirOps) {
  bonus = 1;
  if (myOps >= defcon) {
    bonus = 3;
  }
}

if (bonus > 0) {
  api.addToQueue("vp\t" + faction + "\t" + bonus);
  api.addToQueue("NOTIFY\tArms Race: " + faction.toUpperCase() + " gains " + bonus + " VP");
} else {
  api.addToQueue("NOTIFY\tArms Race: no milops lead");
}

return 1;
```

---

### 8. Muslim Revolution

```javascript

if (api.isEventActive("awacs")) {
  return 1; 
}

const countries = ["sudan", "egypt", "libya", "syria", "iran", "iraq", "jordan", "saudiarabia"];
const targets = countries.filter((id) => Number(context.game.countries[id].us) > 0);

if (targets.length === 0) {
  return 1;
}

if (api.isPlayer("ussr")) {

  const chosen = targets.length <= 2 ? targets.slice() : [];

  while (chosen.length < Math.min(2, targets.length)) {
    const remaining = targets.filter((id) => chosen.indexOf(id) === -1);
    chosen.push(await api.playerSelectCountry(remaining));
  }

  for (let i = 0; i < chosen.length; i++) {
    const country = chosen[i];
    await api.playerRemoveInfluence(country, Number(board[country].us), "us");
  }

  await api.endTurn();
}

return 0;
```



### 9. Destalinization

```javascript
api.setEvent("destalinization_played", 1);

const board = context.game.countries;
const ussr = {};
let available = 0;

for (const id in board) {
  const n = Number(board[id].ussr) || 0;
  ussr[id] = n;
  available += n;
}

const moves = Math.min(4, available);
if (moves === 0) {
  return 1;
}

if (api.isPlayer("ussr")) {

  for (let n = 0; n < moves; n++) {
    const options = Object.keys(ussr).filter((id) => ussr[id] > 0);
    const country = await api.playerSelectCountry(options);
    await api.playerRemoveInfluence(country, 1, "ussr");
    ussr[country] -= 1;
  }

  const placed = {};
  for (let n = 0; n < moves; n++) {
    const options = Object.keys(board).filter((id) => {
      return api.isControlled("us", id) != 1 && (placed[id] || 0) < 2;
    });
    const country = await api.playerSelectCountry(options);
    await api.playerPlaceInfluence(country, 1, "ussr");
    placed[country] = (placed[country] || 0) + 1;
  }

  await api.endTurn();

}

return 0;
```

---

### 10. Star Wars

```javascript
const state = context.game.state;
const cardId = state.eventing_card;

if (state.space_race_us <= state.space_race_ussr) {
  return 1;
}

api.setEvent("starwars", 1);

const discards = (context.game.deck[0] && context.game.deck[0].discards) || {};
const options = [];

for (const id in discards) {
  const card = discards[id];
  if (!card || !card.name || card.scoring == 1) continue;
  if (state.headline == 1 && id === "unintervention") continue;
  // skip shuttle diplomacy in discards if active
  if (state.events.shuttlediplomacy == 1 && id === "shuttle") continue;
  options.push({ id: id, label: card.name });
}

if (options.length === 0) {
  return 1;
}

if (api.isPlayer("us")) {
  const chosen = await api.playerSelectOption(options);
  const name = options.find((opt) => opt.id === chosen).label;
  api.addMove("resolve\t" + cardId);
  api.addMove("event\tus\t" + chosen);
  api.addMove("NOTIFY\tUS retrieved " + name);
  api.addMove("undiscard\t" + chosen);
  await api.endTurn();
};
return 0;
```



### 11. Junta

Junta is a card that takes place over two stages, with the events of the first stage (placement) affecting how the second stage works. It also involves realignments, which are more complicated than other functions. For this reason, the code here requires two code boxes.

The first (default) event code:

```javascript
const NFT_CARD_ID = "custom-junta-example-201";
const tab = String.fromCharCode(9);

let player = "";
switch (context.game.state.eventing_player) {
  case "us":
  case "ussr":
    player = context.game.state.eventing_player;
    break;
  default:
    return 1;
}

const board = context.game.countries;
const countries = Object.keys(board).filter((id) => {
  const region = board[id] && board[id].region;
  return region === "camerica" || region === "samerica";
});

return await api.asEventingPlayer(async () => {
  const country = await api.playerSelectCountry(countries);
  api.addMove(["NFT_EVENT", NFT_CARD_ID, "1", player].join(tab));
  await api.playerPlaceInfluence(country, 2, player);
  await api.endTurn();
  return 0;
});```

The second picks up when the NFT_EVENT command specifying the second entry in the card's code array (1) is triggered.

```javascript
const tab = String.fromCharCode(9);
const sent = args && args[0];
const state = context.game.state;
const board = context.game.countries;

let player = "";
switch (state.eventing_player) {
  case "us":
    player = "us";
    break;
  case "ussr":
    player = "ussr";
    break;
  default:
    break;
}

if (sent === "us" || sent === "ussr") {
  player = sent;
}
if (player !== "us" && player !== "ussr") {
  return 1;
}

const enemy = player === "us" ? "ussr" : "us";
const limited = state.limit_region || [];
const regionBlocked = (region) => {
  if (Array.isArray(limited)) return limited.indexOf(region) !== -1;
  return String(limited).indexOf(region) !== -1;
};

const candidates = Object.keys(board).filter((id) => {
  const country = board[id];
  if (!country) return false;
  if (country.region !== "camerica" && country.region !== "samerica") return false;
  if (regionBlocked(country.region)) return false;
  return (Number(country[enemy]) || 0) > 0;
});

const coupTargets = candidates.slice();
const realignTargets = candidates.slice();

if (coupTargets.length === 0 && realignTargets.length === 0) {
  return 1;
}

return await api.asEventingPlayer(async () => {
  const menu = [];
  if (coupTargets.length > 0) menu.push({ id: "coup", label: "coup" });
  if (realignTargets.length > 0) menu.push({ id: "realign", label: "realign" });
  menu.push({ id: "skip", label: "skip" });

  const choice = await api.playerSelectOption(menu);

  if (choice === "coup") {
    const country = await api.playerSelectCountry(coupTargets);
    api.addMove(["coup", player, country, "2"].join(tab));
    await api.endTurn();
    return;
  }

  if (choice === "realign") {
    const tally = {};
    for (let i = 0; i < realignTargets.length; i++) {
      tally[realignTargets[i]] = Number(board[realignTargets[i]][enemy]) || 0;
    }
    for (let n = 0; n < 2; n++) {
      const options = realignTargets.filter((id) => tally[id] > 0);
      if (options.length === 0) break;
      const country = await api.playerSelectCountry(options);
      const result = await api.playerRealign(country, player);
      if (result && result.removedFaction === enemy) {
        tally[country] -= result.removed;
      }
    }
    await api.endTurn();
    return 0;
  }

  api.addMove(["NOTIFY", player.toUpperCase() + " skips the Junta operations"].join(tab));
  await api.endTurn();
  return 0;
});
```


