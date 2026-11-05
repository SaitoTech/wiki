---
title: Twilight Struggle - Custom Cards - Example Code
description: 
published: true
date: 2026-11-05T12:35:03.718Z
tags: 
editor: markdown
dateCreated: 2026-11-04T14:10:51.790Z
---

# Programmable Card Examples

Working cookbook for Twilight Struggle programmable cards, arranged in order of complexity. When coding, remember to replace `YOUR_NFT_ID` with the card id available on the card greation coding page.

---

### 1. Allende — place influence in one country

```javascript
const faction = api.returnEventingPlayer();
if (!api.isPlayer(faction)) {
  return 0;
}

api.addMove("place\tussr\tussr\tchile\t2");
api.addMove("NOTIFY\tUSSR places 2 in Chile");
api.endTurn();
return 0;
```

---

### 2. Panama Canal — place in several countries

```javascript
const faction = api.returnEventingPlayer();
if (!api.isPlayer(faction)) {
  return 0;
}

api.addMove("place\tus\tus\tpanama\t1");
api.addMove("place\tus\tus\tvenezuela\t1");
api.addMove("place\tus\tus\tcostarica\t1");
api.addMove("NOTIFY\tPanama Canal: US places in Panama, Venezuela, and Costa Rica");
api.endTurn();
return 0;
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
const faction = api.returnEventingPlayer();
if (!api.isPlayer(faction)) {
  return 0;
}

const cuba = context.game.countries && context.game.countries.cuba;
const us = cuba ? Number(cuba.us) || 0 : 0;
const ussr = cuba ? Number(cuba.ussr) || 0 : 0;

if (us > 0) {
  api.addMove("remove\tussr\tus\tcuba\t" + us);
}
if (ussr < 3) {
  api.addMove("place\tussr\tussr\tcuba\t" + (3 - ussr));
}
api.addMove("NOTIFY\tFidel: Cuba is now a USSR stronghold");
api.addMove("resolve\tYOUR_NFT_ID");
api.endTurn();
return 0;
```

---

### 5. Duck and Cover — lower DEFCON and award VP

```javascript
const faction = api.returnEventingPlayer();
if (!api.isPlayer(faction)) {
  return 0;
}

const defcon = Number(context.game.state && context.game.state.defcon) || 5;
const vp = Math.max(0, 5 - (defcon - 1)); // after lowering one step

api.addMove("defcon\tlower");
api.addMove("vp\tus\t" + vp);
api.addMove("NOTIFY\tDuck and Cover: DEFCON falls, US gains " + vp + " VP");
api.endTurn();
return 0;
```

---

### 6. One Small Step — advance the Space Race when behind

```javascript
const state = context.game.state || {};
const faction = api.returnEventingPlayer();
const usTrack = Number(state.space_race_us) || 0;
const ussrTrack = Number(state.space_race_ussr) || 0;
const behind =
  faction === "us" ? usTrack < ussrTrack : ussrTrack < usTrack;

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
if (!api.isPlayer(faction)) {
  return 0;
}

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
  api.addMove("vp\t" + faction + "\t" + bonus);
  api.addMove("NOTIFY\tArms Race: " + faction.toUpperCase() + " gains " + bonus + " VP");
} else {
  api.addMove("NOTIFY\tArms Race: no milops lead");
}

api.addMove("resolve\tYOUR_NFT_ID");
api.endTurn();
return 0;
```

---

### 8. Side-aware branch — different effects for US and USSR

**Demonstrates:** `api.returnEventingPlayer()` for dual-use events.

```javascript
// Side-aware placement.
const faction = api.returnEventingPlayer();
if (!api.isPlayer(faction)) {
  return 0;
}

if (faction === "us") {
  api.addMove("place\tus\tus\twestgermany\t2");
  api.addMove("NOTIFY\tUS path: 2 in West Germany");
} else {
  api.addMove("place\tussr\tussr\teastgermany\t2");
  api.addMove("NOTIFY\tUSSR path: 2 in East Germany");
}

api.addMove("resolve\tYOUR_NFT_ID");
api.endTurn();
return 0;
```

---

### 9. Pinochet — menu choice

**Demonstrates:** `api.playerSelectOption`.

