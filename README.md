# Dead Man's Switch — v0.8.32

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
| Free discards | 5 per round. Each discard draws 1 replacement. Paid discards cost 1 hand (2 with The Usurer boss). |
| 7 Dump | Playing a 7 opens a suit dump — play any number of that suit in sequence. If the new middle card is a 7 (player-played or otherwise), the dump opens immediately for the next hand. |
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
- **Score display:** values ≥ 1,000,000,000 shown in scientific notation (e.g. `1.234e9`)

---

## Card Levels

| Level | Colour | Description |
|-------|--------|-------------|
| L0 | White | No power |
| L1 ★ | Steel grey | Power active |
| L2 ★★ | Gold | Enhanced power |
| L3 ★★★ | Blue | Maximum power |

Cards that always start at L1: **A, 2, 7, 8, J**. Black Kings L1; Red Kings L0.

Cards that start at L0 (upgradeable): 3, 4, 5, 6, 9, 10, Q

---

## Card Powers

Stackable powers (★) fire independently for each copy in a same-number stack or trailing chain.

| Card | Stackable | L1 | L2 | L3 |
|------|-----------|----|----|-----|
| **A** | | Declare suit for next card | Declare + draw 1 | Declare + draw 2 |
| **2** | ★ | Draw 2 cards | Draw 4 | Draw 6 |
| **3** | ★ | +3% free relic chance at round end | +6% | +9% |
| **4** | | Return 1 card from discard to hand | Return up to 2 | Return up to 3 |
| **5** | | Passive: +50 pts per hand while held (not played) | +100 pts | +150 pts |
| **6** | ★ | Recover 1 free discard | Recover 2 | Grant +2 extra discards beyond cap |
| **7** | | Opens a suit dump | Dump ×1.5 | Dump ×2 |
| **8** | ★ | +1 hand | +2 hands | +3 hands |
| **9** | ★ | Wild suit — matches anything (no power) | Wild + reshuffle hand, draw 7 | Wild + reshuffle, draw 9 |
| **10** | ★ | +100 pts to next hand scored | +200 pts | +300 pts |
| **J** | | Free play + 1 bonus slot | Free play + draw 1 + 1 bonus slot | Free play + draw 1 + 2 bonus slots |
| **Q** | ★ | Next hand ×2 multiplier (additive) | ×3 per queen | ×4 per queen |
| **K** | ★ | Draw 5 cards | Draw 6 | Draw 7 |

**Jack bonus slots:** Stage additional cards matching the suit OR number of the last non-Jack staged card.

**Queen stacking:** Additive by default. 3× L2 Queens = ×9. Multiplicative with Blood Pact.

**Power Surge relic:** The first power card played each hand fires twice — all draw/recover/hand counts are doubled for that card.

---

## Round Structure

- **24 base game rounds** (Tiers 1–8, 3 rounds per tier). Round 3 of each tier is a Boss Round.
- **30 endless mode rounds** (Tiers 9–18, rounds 25–54) — unlocked after clearing Tier 8.
- Targets scale from 300 pts (R1) to 25,000 pts (R24). Endless targets scale aggressively, roughly tripling each tier from T11 — reaching ~656M at T18 Boss.

### Reward Screen

Choose 2 rewards (3 with The Vault relic): **Add Card · Remove Cards · Upgrade Card · Gain Relic** (boss rounds only).

Boss wins grant +1 reroll charge. Lucky 3 and The Void can grant additional free relic picks.

---

## Relics

One relic is chosen at game start (no legendaries). More are earned through boss rounds and card powers.

### Common

| Relic | Effect |
|-------|--------|
| 💀 Dead Man's Hand | Aces score 200 pts instead of 110. |
| 🔗 Daisy Chain | +25 flat bonus per card after the first in any multi-card hand. |
| 💰 Penny Pincher | Each unused free discard at round end upgrades a random L0 card to L1. |
| ⚡ Swift Hand | +1 extra hand next round per 3 unused hands this round (max +2). |
| 💛 Heart of Gold | Hearts score +20 bonus pts each. |
| 🕳️ Ace in the Hole | After each successful round, a random Ace is added to your deck. |
| 🗑️ Trashman | +1 free discard per round. Stackable. |
| 🎒 Full House | Once per round, discard your entire hand and draw 7 fresh cards. |
| ⚒️ The Anvil | Playing a card matching the middle card's number scores +150 bonus. |
| 🧩 Odd Fit | Cards that match by number only (not suit) score +40 bonus each. |
| 🔭 Gies a Swatch | Deck preview shows cards in draw order instead of sorted. Top 3 labelled Next/2nd/3rd. |
| 🃏 Patient Gambler | Playing a single card draws 2 extra cards at the start of your next turn. |
| 🤖 AI Fingers | Draw back to 8 cards by default instead of 7. |
| 2️⃣ Evens | Even-numbered cards (2, 4, 6, 8, 10) score 50% more base points. |
| 1️⃣ Odds | Odd-numbered cards (A, 3, 5, 7, 9) score 50% more base points. Stacks with Dead Man's Hand (Ace = 300 pts). |
| 🎰 Gambler's Anonymous | 10% chance any hand scores double. Otherwise all hands score 10% less. Preview always shows reduced value. |
| 🎰 Slot Machine | Holding 3+ 7s at hand start grants max(1,000, 20% of target) bonus pts. Once per round. |
| ⚡ Power Surge | The first power card played each hand fires its power twice. |

### Uncommon

