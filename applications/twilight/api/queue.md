---
title: Twilight Struggle API - Full Queue Instructions
description: Custom Cards QUEUE API
published: true
date: 2026-11-05T06:58:46.050Z
tags: 
editor: markdown
dateCreated: 2026-11-04T10:49:02.675Z
---

## Twilight Struggle Queue Commands

| Queue Instruction | Arguments and Format | Description |
|---|---|---|
| `player_turn_card_selected` | `player_turn_card_selected\t{us\|ussr}\t{card}` | On the matching client (US=player 2, USSR=player 1), runs `playerTurnCardSelected` for that card, then pauses the queue. |
| `bgs` | `bgs` or `bgs\treset` | With `reset`, restores default battlegrounds; otherwise re-parses each country's `bg` flag as an integer (used after Kissinger SETVARs). |
| `add_latewar_card_to_deck` | `add_latewar_card_to_deck\t{card}` | Adds the chosen optional Late-War card to the deck via `addTwilightCardToDeck`. |
| `choose_latewar_optional_cards` | `choose_latewar_optional_cards\t{playerNum}` | Lets player 1/2 pick a Late-War optional card via overlay (rolls 4 candidates); others wait. |
| `add_midwar_card_to_deck` | `add_midwar_card_to_deck\t{card}` | Adds the chosen optional Mid-War card to the deck. |
| `choose_midwar_optional_cards` | `choose_midwar_optional_cards\t{playerNum}` | Same as late-war chooser but for Mid-War options. |
| `init` | `init` | Initializes NFTs, assigns `game.player`, optionally reorders players for fixed US/USSR seating. |
| `update_observers` | `update_observers\t{playerNum}` | Active player submits `observer_cards_update` with a JSON hand snapshot, then ends turn. |
| `observer_cards_update` | `observer_cards_update\t{playerNum}\t{jsonHand}` | Intended to give observers the revealed hand; implementation stringifies `mv[2]` then iterates characters (likely broken). |
| `revert` | `revert` | Calls `revertTurn()` to restore start-of-turn state/queue snapshot. |
| `final_scoring` | `final_scoring` | Runs `finalScoring()` and stops the queue. |
| `turn` | `turn` | Increments action-round counter, clears China-card eligibility, updates AR UI. |
| `purge` | `purge\t{card}` | Cancels the event and removes the card from the next deal (Saito community deck tooling). |
| `discard` | `discard\t{us\|ussr}\t{card}` | Discards `card` from hand into discards; special-cases China (passes facedown to opponent). |
| `fyp_discard` | `fyp_discard\t{card}` | Puts `card` into the discard pile without removing from hand (Five Year Plan path). |
| `undiscard` | `undiscard\t{card}` | Removes `card` from discards back into the live deck (or rebuilds from all-cards table). |
| `wargames` | `wargames\t{us\|ussr}\t{0\|1}` | `0` = discard only; `1` applies Wargames concession VP and ends the game (late-war threshold differs). |
| `card` | `card\t{us\|ussr}\t{card}` | If local faction matches, starts `playerTurn(card)`; pauses queue. No current push sites found (legacy). |
| `hand` | `hand\t{playerNum}\t{card}` | Gives `card` to that player's hand locally and removes it from the other client's hand tracking. |
| `grainsales` | `grainsales\tussr\t{card}` then `grainsales\tus\t{card}` | USSR offers a card to US for play-or-return; US return path re-hands the card to USSR. |
| `stage` | `stage` [optional unused args] | No-op splice; never pushed in current sources (legacy). |
| `clearcheclicktargets` | `clearcheclicktargets` | Clears Che coup highlight CSS classes after a second-target pick. |
| `checoup` | `checoup\tussr\t{country}\t{ops}` | Resolves Che's first coup on `country` with `ops`; on success prompts USSR for a second coup target. |
| `missileenvy` | `missileenvy\t{senderPlayerNum}\t{card}` | Receiver plays offered card for ops (opponent-owned) or event (own/neutral), then discards it. |
| `quagmire` | `quagmire\t{us\|ussr}\t{discardedCard}` | Rolls to escape Quagmire/Bear Trap after discard; failure sets double-quagmire/beartrap flag. |
| `tehran` | `tehran\tussr\t{keysNum}` (+ keys on queue) / `tehran\tus\t{discardCount}` (+ crypt entries) | Our Man in Tehran: USSR supplies deck keys; US chooses discards; US reply strips those crypt cards. |
| `limit` | `limit\t{china\|coups\|spacerace\|realignments\|placement\|milops\|ignoredefcon}` or `limit\tregion\t{region}` | Enables temporary action restrictions for the current ops sequence. |
| `flush` | `flush\tdiscards` | Clears the discard object (`discards` is the only implemented subtype). |
| `latinamericandebtcrisis` | `latinamericandebtcrisis` | USSR doubles influence in up to two South American countries that already have USSR influence. |
| `northsea` | `northsea` | Prompts US about an extra turn (North Sea Oil); both choices currently enqueue `play\t2`. |
| `space` | `space\t{us\|ussr}\t{card}` | Attempts space race with `card` for that faction and discards it (except China). |
| `unlimit` | `unlimit\t{china\|cmc\|coups\|spacerace\|realignments\|placement\|milops\|ignoredefcon\|region}` [`\t{country}` for `cmc`] | Clears the matching limit; `cmc` also clears Cuban Missile Crisis and may record removal country. |
| `dynamic_deck_management` | `dynamic_deck_management` | Saito-deck only: runs `dynamicDeckManagement()` to add/remove cards. |
| `display_new_optional_cards` | `display_new_optional_cards` | Saito-deck only: shows overlay of newly added optional cards, then clears the list. |
| `pinochet` | `pinochet` | USSR removes 1 US influence from Central/South America (if any exists). |
| `nixon_shock_play_card_or_hand_to_opponent` | `nixon_shock_play_card_or_hand_to_opponent\t{playerNum}\t{activeFaction}` | Drawn-card chooser: play (US only), keep, or hand to opponent. |
| `chernobyl` | `chernobyl\t{region}` | Sets Chernobyl restricted region for USSR placements. |
| `dice` | `dice\tburn\t{us\|ussr}` | Burns one shared die roll on the acting/observer client (sync entropy). |
| `aldrichreveal` | `aldrichreveal` [`\tus` unused] | US reveals hand via `showhand` + NOTIFY (Ask Not / Aldrich paths). |
| `aldrich` | `aldrich\tus\t{n}` (+ `n` card keys below) / `aldrich\tussr\t{card}` | US publishes hand keys; USSR picks one discard; USSR reply removes it from US hand. |
| `cambridge` | `cambridge\t{regionOrScoringCard}[\t...]` | USSR places 1 OP in any country belonging to the listed region keys (from revealed US scoring cards). |
| `teardownthiswall` | `teardownthiswall` | US may take a 3-OP Europe-restricted free coup/realign package (via `limit`/`ops`) or skip. |
| `deal` | `deal\t{playerNum}` | That player computes cards needed (8/9 by round, China excluded) and queues engine `DEAL`. |
| `reshuffle_and_insert_discards` | `reshuffle_and_insert_discards` | If draw pile is short, deals remaining cards then shuffles discards back (skips rounds 4/8 insert turns). |
| `ops` | `ops\t{us\|ussr}\t{card}\t{ops}` [`\t{any}` to skip back button] | Plays ops for faction/card (modified by events); does **not** self-remove—cleared by `resolve\tops`. |
| `milops` | `milops\t{us\|ussr}\t{amount}` | Adds military operations points for that faction. |
| `vp` | `vp\t{us\|ussr}\t{points}` [`\t{delayFlag}`] | Awards VP; if `delayFlag==1`, banks into `vp_outstanding` instead of immediate board VP. |
| `coup` | `coup\t{us\|ussr}\t{country}\t{ops}` [`\t{card}`] | Resolves a coup; awards milops unless limited; optional `card` affects ops modifiers. |
| `realign` | `realign\t{us\|ussr}\t{country}` | Applies realignment on non-origin clients only (origin already applied locally). |
| `defcon` | `defcon\tlower` or `defcon\traise` | Lowers DEFCON via `lowerDefcon()`, or raises by 1 (capped at 5). |
| `move` | `move\t{us\|ussr}` | Sets `game.state.move` phasing flag (0=USSR, 1=US). No current push sites found (legacy). |
| `event` | `event\t{us\|ussr}\t{card}` | Triggers `playEvent`; may remove/discard non-recurring cards; Flower Power headline can inject delayed VP. |
| `stability` | `stability\t{faction}\t{country}\t{adj}` | Adds `adj` to country stability/control value. |
| `place` | `place\t{originFaction}\t{influenceFaction}\t{country}\t{amount}` | Places influence on non-origin clients only (origin client already applied locally). |
| `setvar` | See notes: `setvar\t{playerNum}\thold\t{json}` / `setvar\t{playerNum}\topponent_cards_in_hand\t{n}` / `setvar\tgame\tstate\tback_button_cancelled\t{0\|1}` | Twilight lowercase setter for hold-card lists, opponent hand size, and back-button cancel; other `setvar\tgame\tstate\tevents\t...` paths are spliced but not applied. |
| `remove` | `remove\t{originFaction}\t{influenceFaction}\t{country}\t{amount}` | Removes influence on non-origin clients only. |
| `resolve` | `resolve\t{token}` | Twilight-specific clear of the matching queued step (`event`/`ops`/`play`/`deal`/`headline`/`placement`/same-name instruction, etc.); also discards/removes matching card id. Distinct from engine `RESOLVE`. |
| `clear` | `clear\theadline` | Clears headline state flags after headline resolution. |
| `placement` | `placement\t{playerNum}` | Initial influence placement UI for that player; left on queue until `resolve\tplacement`. |
| `placement_bonus` | `placement_bonus\t{playerNum}\t{bonusOps}` | US bonus initial placement of `bonusOps` influence; resolved via `resolve\tplacement_bonus`. |
| `headline` | `headline` or `headline\t{stage}` [`\t{hash}\t{xor}\t{card}`] | Headline phase state machine (`headline1` default; later stages carry commitment data). |
| `deckaddcards` | `deckaddcards\t{jsonCardsObject}` | Merges card defs from JSON into the live deck. No current push sites (engine has `DECKADDCARDS`). |
| `round` | `round` | End/start-of-round controller: NORAD/extra turns/discards, `endRound`, queues turns/headline/deals/optional-card picks. |
| `play` | `play\t{playerNum}` | Starts that player's action round (`playMove`); may interrupt for NORAD; left until `resolve\tplay`/`resolve\tturn`. |
| `showhand` | `showhand\t{playerNum}\t{cardId cardId...}` | Shows space-separated hand cards to the opponent via overlay. |
| `modal` | `modal\t{title}` [`\t{body}`] | Displays a modal dialog. |
| `sharehandsize` | `sharehandsize\t{playerNum}` | That player publishes hold-card list + non-China hand count via `setvar`. |
| `war` | `war\t{card}\t{winner}\t{die}\t{modifications}\t{player}\t{success}` | Renders the war overlay with the resolved war outcome (all args optional with defaults). |