```javascript
// Inspired by Pinochet.
const faction = api.returnEventingPlayer();
if (!api.isPlayer(faction)) {
  return 0;
}

const choice = await api.playerSelectOption([
  { id: "chile", label: "2 Influence in Chile" },
  { id: "argentina", label: "2 Influence in Argentina" }
]);

api.addMove("place\tus\tus\t" + choice + "\t2");
api.addMove("NOTIFY\tUS places 2 in " + choice);
api.addMove("resolve\tYOUR_NFT_ID");
api.endTurn();
return 0;
```

---

### 10. Special Relationship — control check, event flag, country pick, VP

**Demonstrates:** `isControlled`, `isEventActive`, `playerSelectCountry`, and `vp`.

```javascript
// Based on Special Relationship.
const faction = api.returnEventingPlayer();
if (!api.isPlayer(faction)) {
  return 0;
}

if (api.isControlled("us", "uk") != 1) {
  api.addMove("NOTIFY\tSpecial Relationship: US does not control the UK");
  api.addMove("resolve\tYOUR_NFT_ID");
  api.endTurn();
  return 0;
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
api.addMove("resolve\tYOUR_NFT_ID");
api.endTurn();
return 0;
```

---

### 11. Junta-style — place, then optional coup

**Demonstrates:** menu + `coup` queue command.

```javascript
// Adaptation of Junta (Central/South America).
const faction = api.returnEventingPlayer();
if (!api.isPlayer(faction)) {
  return 0;
}

const country = await api.playerSelectCountry([
  "mexico", "guatemala", "elsalvador", "honduras", "nicaragua", "costarica", "panama", "cuba",
  "venezuela", "colombia", "ecuador", "peru", "chile", "bolivia", "paraguay", "uruguay", "argentina", "brazil"
]);

api.addMove("place\t" + faction + "\t" + faction + "\t" + country + "\t2");

const follow = await api.playerSelectOption([
  { id: "coup", label: "Free coup in that country" },
  { id: "skip", label: "Skip the coup" }
]);

if (follow === "coup") {
  api.addMove("coup\t" + faction + "\t" + country + "\t2");
}

api.addMove("resolve\tYOUR_NFT_ID");
api.endTurn();
return 0;
```

---

### 12. Socialist Governments — cancel when Iron Lady is active

**Demonstrates:** `isEventActive` guard + `remove`.

```javascript
// Adaptation of Socialist Governments / Iron Lady.
const faction = api.returnEventingPlayer();
if (!api.isPlayer(faction)) {
  return 0;
}

if (api.isEventActive("ironlady") == 1) {
  api.addMove("NOTIFY\tIron Lady cancels this effect");
  api.addMove("resolve\tYOUR_NFT_ID");
  api.endTurn();
  return 0;
}

const country = await api.playerSelectCountry([
  "italy", "france", "spain", "greece", "turkey", "westgermany", "uk"
]);
const us = Number((context.game.countries[country] || {}).us) || 0;
const amount = Math.min(2, us);

if (amount > 0) {
  api.addMove("remove\tussr\tus\t" + country + "\t" + amount);
  api.addMove("NOTIFY\tSocialist Governments: remove " + amount + " US from " + country);
} else {
  api.addMove("NOTIFY\tNo US influence to remove in " + country);
}

api.addMove("resolve\tYOUR_NFT_ID");
api.endTurn();
return 0;
```

---

### 13. The Reformer — scale placements from the VP track

**Demonstrates:** reading `context.game.state.vp`, then repeated country picks.

```javascript
// Adaptation of The Reformer.
const faction = api.returnEventingPlayer();
if (!api.isPlayer(faction)) {
  return 0;
}

const vp = Number(context.game.state && context.game.state.vp) || 0;
const picks = vp < 0 ? 2 : 1;
const europe = [
  "eastgermany", "poland", "czechoslovakia", "hungary", "romania",
  "bulgaria", "yugoslavia", "finland", "austria"
];

const chosen = [];
for (let i = 0; i < picks; i++) {
  const remaining = europe.filter((id) => chosen.indexOf(id) === -1);
  chosen.push(await api.playerSelectCountry(remaining));
}

for (const country of chosen) {
  api.addMove("place\tussr\tussr\t" + country + "\t1");
}
api.addMove("NOTIFY\tReformer: USSR places in " + chosen.join(", "));
api.addMove("resolve\tYOUR_NFT_ID");
api.endTurn();
return 0;
```

---

### 14. Marshall Plan — several sequential places after choices

**Demonstrates:** filtering candidates, then batching places.

