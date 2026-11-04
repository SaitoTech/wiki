---
title: Twilight Struggle - Custom Cards - Example Code
description: 
published: true
date: 2026-11-04T14:10:51.790Z
tags: 
editor: markdown
dateCreated: 2026-11-04T14:10:51.790Z
---

# Custom Card - Examples

This page has code to implement real Twilight Struggle events. To use them, replace `YOUR_NFT_ID` with your card’s custom id (this will be slug of the title plus its card number) and modify the results to make your own card.

Where the original card uses a command programmable cards cannot enqueue yet (`remove`, Space Race, VP, coup), the example notes that and implements the part that *is* supported.

---

## Example 1: Allende

USSR places 2 influence in Chile.

```javascript
api.addToQueue("place\tussr\tussr\tchile\t2");
await api.endTurn();
return 0;
```

---

## Example 2: Panama Canal Returned

US places 1 influence in Panama, Venezuela, and Costa Rica.

```javascript
api.addToQueue("place\tus\tus\tpanama\t1");
api.addToQueue("place\tus\tus\tvenezuela\t1");
api.addToQueue("place\tus\tus\tcostarica\t1");
await api.endTurn();
return 0;
```

---

## Example 3: Camp David Accords

US places 1 influence in Israel, Egypt, and Jordan.

(Native Camp David also awards 1 VP and cancels Arab-Israeli War. Programmable cards cannot enqueue `vp` or cancel events yet, so this example covers the influence.)

```javascript
api.addToQueue("place\tus\tus\tisrael\t1");
api.addToQueue("place\tus\tus\tegypt\t1");
api.addToQueue("place\tus\tus\tjordan\t1");
await api.endTurn();
return 0;
```

---

## Example 4: US/Japan Mutual Defense Pact

US places enough influence in Japan to lead the USSR by 4.

```javascript
const japan = context.game.countries.japan;
const us = Number(japan.us) || 0;
const ussr = Number(japan.ussr) || 0;
const needed = (ussr + 4) - us;

if (needed > 0) {
  api.addToQueue("place\tus\tus\tjapan\t" + needed);
}

api.addToQueue("resolve\tYOUR_NFT_ID");
await api.endTurn();
return 0;
```

---

## Example 5: Solidarity

If John Paul II has been evented, US places 3 influence in Poland.

```javascript
if (api.isEventActive("johnpaul") != 1) {
  api.addToQueue("NOTIFY\tSolidarity does not trigger without John Paul II");
  api.addToQueue("resolve\tYOUR_NFT_ID");
  await api.endTurn();
  return 0;
}

api.addToQueue("place\tus\tus\tpoland\t3");
api.addToQueue("resolve\tYOUR_NFT_ID");
await api.endTurn();
return 0;
```

---

## Example 6: Independent Reds

US chooses an Eastern European country where the USSR has more influence, then matches that influence.

```javascript
const list = ["yugoslavia", "romania", "bulgaria", "hungary", "czechoslovakia"];
const options = [];

for (let i = 0; i < list.length; i++) {
  const id = list[i];
  const c = context.game.countries[id];
  const us = Number(c.us) || 0;
  const ussr = Number(c.ussr) || 0;
  const diff = ussr - us;
  if (diff > 0) {
    options.push({ id: id, label: id + " (+" + diff + ")" });
  }
}

if (!options.length) {
  api.addToQueue("NOTIFY\tIndependent Reds: nothing to match");
  api.addToQueue("resolve\tYOUR_NFT_ID");
  await api.endTurn();
  return 0;
}

const country = await api.playerSelectOption(options);
const c = context.game.countries[country];
const amount = (Number(c.ussr) || 0) - (Number(c.us) || 0);

api.addToQueue("place\tus\tus\t" + country + "\t" + amount);
api.addToQueue("resolve\tYOUR_NFT_ID");
await api.endTurn();
return 0;
```

---

## Example 7: Junta

The eventing player places 2 influence in a Central or South American country.

(Native Junta then offers a free coup/realignment. Programmable cards cannot enqueue `coup` / `realign` / `ops` yet, so this example covers the placement.)

```javascript
const faction = api.returnEventingPlayer();
const targets = [
  "mexico", "guatemala", "elsalvador", "honduras", "nicaragua",
  "costarica", "panama", "cuba", "haiti", "dominicanrepublic",
  "venezuela", "colombia", "ecuador", "peru", "chile",
  "bolivia", "argentina", "paraguay", "uruguay", "brazil"
];

const country = await api.playerSelectCountry(targets);

api.addToQueue("place\t" + faction + "\t" + faction + "\t" + country + "\t2");
api.addToQueue("NOTIFY\tJunta: placed 2 in " + country + " (coup/realign follow-up not available to NFT cards)");
api.addToQueue("resolve\tYOUR_NFT_ID");
await api.endTurn();
return 0;
```

---

## Example 8: Comecon

USSR places 1 influence in each of up to 4 non-US-controlled Eastern European countries.

```javascript
const east = [
  "finland", "poland", "eastgermany", "austria", "czechoslovakia",
  "bulgaria", "hungary", "romania", "yugoslavia"
];
const open = east.filter(function (id) {
  return api.isControlled("us", id) != 1;
});

const picks = [];
const limit = Math.min(4, open.length);

while (picks.length < limit) {
  const remaining = open.filter(function (id) {
    return picks.indexOf(id) === -1;
  });
  picks.push(await api.playerSelectCountry(remaining));
}

for (let i = 0; i < picks.length; i++) {
  api.addToQueue("place\tussr\tussr\t" + picks[i] + "\t1");
}

api.addToQueue("resolve\tYOUR_NFT_ID");
await api.endTurn();
return 0;
```

---

## Example 9: OAS Founded

US places 2 influence in Central or South America (1 per country in this simplified version).

```javascript
const americas = [
  "mexico", "guatemala", "elsalvador", "honduras", "nicaragua",
  "costarica", "panama", "cuba", "haiti", "dominicanrepublic",
  "venezuela", "colombia", "ecuador", "peru", "chile",
  "bolivia", "argentina", "paraguay", "uruguay", "brazil"
];

const first = await api.playerSelectCountry(americas);
const second = await api.playerSelectCountry(
  americas.filter(function (id) { return id !== first; })
);

api.addToQueue("place\tus\tus\t" + first + "\t1");
api.addToQueue("place\tus\tus\t" + second + "\t1");
api.addToQueue("resolve\tYOUR_NFT_ID");
await api.endTurn();
return 0;
```

---

## Example 10: Puppet Governments

US places 1 influence in each of three countries that currently have no influence.

```javascript
const countries = context.game.countries;
const empty = Object.keys(countries).filter(function (id) {
  return Number(countries[id].us) === 0 && Number(countries[id].ussr) === 0;
});

if (!empty.length) {
  api.addToQueue("NOTIFY\tPuppet Governments: no empty countries");
  api.addToQueue("resolve\tYOUR_NFT_ID");
  await api.endTurn();
  return 0;
}

const picks = [];
const limit = Math.min(3, empty.length);

while (picks.length < limit) {
  const remaining = empty.filter(function (id) {
    return picks.indexOf(id) === -1;
  });
  picks.push(await api.playerSelectCountry(remaining));
}

for (let i = 0; i < picks.length; i++) {
  api.addToQueue("place\tus\tus\t" + picks[i] + "\t1");
}

api.addToQueue("resolve\tYOUR_NFT_ID");
await api.endTurn();
return 0;
```