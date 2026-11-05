---
title: Twilight Struggle - Custom Cards - Example Code
description: 
published: true
date: 2026-11-05T14:22:32.528Z
tags: 
editor: markdown
dateCreated: 2026-11-04T14:10:51.790Z
---

# Programmable Card Examples

Working cookbook for Twilight Struggle programmable cards, arranged in order of complexity. When coding, remember to replace `YOUR_NFT_ID` with the card id available on the card greation coding page.

---

### 1. Allende — place influence in one country

```javascript
api.addMove("place\tussr\tussr\tchile\t2");
api.addMove("NOTIFY\tUSSR places 2 in Chile");
return 1;
```

---

### 2. Panama Canal — place in several countries

```javascript
api.addMove("place\tus\tus\tpanama\t1");
api.addMove("place\tus\tus\tvenezuela\t1");
api.addMove("place\tus\tus\tcostarica\t1");
api.addMove("NOTIFY\tPanama Canal: US places in Panama, Venezuela, and Costa Rica");
return 1;
```

---

### 3. US/Japan — read board state, place enough to control

```javascript
const japan = context.game.countries && context.game.countries.japan;
const us = Number(japan.us) || 0;
const ussr = Number(japan.ussr) || 0;
const needed = ussr + 4 - us;

if (needed > 0) {
  api.addToQueue("place\tus\tus\tjapan\t" + needed);
  api.addToQueue("NOTIFY\tUS/Japan: +" + needed + " in Japan");
}

return 1;
```

---

### 4. Fidel — remove opponent influence, take control

```javascript
const cuba = context.game.countries && context.game.countries.cuba;
const us = cuba ? Number(cuba.us) || 0 : 0;
const ussr = cuba ? Number(cuba.ussr) || 0 : 0;

if (us > 0) {
  api.addMove("remove\tussr\tus\tcuba\t" + us);
  
}
api.addMove("place\tussr\tussr\tcuba\t" + (3 - ussr));
return 1;
```

---

### 5. Duck and Cover — lower DEFCON and award VP

```javascript
const defcon = Number(context.game.state && context.game.state.defcon) || 5;
const vp = Math.max(0, 5 - (defcon - 1));

api.addToQueue("defcon\tlower");
api.addToQueue("vp\tus\t" + vp);
api.addToQueue("NOTIFY\tDuck and Cover: DEFCON falls, US gains " + vp + " VP");
return 1;
```

---

### 6. One Small Step — advance the Space Race when behind

```javascript
const state = context.game.state || {};
const faction = api.returnEventingPlayer();
const usTrack = Number(state.space_race_us) || 0;
const ussrTrack = Number(state.space_race_ussr) || 0;
const behind = faction === "us" ? usTrack < ussrTrack : ussrTrack < usTrack;

if (behind) {
  api.advanceSpaceRace(faction, true); // skip intermediate VP
  api.advanceSpaceRace(faction);
}
return 1;
```

---

### 7. Arms Race — award VP from milops leadership

**Demonstrates:** reading milops / DEFCON, then `vp`.

```javascript
// Based on Arms Race.
const faction = api.returnEventingPlayer();
const state = context.game.state || {};
const myOps = Number(faction === "us" ? state.milops_us : state.milops_ussr) || 0;
const theirOps = Number(faction === "us" ? state.milops_ussr : state.milops_us) || 0;
const defcon = Number(state.defcon) || 0;

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

### 8. Berlin Agreement - different effects for US and USSR

```javascript
const faction = api.returnEventingPlayer();

if (faction === "us") {
  api.addToQueue("place\tus\tus\twestgermany\t2");
  api.addToQueue("NOTIFY\tUS path: 2 in West Germany");
} else {
  api.addToQueue("place\tussr\tussr\teastgermany\t2");
  api.addToQueue("NOTIFY\tUSSR path: 2 in East Germany");
}

return 1;
```

---

### 9. Pinochet — let player select from menu

```javascript

//
// non-eventing player halts game queue
//
const faction = api.returnEventingPlayer();
if (!api.isPlayer(faction)) {
  return 0;
}

//
// eventing player continues
//
const choice = await api.playerSelectOption([
  { id: "chile", label: "2 Influence in Chile" },
  { id: "argentina", label: "2 Influence in Argentina" }
]);

api.addMove("place\tus\tus\t" + choice + "\t2");
api.addMove("NOTIFY\tUS places 2 in " + choice);
api.endTurn();
return 0;
```

---

### 10. Special Relationship - check NATO and offer placement

```javascript
if (!api.isPlayer("us")) {
  return 0;
}

if (api.isControlled("us", "uk") != 1) {
  api.addToQueue("NOTIFY\tSpecial Relationship: US does not control the UK");
  return 1;
}

const nato = api.isEventActive("nato") == 1;
const amount = nato ? 2 : 1;
const candidates = nato
  ? ["canada", "france", "italy", "westgermany", "benelux", "spain"]
  : ["canada", "france", "norway", "benelux"];

const country = await api.playerSelectCountry(candidates);
api.addMove("place\tus\tus\t" + country + "\t" + amount);
if (nato) {
  api.addMove("vp\tus\t2");
}
api.addMove(
  "NOTIFY\tSpecial Relationship: +" +
    amount +
    " in " +
    country +
    (nato ? " and 2 VP (NATO)" : "")
);
api.endTurn();
return 0;
```