```javascript
// Adaptation of Marshall Plan.
const faction = api.returnEventingPlayer();
if (!api.isPlayer(faction)) {
  return 0;
}

const western = [
  "canada", "uk", "france", "spain", "italy", "greece", "turkey",
  "westgermany", "benelux", "denmark", "norway", "sweden", "austria", "finland"
];
const open = western.filter((id) => api.isControlled("ussr", id) != 1);
const picks = [];

while (picks.length < 3 && picks.length < open.length) {
  const remaining = open.filter((id) => picks.indexOf(id) === -1);
  picks.push(await api.playerSelectCountry(remaining));
}

for (const country of picks) {
  api.addMove("place\tus\tus\t" + country + "\t1");
}
api.addMove("NOTIFY\tMarshall Plan: US places in " + picks.join(", "));
api.addMove("resolve\tYOUR_NFT_ID");
api.endTurn();
return 0;
```

---

### 15. Wargames — second code box via `NFT_EVENT`

**Demonstrates:** multi-code NFT; `NFT_EVENT\t{id}\t{index}`.

**Code box 0**

```javascript
// Based on Wargames — stage a follow-up box when DEFCON is 2.
const faction = api.returnEventingPlayer();
if (!api.isPlayer(faction)) {
  return 0;
}

const defcon = Number(context.game.state && context.game.state.defcon);
if (defcon !== 2) {
  api.addMove("NOTIFY\tWargames: DEFCON is not 2");
  api.addMove("resolve\tYOUR_NFT_ID");
  api.endTurn();
  return 0;
}

const choice = await api.playerSelectOption([
  { id: "end", label: "Trigger follow-up (end-game style)" },
  { id: "stop", label: "Continue the game" }
]);

api.addMove("resolve\tYOUR_NFT_ID");
if (choice === "end") {
  api.addMove("NFT_EVENT\tYOUR_NFT_ID\t1");
} else {
  api.addMove("NOTIFY\tWargames: player continues");
}
api.endTurn();
return 0;
```

**Code box 1** (runs via `NFT_EVENT\tYOUR_NFT_ID\t1`)

```javascript
// Follow-up box. NFT_EVENT is already spliced before this runs — no resolve needed.
const faction = api.returnEventingPlayer();
if (!api.isPlayer(faction)) {
  return 0;
}

api.addMove("vp\t" + faction + "\t6");
api.addMove("NOTIFY\tWargames follow-up: " + faction.toUpperCase() + " scores 6 VP");
api.endTurn();
return 0;
```

---

### 16. Summit — follow-up box with args + DEFCON change

**Demonstrates:** `NFT_EVENT` trailing args become `args[]` in the later box.

**Code box 0**

```javascript
const faction = api.returnEventingPlayer();
if (!api.isPlayer(faction)) {
  return 0;
}

const mode = await api.playerSelectOption([
  { id: "raise", label: "Raise DEFCON" },
  { id: "lower", label: "Lower DEFCON" },
  { id: "same", label: "Leave DEFCON alone" }
]);

api.addMove("resolve\tYOUR_NFT_ID");
api.addMove("NFT_EVENT\tYOUR_NFT_ID\t1\t" + mode);
api.endTurn();
return 0;
```

**Code box 1**

```javascript
const mode = typeof args !== "undefined" && args[0] ? String(args[0]) : "same";
const faction = api.returnEventingPlayer();
if (!api.isPlayer(faction)) {
  return 0;
}

if (mode === "raise") {
  api.addMove("defcon\traise");
} else if (mode === "lower") {
  api.addMove("defcon\tlower");
}
api.addMove("NOTIFY\tSummit follow-up: DEFCON mode " + mode);
api.endTurn();
return 0;
```

---

### 17. Puppet Governments — scan empty countries

**Demonstrates:** building a candidate list from `context.game.countries`.

```javascript
// Adaptation of Puppet Governments.
const faction = api.returnEventingPlayer();
if (!api.isPlayer(faction)) {
  return 0;
}

const countries = context.game.countries || {};
const empty = Object.keys(countries).filter((id) => {
  const c = countries[id];
  return c && Number(c.us) === 0 && Number(c.ussr) === 0;
});

if (!empty.length) {
  api.addMove("NOTIFY\tPuppet Governments: no empty countries");
  api.addMove("resolve\tYOUR_NFT_ID");
  api.endTurn();
  return 0;
}

const picks = [];
const limit = Math.min(3, empty.length);
while (picks.length < limit) {
  const remaining = empty.filter((id) => picks.indexOf(id) === -1);
  picks.push(await api.playerSelectCountry(remaining));
}

for (const country of picks) {
  api.addMove("place\tus\tus\t" + country + "\t1");
}
api.addMove("NOTIFY\tPuppet Governments: US places in " + picks.join(", "));
api.addMove("resolve\tYOUR_NFT_ID");
api.endTurn();
return 0;
```

