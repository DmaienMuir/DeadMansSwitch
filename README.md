# Dead Man's Switch — v0.8.27

A survival roguelike built on Switch card game rules. Single HTML file, no dependencies.

---

## How to Play

Each turn you play one card (or a valid combination) from your hand onto the middle card. A card is legal if it matches the middle card's **suit** or **number**. The middle card updates after every play. Draw back to your hand size cap after each card played.

Beat the round's score target before you run out of hands.

---

## Core Rules

| Rule | Detail |
|------|--------|
| Hand size cap | `ceil(totalCards / 2)` where totalCards = deck + hand + discard |
| Free discards | 4 per round. Each discard draws 1 replacement. Paid discards cost 1 hand (2 with The Usurer boss). |
| 7 Dump | Playing a 7 opens a suit dump — play any number of cards of that suit in sequence. Only the final card fires its power (except 3s). |
| Same-number stack | Multiple cards of the same number played simultaneously. Each stackable power fires independently. |
| Jack chain | Jacks don't consume a hand. They grant bonus slots for follow-up cards. |
| Ace | Always playable. Declares the active suit for the next card. |
| Wild 9 (L1+) | Matches any suit or number. |
| Full Hand bonus | ×3 if every card in hand is played in one turn. |

---

## Scoring

- **Number cards (2–10):** face value × 10 pts
- **A, J, Q, K:** 110 pts each
- **Hand-size multipliers:** 3 cards ×1.5 · 5 cards ×2 · 7 cards ×3 · 10 cards ×5
- **Full Hand bonus:** ×3 (applied after all other multipliers)

---

## Card Levels

| Level | Colour | Description |
|-------|--------|-------------|
| L0 | White | No power |
| L1 ★ | Steel grey | Power active |
| L2 ★★ | Gold | Enhanced power |
| L3 ★★★ | Blue | Maximum power |

Cards that always start at L1: **A, 2, 7, 8, J**

Black Kings start at L1; Red Kings start at L0.

Cards that start at L0 (can be upgraded): 3, 4, 5, 6, 9, 10, Q

---

## Card Powers

Stackable powers (★) fire independently for each card of that number in a same-number stack or trailing chain.

| Card | Stackable | L1 | L2 | L3 |
|------|-----------|----|----|-----|
| **A** | | Declare suit for next card | Declare + draw 1 | Declare + draw 2 |
| **2** | ★ | Draw 2 cards | Draw 4 cards | Draw 6 cards |
| **3** | ★ | +3% free relic chance at round end | +6% | +9% |
| **4** | | Return 1 card from discard to hand | Return up to 2 | Return up to 3 |
| **5** | | Passive: +50 pts per hand while held in hand (not played) | +100 pts | +150 pts |
| **6** | ★ | Recover 1 free discard | Recover 2 free discards | Grant +2 extra discards beyond cap |
| **7** | | Opens a suit dump | Dump scores ×1.5 | Dump scores ×2 |
| **8** | ★ | +1 hand | +2 hands | +3 hands |
| **9** | ★ | Wild suit — matches anything (no power) | Wild + reshuffle hand, draw 7 | Wild + reshuffle hand, draw 9 |
| **10** | ★ | +100 pts added to next hand scored | +200 pts | +300 pts |
| **J** | | Free play (no hand cost) + 1 bonus slot | Free play + draw 1 + 1 bonus slot | Free play + draw 1 + 2 bonus slots |
| **Q** | ★ | Next hand ×2 multiplier (additive stacking) | ×3 per queen | ×4 per queen |
| **K** | ★ | Draw 5 cards | Draw 6 cards | Draw 7 cards |

**Jack bonus slots:** After a Jack, bonus slots let you stage additional cards matching the suit OR number of the last non-Jack staged card.

**Queen stacking (default):** Additive. Playing 3× L2 Queens = ×9 on the next hand. With Blood Pact relic: multiplicative.

**7 and open middles:** If the new middle card after any play is a 7, the dump immediately becomes available for the next hand.

---

## Round Structure

- **24 base game rounds** (Tiers 1–8, 3 rounds per tier). Round 3 of each tier is a Boss Round.
- **30 endless mode rounds** (Tiers 9–18, rounds 25–54) — unlocked after clearing Tier 8.
- Score targets scale from 300 pts (R1) to 25,000 pts (R24) in the base game, and up to 5,400,000 pts (R54) in endless mode.

