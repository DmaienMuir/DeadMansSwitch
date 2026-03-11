# Dead Man's Switch

A single-player roguelike deck-builder built on the rules of **Switch**. Play cards to beat a score target each round. Upgrade your deck and collect relics between rounds to survive all 24 levels.

Vibe-coded using Claude Sonnet 4.6, with the intention of making an addictive game that is a mix of Scottish house-rules Switch and Balatro, with a few elements of Slay the Spire. I accept no responsibility for any bugs. They will be fixed or they will not, depending on the whims of Claude. The existance of this game is in no way an endorsement of generative AI, which is slowly killing our planet and eroding clever people's ability to think.

---

## How to Play

[Play the game here!](https://dmaienmuir.github.io/DeadMansSwitch/index.html)

---

## Core Rules

A card is **legal** to play if it matches the middle card by **suit** or **number**.

- Play one card (or a legal group) per hand.
- After each play, draw back up to your hand size cap.
- Each round: **8 hands**, **4 free discards**.
- Discards beyond the free limit cost **1 hand** each.
- **Hand size cap** = ⌈(deck + hand + discard) / 2⌉. Pack Rat relic adds +4.
- Double-click or double-tap a legal card to stage it.

### Special Cards

| Card | Rule |
|------|------|
| **Ace** | Always legal. You declare the active suit for the next card. |
| **7** | Opens a suit dump — following cards must match the 7's suit. |
| **Jack** | Always legal after another Jack. Does **not** cost a hand. |
| **Same-number stack** | Multiple cards of the same number can be played together as one hand. |

### 7-Dump Rules

- Cards must match the opening 7's suit (strict suit-only).
- Jacks can be played mid-dump. If it matches the dump suit it stays in; if not, it exits into jack chain mode.
- Aces are always chainable. An off-suit Ace is terminal (only further Aces may follow).
- Only the **final card** fires its power — except Threes, which always fire.
- Trailing same-number stacks at the end of a dump each fire their own power.

### Jack Chain Rules

- After a Jack, non-J/A cards must match the Jack's suit.
- **L2 Jack** grants 1 bonus staging slot. **L3 Jack** grants 2. In a bonus slot the next card may match by suit *or* number of the last non-Jack played.
- Aces after Jacks enter ace mode — only more Aces may follow.

---

## Scoring

| Card | Points |
|------|--------|
| 2 – 10 | Face value × 10 |
| A, J, Q, K | 110 each |

### Hand-Size Multipliers

| Cards Played | Multiplier |
|---|---|
| 3 | ×1.5 |
| 5 | ×2 |
| 7 | ×3 |
| 10+ | ×5 |
| **Full Hand** (every card played at once) | ×3 (applied after all other multipliers) |

---

## Card Powers

Cards have levels L0–L3. L0 cards have no power. Cards gain power at L1 and improve at L2 and L3.

**Default starting levels:**
- L1 from the start: A, 2, 7, 8, J, black Kings (♠♣)
- L0 from the start: 3, 4, 5, 6, 9, 10, Q, red Kings (♥♦)

Cards marked **STACKABLE** (★) fire their power once per copy in a same-number stack or a trailing stack at the end of a dump or chain.

| Card | L1 | L2 | L3 | Notes |
|------|----|----|-----|-------|
| **A** | Declare suit | Declare + draw 1 | Declare + draw 2 | Always legal |
| **2** ★ | Draw 2 | Draw 4 | Draw 6 | Chain Reaction relic multiplies instead of adds |
| **3** ★ | +3% free relic chance | +6% | +9% | Fires always regardless of position. Chance rolls at round end. |
| **4** | Return 1 from discard | Return up to 2 | Return up to 3 | Cannot salvage other 4s |
| **5** | Passive: +50 pts/hand while held | +100 | +150 | Bonus fires when 5 is in hand but unplayed |
| **6** ★ | Recover 1 free discard | Recover 2 | +2 extra discards beyond cap | |
| **7** | Open dump | Dump ×1.5 | Dump ×2 | Multiple L2/L3 7s multiply: L2+L3=×3, L3+L3=×4 |
| **8** ★ | +1 hand | +2 hands | +2 hands + draw 1 | Playing 8 doesn't cost a hand |
| **9** | Shuffle + draw 7 | Shuffle + draw 8 | Shuffle + draw 9 | |
| **10** ★ | +100 pts next hand | +200 | +300 | Multiple 10s stack additively |
| **J** | Free play | Free + draw 1 + 1 bonus slot | Free + draw 2 + 2 bonus slots | |
| **Q** | Next hand ×2 | Next hand ×3 | Next hand ×4 | Stack multiplicatively: L1+L1=×4, L3+L3=×16 |
| **K** ★ | Draw 5 | Draw 6 | Draw 7 | Black Kings start L1, red Kings start L0 |

---

## Rounds

24 rounds total. Boss rounds: **3, 6, 9, 12, 15, 18, 21, 24**.

| Round | Target | | Round | Target | | Round | Target |
|---|---|---|---|---|---|---|---|
| 1 | 300 | | 9 ★ | 2,450 | | 17 | 9,500 |
| 2 | 420 | | 10 | 2,950 | | 18 ★ | 11,000 |
| 3 ★ | 560 | | 11 | 3,500 | | 19 | 12,500 |
| 4 | 800 | | 12 ★ | 4,300 | | 20 | 14,500 |
| 5 | 1,000 | | 13 | 5,100 | | 21 ★ | 17,000 |
| 6 ★ | 1,250 | | 14 | 6,000 | | 22 | 19,500 |
| 7 | 1,550 | | 15 ★ | 7,100 | | 23 | 22,000 |
| 8 | 2,000 | | 16 | 8,500 | | 24 ★ | 25,000 |

---

## Between Rounds

After clearing a round choose **2 rewards** (3 with The Vault):

- **Add** — add a card to your deck (boss rounds guarantee L1+)
- **Subtract** — remove up to 2 cards from your deck
- **Upgrade** — upgrade a card by one level (max L3)
- **Relic** — choose one of 3 relics to keep *(boss rounds only)*

**Lucky Three:** If 3s were played during the round, accumulated relic chance is rolled at round end. On a success you get a bonus free relic pick before the normal reward screen.

---

## Bosses

One of eight bosses is assigned to each boss round in a shuffled order.

| Boss | Effect | Target |
|------|--------|--------|
| ⛓️ The Warden | Max hand size capped at 12 | ×1.00 |
| 💸 The Usurer | Paid discards cost 2 hands instead of 1 | ×1.00 |
| 🎯 The Marksman | Dealt 26 cards. One hand to win. 5 free discards. | ×0.85 |
| 🩸 The Hexer | A random number is treated as L0 for the round | ×0.85 |
| ⏳ The Eroder | Each hand scores 10% less (floor 30%) | ×0.65 |
| 🔒 The Purist | Suit-only matching. Same-number stacking disabled. | ×0.85 |
| ⚗️ The Alchemist | All L0 cards removed for the round | ×1.40 |
| ✊ The Anarchist | All J, Q, K removed for the round | ×0.70 |

---

## Relics

### Common
| Relic | Effect |
|-------|--------|
| 💀 Dead Man's Hand | Aces score 200 pts instead of 110 |
| 🔗 Daisy Chain | +25 pts per card after the first in any multi-card hand |
| 💰 Penny Pincher | Each unused free discard at round end upgrades a random L0 card to L1 |
| ⚡ Swift Hand | +1 extra hand next round per 3 unused hands this round (max +2) |
| 📖 Dusty Tome | Jacks score +50 pts each |
| 💛 Heart of Gold | Hearts score +20 pts each |
| 🕳️ Ace in the Hole | A random Ace added to deck after each successful round |
| 🗑️ Trashman | +1 free discard per round. Stackable. |
| ♣️ Club House | Clubs score +20 pts each |
| ♠️ Spade Work | Spades score +20 pts each |
| ♦️ Diamond Eye | Diamonds score +20 pts each |
| ⭐ Tin Star | Queens score +50 pts each |
| 🐀 Pack Rat | +4 to maximum hand size |
| 🐇 Rabbit Foot | Draw 1 extra card when you draw the last card from the deck |
| 🎒 Full House | Once per round: discard your entire hand and draw 7 fresh cards |
| 🧩 Odd Fit | Cards matching by number only (not suit) score +40 bonus each |
| ⚒️ The Anvil | Single card matching middle card's number scores +150 bonus |

### Uncommon
| Relic | Effect |
|-------|--------|
| 🃏 The Fool | First hand each round scores ×2 |
| 🩸 Blood Pact | Queens multiply ×3 instead of ×2, but cost 1 extra hand |
| 🪬 Ward | Once per round: prevent running out of hands, draw 2 instead |
| 💥 Chain Reaction | Multiple 2s multiply draw values instead of adding |
| 🪞 Mirror Shard | First discard each round doesn't count against free discard limit |
| 🌙 Night Market | Reward screens show 8 options instead of 6 |
| 🦊 Fox's Gambit | Each Jack played draws 1 extra card |
| 🐰 White Rab | Same-number group in a hand multiplies score (2 matching = ×2, 3 = ×3 …) |
| ⚙️ On The Gear | On acquisition: upgrade 5 random cards by one level |
| 🎲 Fuck That | 3 charges to re-roll any reward option. Destroyed when exhausted. |
| 🎲 Gambler's Chip | After each hand, one random card in hand is always legal next turn |
| 🗺️ Do Where Labs On? | You play the first middle card yourself at round start (no points) |

### Rare
| Relic | Effect |
|-------|--------|
| 🎯 Sniper | Single-card hands score ×3 |
| 🔥 Wildfire | In a dump or chain, every card after the 3rd scores double |
| 👑 The Crown | Clear with 1+ hand remaining → next round's target −15% |
| 🌑 Eclipse | Once per round: empty deck auto-reshuffles the discard pile |
| 🏦 The Vault | Next 3 rounds give 3 reward choices instead of 2 |
| 📒 Can I See Your Logbook? | Duplicate an owned relic's effect |
| 🪟 Mirror Image | Immediately doubles every card in your deck, hand, and discard |
| 🎨 Colorblind | ♠/♣ treated as same suit. ♥/♦ treated as same suit. |
| 👑 On Yersel Hen! | +100 pts per unplayed Queen held in hand, every hand |
| 🃏 Cunts got cairds? | Pick **up to 2 cards** from Add and Upgrade reward screens |

### Legendary
| Relic | Effect |
|-------|--------|
| 🪨 Philosopher's Stone | Every card scores at least 100 pts |
| 🐍 Hydra | Every discard draws 3 additional cards |
| 🌌 The Void | Deck never truly empties — discard reshuffles in every time |
| 🌊 Crimson Tide | Each Queen played permanently raises all future Queen base multipliers by +1 |

---

## Version

v0.7.10
