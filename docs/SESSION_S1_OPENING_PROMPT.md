# SESSION S1 — OPENING PROMPT

> Paste this as your first message to Sonnet in Claude Code.

---

## Context

You're starting Session 1 of Showrunner — a soap-opera engine where the player curates a cast of dots and an algorithmic Drama Director generates intertwining arcs across battles. Combat is content; relationships are the show.

Read these first, in order:
1. `CLAUDE.md` — project conventions and hard rules
2. `docs/SPEC_SHOWRUNNER_v0.2.md` — full design (you don't need every section yet; focus on Parts I, IX, XII, XIII)

## Goal of S1

Ship the combat substrate and a single playable battle. **Slot machine dopamine layer at full strength.** No relationships, no chronicle yet, no patron mechanics. Just: tap battle button, watch dots fight, see hit tiers fire, see win-prob bar swing, see one team win.

## What to build

**Project scaffold:**
- Vite + React (JSX, not TS)
- Mobile-first portrait layout
- localStorage stubs in place (don't use yet)
- Hot-reload dev server working

**Files (target, not strict):**
- `src/main.jsx` — entry
- `src/App.jsx` — root, currently just renders BattleView
- `src/engine/constants.js` — tunable knobs in one place
- `src/engine/dots.js` — Dot factory, properties, naming
- `src/engine/combat.js` — damage formula, hit tier roll, conversion roll, win-prob calc
- `src/engine/ai.js` — behavior modules (4 for S1: engage_nearest, flee_threat, retreat_low_hp, idle), decision aggregation
- `src/engine/sim.js` — battle tick loop, dot updates, collision
- `src/ui/BattleView.jsx` — canvas + HUD + battle button + speed toggle

## S1 spec details

**Roster:** 8 dots per team, 2 teams = 16 dots per battle. Pick names from a 50-name pool. Greek-letter team labels (α, β, γ, δ — only 2 used in S1).

**Stats per dot:**
- HP (40-80), maxHP
- ATK (10-25), DEF (5-15), SPD (1.5-3.0 px/tick)
- range (24-48 px), aggression (0-1), morale (0-1)
- role: frontline | ranged (S1 only ships these two; healer/skirmisher in S3+)
- team, color (team-colored), position {x, y}, velocity {vx, vy}
- target id, lastHit tick

**Hit tier roll (this is the dopamine):**
- 15% glance (×0.5 dmg)
- 70% normal (×1.0)
- 12% solid (×1.4)
- 2.5% crit (×1.8)
- 0.5% landmark (×2.5) → **400ms slow-mo + visual burst**

**Damage formula:** `max(1, floor((ATK - DEF/2) × hitTierMult))`

**Behavior modules (S1, 4 only):**
- `engage_nearest(dot, world) → {move: vec, action: {type:'attack', targetId} | null, weight}`
- `flee_threat(dot, world) → ...` (active when HP/maxHP < 0.4 and threat within 80px)
- `retreat_low_hp(dot, world) → ...` (active when HP/maxHP < 0.25)
- `idle(dot, world) → ...` (fallback)

Each returns weighted move vector + optional action. Aggregate: vector-sum movement, winner-take-all action with hysteresis (don't switch action targets within 200ms unless current target dead/out-of-range).

**Win-prob bar:**
Monte Carlo 100 trials at battle start, recompute every 2 seconds. Show as horizontal bar at top of HUD, animated transitions. Trial = run a fast deterministic sim with current state, count wins.

**Battle end:** all dots of one team dead = other team wins. Display "α wins" banner, fade in. Battle button re-enables after 1.5s.

**UI layout (portrait):**
```
┌─────────────────────────┐
│ Win-prob:  α━━━━●━━ β   │  ~50px HUD top
│ B12 · t=23s · 1×        │
├─────────────────────────┤
│                         │
│   battlefield canvas    │  ~400px square, fit width
│   (no pan, no zoom)     │
│                         │
├─────────────────────────┤
│ [BATTLE]  [1× / 2× / 4×]│  ~80px action row
└─────────────────────────┘
```

Speed toggle = sim ticks per frame. 1× = 1, 2× = 2, 4× = 4. Default 2×.

**Visual:**
- Canvas 2D, 360×400 logical pixels, scale to device pixel ratio
- Dots: 8px radius, team color fill, dark outline
- Health: thin arc above each dot, depleting
- Hit tier visual:
  - glance: small grey particle
  - normal: 3 sparks in attacker direction
  - solid: 5 sparks, brighter
  - crit: 8 sparks + brief outline flash on target
  - landmark: 12 sparks + 400ms slow-mo (sim ticks at 0.25× during) + screen shake + radial burst

## What NOT to build in S1

- Patron mechanics, divine actions, XP — S2
- Affinity, relationships, buddies — S3
- Hidden state, confessions — S4
- Chronicle, fast-sim, drama digest — S5
- Drama director — S6
- Items, loot piñata — S7
- MBTI, love types — S8
- Family — S9
- Social events — S10
- Cliques — S11
- Cast UI, season focus, write-off — S12
- Tab bar (single view in S1) — S2 will introduce it
- localStorage actual reads/writes — S2

Resist scope creep. One layer per session.

## Closing the session

When S1 lands:
1. Verify dev server runs and battle is watchable on phone
2. Commit with a clean message
3. Write `docs/DIGEST_S1.md` with:
   - Total lines per file
   - What landed (mapped to spec sections)
   - Constraints honored (no `?.[]`, hooks before returns, brace balance)
   - Open TODOs and known issues
   - Any deviations from this prompt and why
4. Write `docs/SESSION_S2_OPENING_PROMPT.md` with the next session's scope

## Acceptance criteria

- [ ] `npm run dev` works, opens in mobile browser
- [ ] BATTLE button starts a fight
- [ ] Dots move, attack, take damage, die
- [ ] Hit tiers visibly differ — landmark hits feel like the slot machine landed
- [ ] Win-prob bar swings during battle
- [ ] Battle ends with a winner banner
- [ ] Speed toggle works (1× / 2× / 4×)
- [ ] No `?.[]` in codebase, hooks ordering correct
- [ ] DIGEST_S1.md written

If any acceptance criterion is unclear, ask Seth before assuming. Otherwise: build.