### Reward Screen (after each round)

Choose 2 rewards (3 with The Vault relic):

- **Add Card** — add 1 card to your deck
- **Remove Cards** — remove up to 2 cards from your deck
- **Upgrade Card** — upgrade 1 card by 1 level (max L3)
- **Gain Relic** — choose 1 relic (boss rounds only, not round 24)

Boss wins also grant +1 reroll charge, usable on any reward screen option.

---

## Relics

Relics are persistent bonuses that last the entire run. One relic is chosen at the start of each run; more are earned through boss rounds.

### Common

| Relic | Effect |
|-------|--------|
| 💀 Dead Man's Hand | Aces score 200 pts instead of 110. |
| 🔗 Daisy Chain | Each card after the first in any multi-card hand adds +25 flat bonus. |
| 💰 Penny Pincher | Each unused free discard at round end upgrades a random L0 card to L1. |
| ⚡ Swift Hand | Gain +1 extra hand next round for every 3 unused hands this round (max +2). |
| 💛 Heart of Gold | Hearts score +20 bonus pts each. |
| 🕳️ Ace in the Hole | After each successful round, a random Ace is added to your deck. |
| 🗑️ Trashman | +1 free discard per round. Stackable — each copy adds another +1. |
| 🎒 Full House | Once per round, discard your entire hand and draw 7 fresh cards. |
| ⚒️ The Anvil | Playing a card that matches the middle card's number scores +150 bonus. |
| 🧩 Odd Fit | Cards that match by number only (not suit) each score +40 bonus. |

### Uncommon

| Relic | Effect |
|-------|--------|
| 🃏 The Fool | First hand played each round scores ×2. |
| 🩸 Blood Pact | Queens stack multiplicatively instead of additively (3× L3 Queens = ×64), but each Queen costs 1 extra hand. |
| 🪬 Ward | Once per round, if you would run out of hands, prevent it and draw 2 cards instead. |
| 💥 Chain Reaction | Playing multiple 2s together multiplies their draw values instead of adding. e.g. L1+L2+L1 = 2×4×2 = 16 cards drawn. |
| 🌙 Night Market | See 8 cards instead of 6 for Add, Remove, and Upgrade reward choices. |
| 🦊 Fox's Gambit | Each Jack played draws 1 extra card. |
| 🐰 White Rab | Same-number cards in a hand multiply the score: 2 matching = ×2, 3 = ×3, and so on. |
| ⚙️ On The Gear | On acquisition: 5 random cards in your deck are upgraded by 1 level (max L3). |
| 🎲 Fuck That | 3 charges. Re-roll any reward screen option. When all 3 are used, relic is destroyed and returns to the pool. |
| 🎲 Gambler's Chip | After each hand, one random card in your hand is always legal to play. |
| 🔫 Rapid Shooter | In multi-card hands, 2s, 6s, 8s, and Ks that are not the last card also fire their power. |
| ⏰ Late Guy | Hands scored with 3 or fewer hands remaining score double. |
| 🗺️ Do Where Labs On? | At the start of each round, play the first middle card yourself from your hand. You score no points for it. |
| 🔄 Cover My Shift? | Consume to re-roll the current boss. Button appears on the boss splash screen. Returns to pool after use. |

### Rare

| Relic | Effect |
|-------|--------|
| 🔍 Treasure Hunter | Lucky 3 chance from 3s is doubled (L1: +6%, L2: +12%, L3: +18% per card). |
| 🎯 Sniper | Single-card hands score ×6. |
| 🔥 Wildfire | In a suit dump or chain, every card after the 3rd scores double. |
| 👑 The Crown | If you clear a round with at least 1 hand remaining, the next round's target is reduced by 15%. |
| 🌑 Eclipse | Each time your deck reshuffles during a round, score +3,000 bonus points. |
| 🏦 The Vault | For the next 3 rounds after acquisition, you get 3 reward choices instead of 2. |
| 📒 Can I See Your Logbook? | Choose one relic you already own — its effect is duplicated. |
| 🪟 Mirror Image | Immediately duplicates every card in your deck, hand, and discard pile. |
| 🃏 Cunts got cairds? | Pick UP TO 2 cards from the Add and Upgrade reward screens each time. |
| 🎨 Colorblind | Spades and clubs are treated as the same suit. Hearts and diamonds are treated as the same suit. |
| 👑 On Yersel Hen! | Each Queen held in hand (not played) multiplies the final score of the played hand by ×1.5. |