---

### 18. Comecon — filter with `whoControls`

**Demonstrates:** regional list + control filter before asking.

```javascript
// Adaptation of Comecon.
const faction = api.returnEventingPlayer();
if (!api.isPlayer(faction)) {
  return 0;
}

const east = [
  "finland", "poland", "eastgermany", "austria", "czechoslovakia",
  "bulgaria", "hungary", "romania", "yugoslavia"
];
const open = east.filter((id) => api.whoControls(id) !== "us");

if (!open.length) {
  api.addMove("NOTIFY\tComecon: no legal countries");
  api.addMove("resolve\tYOUR_NFT_ID");
  api.endTurn();
  return 0;
}

const picks = [];
const limit = Math.min(2, open.length);
while (picks.length < limit) {
  const remaining = open.filter((id) => picks.indexOf(id) === -1);
  picks.push(await api.playerSelectCountry(remaining));
}

for (const country of picks) {
  api.addMove("place\tussr\tussr\t" + country + "\t1");
}
api.addMove("NOTIFY\tComecon: USSR places in " + picks.join(", "));
api.addMove("resolve\tYOUR_NFT_ID");
api.endTurn();
return 0;
```

---

### 19. Formosan Resolution — set a lasting event flag

**Demonstrates:** `api.setEvent` / `api.isEventActive` (runs on every client).

```javascript
// Based on Formosan Resolution.
api.setEvent("formosan", 1);

if (api.isPlayer(api.returnEventingPlayer())) {
  api.addMove("NOTIFY\tFormosan Resolution is now in effect");
  api.addMove("resolve\tYOUR_NFT_ID");
  api.endTurn();
  return 0;
}

return 0;
```

---

### 20. Combined — Star Wars gate, dice, realign

**Demonstrates:** Space Race check, `rollDice`, and `realign` in one event.

```javascript
// Combined adaptation inspired by Star Wars + realignment pressure.
const faction = api.returnEventingPlayer();
const state = context.game.state || {};
const usAhead =
  (Number(state.space_race_us) || 0) > (Number(state.space_race_ussr) || 0);

if (!usAhead) {
  if (api.isPlayer(faction)) {
    api.addMove("NOTIFY\tUS is not ahead on the Space Race");
    api.addMove("resolve\tYOUR_NFT_ID");
    api.endTurn();
  }
  return 0;
}

api.setEvent("starwars", 1);

if (!api.isPlayer(faction)) {
  return 0;
}

const country = await api.playerSelectCountry([
  "poland", "eastgermany", "czechoslovakia", "hungary", "romania", "bulgaria"
]);
const roll = api.rollDice(6);

api.addMove("realign\tus\t" + country);
api.addMove(
  "NOTIFY\tStar Wars-style pressure: realign " + country + " (roll shown locally: " + roll + ")"
);
api.addMove("resolve\tYOUR_NFT_ID");
api.endTurn();
return 0;
```

---

## Quick reference

| # | Source | Capability |
|---|---|---|
| 1 | Allende | single `place` |
| 2 | Panama Canal | multi `place` |
| 3 | US/Japan | read countries, compute amount |
| 4 | Fidel | `remove` + `place` |
| 5 | Duck and Cover | `defcon` + `vp` |
| 6 | One Small Step | `api.advanceSpaceRace` |
| 7 | Arms Race | milops → `vp` |
| 8 | dual-use | `returnEventingPlayer` branch |
| 9 | Pinochet | `playerSelectOption` |
| 10 | Special Relationship | control + flag + country + `vp` |
| 11 | Junta | place + optional `coup` |
| 12 | Socialist Governments | `isEventActive` + `remove` |
| 13 | The Reformer | VP-scaled picks |
| 14 | Marshall Plan | filtered multi-select |
| 15 | Wargames | `NFT_EVENT` second box |
| 16 | Summit | `NFT_EVENT` + args + `defcon` |
| 17 | Puppet Governments | scan empty countries |
| 18 | Comecon | `whoControls` filter |
| 19 | Formosan Resolution | `setEvent` / `isEventActive` |
| 20 | Star Wars mix | Space Race gate + `rollDice` + `realign` |