| Relic | Effect |
|-------|--------|
| 🃏 The Fool | First hand each round scores ×2. |
| 🩸 Blood Pact | Queens stack multiplicatively (3× L3 = ×64), but each costs 1 extra hand. |
| 🪬 Ward | Once per round, if you run out of hands, prevent it and draw 2 cards instead. |
| 💥 Chain Reaction | Multiple 2s multiply their draw values. L1+L2+L1 = 2×4×2 = 16 drawn. |
| 🪞 Mirror Shard | The first card discarded each round doesn't count against free discards. |
| 🌙 Night Market | See 8 cards instead of 6 for Add, Remove, and Upgrade reward choices. |
| 🦊 Fox's Gambit | Each Jack played draws 1 extra card. |
| 🐰 White Rab | Same-number cards multiply the score: 2 matching = ×2, 3 = ×3, etc. |
| ⚙️ On The Gear | On acquisition: 5 random cards upgraded by 1 level (max L3). |
| 🎲 Fuck That | 3 charges. Re-roll any reward screen option. Destroyed when spent. |
| 🎲 Gambler's Chip | After each hand, one random card in hand is always legal to play. |
| 🔫 Rapid Shooter | In multi-card hands, 2s, 6s, 8s, and Ks not in the last position also fire their power. |
| ⏰ Late Guy | Hands scored with 3 or fewer hands remaining score double. |
| 🗺️ Do Where Labs On? | At round start, play the first middle card yourself from your hand. No score for it. |
| 🔄 Cover My Shift? | Consume to re-roll the current boss. Returns to pool after use. |

### Rare

| Relic | Effect |
|-------|--------|
| 🔍 Treasure Hunter | Lucky 3 chance from 3s doubled (L1: +6%, L2: +12%, L3: +18% per card). |
| 🎯 Sniper | Single-card hands score ×6. |
| 🔥 Wildfire | In a suit dump or chain, every card after the 3rd scores double. |
| 👑 The Crown | Clear a round with ≥1 hand remaining → next round's target −15%. |
| 🌑 Eclipse | Each deck reshuffle during a round scores +3,000 bonus points. |
| 🏦 The Vault | Next 3 rounds after acquisition give 3 reward choices instead of 2. |
| 📒 Can I See Your Logbook? | Duplicate one relic you already own. |
| 🪟 Mirror Image | Duplicates every card in your deck, hand, and discard pile. |
| 🃏 Cunts got cairds? | Pick UP TO 2 cards from Add and Upgrade reward screens each time. |
| 🎨 Colorblind | Spades/clubs treated as same suit. Hearts/diamonds treated as same suit. |
| 👑 On Yersel Hen! | Each Queen held in hand (not played) multiplies the final hand score by ×1.5. |

### Legendary

| Relic | Effect |
|-------|--------|
| 🪨 Philosopher's Stone | Hand size bonuses doubled: ×1.5→×3, ×2→×4, ×3→×6, ×5→×10. |
| 🐍 Hydra | For every card discarded, draw 2 additional cards from the deck. |
| 🌌 The Void | Each deck reshuffle during a round grants a free relic choice at round end. |
| 🌊 Crimson Tide | Every Queen played permanently increases all future Queen multipliers by ×1. |
| 🔢 Dyscalculia | Every card scores exactly 250 base points. |

---

## Bosses

| Boss | Effect | Target |
|------|--------|--------|
| ⛓️ The Warden | Max hand size reduced to 12. | 100% |
| 💸 The Usurer | Paid discards cost 2 hands each. | 100% |
| 🎯 The Marksman | Dealt 26 cards; 1 hand; 5 free discards. | 90% |
| 🩸 The Hexer | A random number treated as L0 for this round. | 85% |
| ⏳ The Eroder | Each hand scores 10% less (floor 30%). | 65% |
| 🔒 The Purist | Suit matching only; number matching disabled. | 65% |
| ⚗️ The Alchemist | All L0 cards removed for this round. | 140% |
| ✊ The Anarchist | All J/Q/K removed for this round. | 70% |
| 🔵 Performance Anxiety | 1 relic disabled per 6 rounds into the run. Restored after win. | 85% |
| ✂️ Halfman | All final hand scores halved. | 65% |
| 👕 Casual Wear! | All cards playable on any middle card regardless of suit. | 170% |
| ⚡ Legend Killer | Target greatly increased. Guarantees a Legendary relic choice. | 175% |
| 🧈 Butter Fingers | After each hand, 1 random card discarded from your hand. | 80% |
| 🟥 Surface-Level Communism | Card levels, tooltips, and suit colours hidden. | 80% |
| 🚫 No Mimics | Last hand's number(s) cannot be played next hand. | 75% |
| ⚡ Overclock | Hands score ×2, but 20% chance of scoring nothing. | 100% |
| 🗑️ Dr. Wilson | Fixed target (400 pts / 1,000 endless). Every card played permanently destroyed. | — |
| 👾 Glitch | Middle card suit randomised at the start of every hand. | 75% |
| 🪟 Glass Ceiling | Per-hand score capped by tier: 500 (T1–4) · 1,000 (T5–6) · 2,500 (T7–8) · ×2.5 per 2 tiers thereafter. | 50% |
| 🃏 The Joker | Jokers added to deck. Each turn held: −X pts. Playing one: −3X. X = tier × 100. | 85% |
| 🚿 Leaky Pisser | Each paid discard subtracts 5% of target from current score. | 75% |
| 🔁 Feedback Loop | Remaining hand shuffled back into deck after each hand; redraw same count. | 110% |

---

## Legacy System (Meta-Progression)

Progress persists across runs via `localStorage`.

- **Relic Memory:** Every 3 bosses beaten earns 1 legacy relic pick. On Play Again, choose relics from your current run to carry forward. 6 bosses = 2 picks, 9 = 3, etc.
- **Carried relics** are active from the first hand of the new run, before your starting relic pick.
- **Export / Import:** Save data as JSON (copied to clipboard). Importable on any browser.
- **Reset:** All legacy progress clearable from the title screen.