### Legendary

| Relic | Effect |
|-------|--------|
| 🪨 Philosopher's Stone | Multi-card hand size bonuses are doubled: ×1.5→×3, ×2→×4, ×3→×6, ×5→×10. |
| 🐍 Hydra | For every card you discard, draw 2 additional cards from the deck. |
| 🌌 The Void | Each time your deck reshuffles during a round, gain a free relic choice at the end of that round. |
| 🌊 Crimson Tide | Every Queen played permanently increases all future Queen multipliers by ×1 (stacks across rounds). |
| 🔢 Dyscalculia | Every card scores exactly 250 base points, regardless of its number. |

---

## Bosses

Each boss round modifies the rules for that round. Bosses are shuffled randomly into the 8 boss slots per run; a fresh shuffle is applied for endless mode.

| Boss | Effect | Target |
|------|--------|--------|
| ⛓️ The Warden | Max hand size reduced to 12. | 100% |
| 💸 The Usurer | Paid discards cost 2 hands each instead of 1. | 100% |
| 🎯 The Marksman | Dealt 26 cards; must beat target in a single hand; 5 free discards. | 90% |
| 🩸 The Hexer | A random card number is treated as L0 for this round. | 85% |
| ⏳ The Eroder | Each successive hand scores 10% less (floor 30%). Hand 1=100%, Hand 2=90%… | 65% |
| 🔒 The Purist | Only suit matching allowed; number matching and same-number stacking disabled. | 65% |
| ⚗️ The Alchemist | All L0 cards removed from deck for this round. | 140% |
| ✊ The Anarchist | All Jacks, Queens, and Kings removed from deck for this round. | 70% |
| 🔵 Performance Anxiety | 1 relic disabled per 6 rounds travelled into the run. Restored after the round. | 85% |
| ✂️ Halfman | All final hand scores are halved after all other bonuses. | 65% |
| 👕 Casual Wear! | All cards playable on any middle card regardless of suit. | 170% |
| ⚡ Legend Killer | Target score greatly increased. Clearing guarantees a Legendary relic choice. | 175% |
| 🧈 Butter Fingers | After each hand, 1 random card is discarded from your hand. | 80% |
| 🟥 Surface-Level Communism | Card levels, tooltips, and suit colours are hidden. Powers still function. | 80% |
| 🚫 No Mimics | The number(s) played in your last hand cannot be played in the next hand. | 75% |
| ⚡ Overclock | All hands score ×2, but 20% chance any given hand scores nothing. | 100% |
| 🗑️ Dr. Wilson | Fixed target (400 pts base / 1,000 pts endless). Every card played is permanently destroyed. | — |
| 👾 Glitch | At the start of every hand, the middle card's suit is randomised. | 75% |
| 🪟 Glass Ceiling | Per-hand score capped (500 Tiers 1–4 · 1,000 Tiers 5–6 · scales ×2.5 per 2 tiers from Tier 7). | 50% |
| 🃏 The Joker | Joker cards added to deck. Each turn one is held: −X pts. Playing one: −3X pts. X = tier × 100. | 85% |
| 🚿 Leaky Pisser | Each paid discard subtracts 5% of the target score from your current score. Free discards unaffected. | 75% |
| 🔁 Feedback Loop | After each hand, your remaining hand is shuffled back into the deck and you redraw the same number. | 110% |

---

## Legacy System (Meta-Progression)

Progress persists across runs via `localStorage`.

- **Relic Memory:** For every 3 bosses beaten in a run, you earn 1 legacy relic pick. After clicking Play Again, you are shown up to 3 of your current relics and choose 1 to carry into the next run. 6 bosses = 2 picks, 9 bosses = 3 picks, and so on.
- **Carried relics** are active from the first hand of the new run, before your starting relic pick.
- **Export / Import:** Save data can be exported as JSON (copied to clipboard) and imported on another device or browser.
- **Reset:** All legacy progress can be cleared from the title screen.