---

## Saito Game Engine Queue Commands

These instructions are provided by the base GameEngine and are available in Twilight Struggle whenever they appear on the queue. Engine handlers run **before** Twilight `handleGameLoop`.

| Queue Instruction | Arguments and Format | Description |
|---|---|---|
| `SETVAR` | `SETVAR\t{key}\t{value}` \| `SETVAR\t{key}\t{subkey}\t{value}` \| `SETVAR\t{key}\t{a}\t{b}\t{value}` \| `SETVAR\t{key}\t{a}\t{b}\t{c}\t{value}` \| `SETVAR\tgame\t{...}` (optional depth) | Writes into `game_self.game` at 1–4 nested keys; numeric-looking leaf values are `parseInt`’d when `> 0`; if first key is `game`, that token is stripped and remaining path args are shifted. |
| `SALERT / salert` | `SALERT\t{message}` | Shows a browser `salert` with `{message}`, then removes itself. |
| `NOTIFY / notify` | `NOTIFY\t{message}` | Appends `{message}` to the game log via `updateLog`, then removes itself. |
| `STATUS / status` | `STATUS\t{message}[\t{target}]` | Sets HUD/status text to `{message}` for target players (`{target}` defaults to `all`; otherwise treated as a player id/list), then removes itself. |
| `LOAD` | `LOAD` | Recognized no-op (comment notes unsupported; does not splice itself). |
| `SAVE` | `SAVE` | Saves a reloadable snapshot under `app.options.saves[game.id]`, logs a restore URL, and removes itself (skipped for PathsOfGlory). |
| `HALTED` | `HALTED` | If confirms are still needed, updates status to waiting and pauses the queue (`return 0`); otherwise falls through without removing itself (cleared via `RESOLVE`). |
| `ACKNOWLEDGE` | `ACKNOWLEDGE\t{notice}[\t{player}]` | Shows acknowledge UI with `{notice}`; optional `{player}` (1-based) restricts who must ack; others/observers clear and continue; acknowledging player pauses until confirm then splices. |
| `SETTLE` | `SETTLE` | Removes itself and calls `queueGameStakeSettlement()` to enqueue stake SEND/RECEIVE flows. |
| `GAMEOVER` | `GAMEOVER` | Marks the game over (`over=1`), shows game-over UI / site message, saves, clears itself, and pauses the queue. |
| `ROUNDOVER` | `ROUNDOVER\t{winner_json}\t{reason}[\t{losers_json}]` | Parses JSON winner (and optional losers), and if local player is seat 1 broadcasts a `roundover` league/tx message; then removes itself. |
| `OBSERVER` | `OBSERVER` | Legacy/obsolete observer toggle; currently only splices itself (body commented out). |
| `PLAY` | `PLAY\t{players}` | `{players}` is `all` or a player id(/list); resets confirms if none pending, calls `playerTurn()` for matching unsettled players (else `nonPlayerTurn`), and pauses (`return 0`); does not splice itself. |
| `RESETCONFIRMSNEEDED` | `RESETCONFIRMSNEEDED\t{players}` | `{players}` is `all`, a single id, or a JSON/array of ids; resets `confirms_needed` when none are pending (or waits if game halted), then removes itself. |
| `RESOLVE` | `RESOLVE[\t{publickey}]` | Without key: removes itself and the previous queue entry (or clears queue). With `{publickey}`: clears that player’s confirm bit; when all confirms done, also clears a pending `HALTED` or the previous instruction; otherwise only removes the `RESOLVE`. |
| `PRERESOLVE` | `PRERESOLVE\t{cmd}` | Inserts `{cmd}` immediately before the nearest older `RESOLVE` on the queue; does not remove the `PRERESOLVE` entry itself. |
| `READY` | `READY` | Sets `initializing=0`, saves, removes itself; in non-browser/background pauses further processing after emitting ready UI. |
| `SHUFFLE` | `SHUFFLE\t{deckidx}` | Calls `shuffleDeck({deckidx})` (1-based) and removes itself. |
| `SHUFFLEDISCARDS` | `SHUFFLEDISCARDS\t{deckidx}` | Moves that deck’s discards into a new encrypted/shuffled deck rebuild sequence (`DECKBACKUP`…`SHUFFLE`) and removes itself. |
| `LOGDECK` | `LOGDECK\t{deckidx}` | Logs the deck crypt contents for `{deckidx}`, then removes itself. |
| `LOGHAND` | `LOGHAND\t{deckidx}` | Logs the hand for `{deckidx}`, then removes itself. |
| `LOGPOOL` | `LOGPOOL\t{poolidx}` | Logs the pool hand for `{poolidx}`, then removes itself. |
| `DISCARD` | `DISCARD\t{deckidx}\t{card}` | Removes `{card}` from that deck’s hand into `discards` (copying from `cards`), then removes itself. |
| `RESOLVEDEAL` | `RESOLVEDEAL\t{deckidx}\t{recipient}\t{cards}` | Recipient decrypts/adds `{cards}` from crypt into hand; splices itself plus the prior entry (typically `DEAL`); purges spent keys/crypt once. |
| `SIMPLEDEAL` | `SIMPLEDEAL\t{cards}\t{deckidx}\t{deck_json}` | Convenience: queues `DECK` + per-player `DECKXOR`/`DECKENCRYPT`/`DEAL` for `{cards}` each from JSON deck object, then removes itself. |
| `DEAL` | `DEAL\t{deckidx}\t{recipient}\t{cards}` | Deals `{cards}` to `{recipient}`: async mode deals plaintext immediately; else queues `RESOLVEDEAL` (+ `REQUESTKEYS` from other players). Does not splice itself (cleared by `RESOLVEDEAL`). |
| `SAFEDEAL` | `SAFEDEAL\t{deckidx}\t{recipient}\t{cards}` | Like deal, but if the crypt is short, reshuffles discards into the deck then deals remaining; removes itself and queues the needed `DEAL`/shuffle sequence. |
| `PUSHONDECK` | `PUSHONDECK\t{deckidx}\t{cards_json}` | Queues backup/XOR/encrypt/restore-with-`push` so `{cards_json}` is added on top of deck `{deckidx}`; removes itself. |
| `REQUESTKEYS` | `REQUESTKEYS\t{deckidx}\t{sender}\t{recipient}\t{cards}` | Only `{sender}` runs: broadcasts `ISSUEKEYS` plus `{cards}` key values and `RESOLVE`, then pauses; others wait (`return 0`). |
| `ISSUEKEYS` | `ISSUEKEYS\t{deckidx}\t{sender}\t{recipient}\t{cards}\t{opponent_deck_length}` | Removes itself; `{recipient}` XOR-decodes the next `{cards}` crypt entries using the following `{cards}` key strings on the queue, then splices those keys. |
| `SECUREROLL` | `SECUREROLL\t{player}\t{hash}\t{sig}` | Commit protocol for secure dice: verifies `{sig}` over `{hash}` for `{player}`, collects commits until all players (and initiator double-commit) are present, then sets `game.dice` and clears stacked `SECUREROLL`s. |
| `SECUREROLL_END` | `SECUREROLL_END` | Resets `sroll` / `sroll_hash` / `sroll_done` state and removes itself (sentinel/end of a secure-roll region). |
| `SIMULTANEOUS_PICK` | `SIMULTANEOUS_PICK\t{player}\t{hash_or_card}\t{sig}` | Commit/reveal simultaneous selection: verifies sigs, waits for all players’ three submissions, writes picks into `game.state.sp[]`, then clears stacked `SIMULTANEOUS_PICK`s. |
| `DECKBACKUP` | `DECKBACKUP\t{deckidx}` | Snapshots deck `{deckidx}` (cards/crypt/keys/hand/fhand/discards/removed) into `old_*` fields and removes itself. |
| `HANDBACKUP` | `HANDBACKUP[\t{deckidx}]` | Like backup but only preserves hand/fhand/discards/removed (crypt/keys cleared); `{deckidx}` optional, defaults to `1`. |
| `DECKRESTORE` | `DECKRESTORE[\t{deckidx}[\tpush]]` | Restores `old_*` into deck `{deckidx}` (default `1`); optional third arg `push` appends restored crypt/hand on top, otherwise prepends underneath; clears `old_*` and removes itself. |
| `DECKADDCARDS` | `DECKADDCARDS[\t{deckidx}[\t{cards_json}]]` | Parses optional JSON card map and merges missing keys into `deck[0].cards` (note: code always writes index `0` despite `{deckidx}`), then removes itself. |
| `CARDS` | `CARDS\t{deckidx}\t{cryptLength}` (+ `{cryptLength}` prior queue strings) | Pops `{cryptLength}` following queue entries into `deck[deckidx-1].crypt` (non-observers only) after removing the `CARDS` instruction. |
| `POOL` | `POOL\t{poolidx}` | Ensures pool `{poolidx}` exists, resets it, then removes itself. |
| `SAFEPOOLDEAL` | `SAFEPOOLDEAL\t{deckidx}\t{cards}\t{poolidx}` | Queues `POOLDEAL`, or deal+`SHUFFLEDISCARDS`+remaining deal if crypt is short; removes itself. |
| `POOLDEAL` | `POOLDEAL\t{deckidx}\t{cards}\t{poolidx}` | Convenience flop: queues `FLIPRESET` then per-player `FLIPCARD` for `{cards}` into `{poolidx}`; removes itself. |
| `FLIPRESET` | `FLIPRESET\t{poolidx}` | Ensures pool exists; clears that pool’s crypt/keys and `decrypted` counter; removes itself. |
| `FLIPCARD` | `FLIPCARD\t{deckidx}\t{cardnum}\t{poolidx}\t{playerid}` | Only `{playerid}` runs: broadcasts keys + `RESOLVEFLIP` (or uses `opponent_decks` if present); others wait. |
| `RESOLVEFLIP` | `RESOLVEFLIP\t{deckidx}\t{cardnum}\t{poolidx}` | Consumes the next `{cardnum}` key strings to XOR-decode pool crypt; after all players’ key sets, hex-decodes into pool hand and trims deck crypt/keys. |
| `OBSERVER_CHECKPOINT` | `OBSERVER_CHECKPOINT` | Removes itself; observers (`player==0`) halt/save for checkpoint; players continue. |
| `DECKANDENCRYPT` | `DECKANDENCRYPT\t{deckidx}\t{players}\t{deck_json}` | Convenience: queues `DECK` + XOR/encrypt for each of `{players}` seats using `{deck_json}`; removes itself. |
| `DECK` | `DECK\t{deckidx}\t{cards_json}` | Resets/creates deck `{deckidx}`, applies pending `to_add`/`to_remove`, sets `.cards` from JSON, builds plaintext hex crypt, removes itself. |
| `DECKXOR` | `DECKXOR\t{deckidx}\t{playerid}` | Only `{playerid}`: XOR-blinds crypt with a local xor pad, generates keys, shuffles, broadcasts `CARDS`+crypt; others wait. Skipped entirely when `async_dealing==1`. |
| `DECKFLUSH` | `DECKFLUSH\t{deckidx}[\tdiscards]` | Intended to clear discards when second arg is `discards`; implementation references undefined `qe` when splicing (see notes). |
| `DECKENCRYPT` | `DECKENCRYPT\t{deckidx}\t{playerid}` | Only `{playerid}`: removes xor pad and re-encrypts crypt with per-card keys, broadcasts `CARDS`+crypt; others wait. Skipped when `async_dealing==1`. |
| `null` | `null` | Removes a literal null/`"null"` queue head (no further args). |
| `NFT_EVENT` | `NFT_EVENT\t{nft_id}\t{code_index}[\t{arg}...]` | Engine splices itself **before** running. Looks up `game.options.nfts` by app id, selects `data.code` by integer `{code_index}`, sets `nft.args` from trailing fields, and runs the script via `executeJS` on every browser client. Script `return 0` pauses the queue; otherwise the queue continues. Do **not** enqueue `resolve` to clear this instruction — it is already gone. |