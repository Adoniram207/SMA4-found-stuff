# SMA4 Found Stuff
### Super Mario Advance 4: Super Mario Bros. 3 (GBA) — Unofficial Research Document

> Discovered and documented by **Adoniram207**  
> Game version: USA (v1.1)  
> Format: CodeBreaker (decrypted) unless noted

---

## Master Code (required for all CodeBreaker codes)

```
000021FA 000A
10002884 0007
```

---

## 1. e-Reader Switch System (`83002D52`)

The game stores all switch effects at address `83002D52`. Each bit controls a different feature. Most were only available in Japan via physical e-Reader cards. Some were never released at all.

**To activate switches, add the hex values of the ones you want.**

Example — activate all: `83002D52 FFFF`

### USA — Officially available via e-Reader

| Hex value | Switch name | Effect |
|-----------|-------------|--------|
| `+0001` | Blue-Green Switch | Adds throwable vegetables from Super Mario Bros. 2 to the main game |
| `+0040` | Orange Switch | Enemies hit by fireballs turn into coins |

### Japan only — Requires Japan e-Reader cards

| Hex value | Switch name | Effect |
|-----------|-------------|--------|
| `+0002` | Cyan Switch | P-Meter fills at half speed, harder to fly |
| `+0010` | Green Switch | In-level timer counts down more slowly |
| `+0080` | Red Switch (Famicom damage) | Mario reverts to small form on any hit, regardless of power-up |
| `+0100` | Yellow Switch | Luigi's unique physics from the original game are active in the main game |
| `+0200` | Red Switch (x2 points) | All points earned are doubled |
| `+0400` | Blue Switch (3-Up Moons) | 1-Up Mushrooms are replaced by 3-Up Moons from Super Mario World |
| `+0800` | Red Switch (harder enemies) | Several map enemies are replaced by stronger versions |
| `+2000` | Red Switch (double boss HP) | All bosses require twice as many hits to defeat |

### Unused — In the code but no e-Reader card was ever made

| Hex value | Effect |
|-----------|--------|
| `+0004` | All 1-Up blocks give three mushrooms instead of one |
| `+0008` | Hold Box mechanic from Super Mario World |
| `+0020` | Enemy point chain starts at 4000 instead of 100 |
| `+1000` | Floating platform rescue (no documented effect) |
| `+4000` | Luigi replaces Mario in level replays |

### Bit 15 — Mega Switch (discovered by Adoniram207)

```
83002D52 FFFF
```

Setting bit 15 (`+8000`) along with all other bits activates **every switch simultaneously**, including all Japan-only and unused features. This was not documented in any official or community RAM map prior to this discovery. The value `FF9D` is a known stable subset.

---

## 2. Inventory Item Codes

Address `33002C2E` controls Mario's inventory slot #1. Slots are sequential from there.

### Item value table

| Hex value | Item |
|-----------|------|
| `00` | Empty |
| `01` | Super Mushroom |
| `02` | Fire Flower |
| `03` | Super Leaf |
| `04` | Frog Suit |
| `05` | Tanooki Suit |
| `06` | Hammer Suit |
| `07` | Lakitu's Cloud |
| `08` | P-Wing |
| `09` | Super Star |
| `0A` | Anchor |
| `0B` | Hammer |
| `0C` | Warp Whistle |
| `0D` | Music Box |
| `0E` | **Cape Feather** ← e-Reader exclusive |
| `0F` | Boomerang |

> Values `07`, `0E`, and `0F` may behave unexpectedly when obtained outside of their intended e-Reader context.

### Mario inventory slots (CodeBreaker, all 15 items)

```
33002C2E 0001   Slot 1  — Super Mushroom
33002C2F 0002   Slot 2  — Fire Flower
33002C30 0003   Slot 3  — Super Leaf
33002C31 0004   Slot 4  — Frog Suit
33002C32 0005   Slot 5  — Tanooki Suit
33002C33 0006   Slot 6  — Hammer Suit
33002C34 0007   Slot 7  — Lakitu's Cloud
33002C35 0008   Slot 8  — P-Wing
33002C36 0009   Slot 9  — Super Star
33002C37 000A   Slot 10 — Anchor
33002C38 000B   Slot 11 — Hammer
33002C39 000C   Slot 12 — Warp Whistle
33002C3A 000D   Slot 13 — Music Box
33002C3B 000E   Slot 14 — Cape Feather
33002C3C 000F   Slot 15 — Boomerang
```

### Luigi inventory slots

Luigi's inventory starts at `33002C59` with the same item values.

```
33002C59 000E   Slot 1 — Cape Feather (Luigi)
```

---

## 3. Active Power-Up Codes

Address `33003F5B` controls the current active power-up on the player. Values differ from the inventory table.

| Hex value | Power-up |
|-----------|----------|
| `00` | Small |
| `01` | Big |
| `02` | Fire |
| `03` | Raccoon |
| `04` | Frog |
| `05` | Tanooki |
| `06` | Hammer |
| `07` | Cape |

### Button-activated power-up codes (CodeBreaker)

```
Press L + Up    — Fire Mario
74000130 01BF
33FE6400 0002
73FE6400 0002
33003F5F 0002

Press L + Down  — Leaf/Raccoon Mario
74000130 017F
33FE6400 0003
73FE6400 0003
33003F5F 0003

Press L + Left  — Frog Mario
74000130 01DF
33FE6400 0004
73FE6400 0004
33003F5F 0004

Press R + Up    — Hammer Bros. Mario
74000130 02BF
33FE6400 0006
73FE6400 0006
33003F5F 0006

Press R + Down  — Cape Mario
74000130 027F
33FE6400 0007
73FE6400 0007
33003F5F 0007

Press R + Right — Raccoon Mario
74000130 01EF
33FE6400 0005
73FE6400 0005
33003F5F 0005
```

---

## 4. Miscellaneous Codes

```
Stop Timer:           33003D0E 0020
P-Meter Always Full:  33003C9F 007F
                      33003F48 00FF
P-Switch Infinite:    33003CF8 00FF
Invulnerability:      33003F64 0035
Infinite Lives (M):   33002A6A 0062
Infinite Lives (L):   33002A6C 0062
```

---

## 5. RAM Map Reference (key addresses)

| Address | Description |
|---------|-------------|
| `03002A6A` | Lives count (Mario) |
| `03002A6C` | Lives count (Luigi) |
| `03002C2E` | Mario inventory slot #1 |
| `03002C59` | Luigi inventory slot #1 |
| `03002D52` | Switch effects bitmask |
| `03003C9F` | P-speed |
| `03003CF8` | P-Switch timer |
| `03003D0E` | Level timer |
| `03003F5B` | Current power-up |
| `03003F60` | Invulnerability timer |

Full RAM map: [Data Crystal](https://datacrystal.tcrf.net/wiki/Super_Mario_Advance_4:_Super_Mario_Bros._3/RAM_map)

---

## Sources

- Data Crystal RAM Map (official community documentation)
- Almar's Guides CodeBreaker codes
- GameHacking.org forum (DarkSerge, Sappharad)
- Personal research by Adoniram207

---

*This document is unofficial and not affiliated with Nintendo.*
