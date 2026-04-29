# THE SHOWRUNNER — Unified Design Specification

> A casting-director soap-opera engine where the player curates a cast and a Drama Director generates intertwining arcs across battles, socials, and generations. Combat is content; relationships are the show.

**Working title placeholder.** This document supersedes the Dot War Unified Spec for the new engine. Dot War spec retained for reference on combat substrate.

**Version:** v0.2 — Claude Code multi-file architecture
**Format target:** Vite + React multi-file project, mobile-first, built via Claude Code on the web (phone-accessible)
**v0.1 → v0.2 changes:** single-file constraint removed; multi-file architecture promoted to first-class; build sequence restored to full 12-session arc with no compression cuts; file structure added as Part XV.

---

## Table of Contents

**Part I — Vision**
1. Thesis & player experience
2. The showrunner reframe
3. Engagement architecture by timescale
4. Non-goals

**Part II — The Cast & Showrunner Layer**
5. Cast slots & XP unlocks
6. Casting events
7. Write-off mechanics
8. Cast history & comeback debt
9. Showrunner toolbox
10. Season system

**Part III — The Drama Director**
11. The 5-phase pipeline
12. Audit dimensions
13. Intervention catalog
14. ROI & budget
15. Cast utilization subsystem
16. Tunable knobs
17. What the director does NOT do

**Part IV — Personality (MBTI)**
18. The 16 types
19. MBTI → behavior gene defaults
20. MBTI → love propensity matrix
21. Pairing tendencies

**Part V — Relationships (8 Loves)**
22. Relationship object structure
23. The 8 love types: healthy & shadow
24. Asymmetric loves
25. Love transformations & arc taxonomy
26. Hidden vs public state

**Part VI — Social Structures**
27. Pair / Triangle / Inner Circle / House / Faction / Dynasty
28. Position within structure
29. Structure-aware drama

**Part VII — Events**
30. Battle events
31. Social events
32. Drama spike events
33. Casting events
34. Lifetime events

**Part VIII — Discord & Accord**
35. Discord catalog
36. Accord catalog
37. Magnitude tables
38. Witness propagation

**Part IX — Combat (Content Layer)**
39. Inherited combat substrate (from Dot War)
40. Behavior modules (compressed to 8)
41. Roles (compressed to 4)
42. Hit tiers slot machine
43. Conversion mechanics
44. Items & loot piñata

**Part X — Chronicle**
45. Chronicle as home screen
46. Pull-to-refresh fast-sim
47. Cliffhanger generation
48. Daily digest & notifications
49. Chronicle entry templates

**Part XI — Hidden State**
50. True vs public layer (Layer-1 reveal model)
51. Reveal triggers
52. Hooks for Layer-2 (future POV restriction)

**Part XII — UI**
53. Tab structure & navigation
54. Bottom-sheet inspector
55. Battle view
56. Cast management view
57. Relationship inspector

**Part XIII — Build & Persistence**
58. Build sequence (12 sessions)
59. Persistence
60. Save export/import

**Part XIV — Decisions**
61. Locked decisions
62. Deferred questions
63. Open questions

**Part XV — File Architecture**
64. Repo layout
65. Module boundaries
66. Inter-module rules
67. Build & run

---

# PART I — VISION

## §1 Thesis

The player is a showrunner. They curate a cast of dots. The Drama Director, an algorithmic writers' room, generates intertwining arcs across battles, socials, and generations. Combat is the medium through which drama plays out, but the relationships are the show. The chronicle is the home screen — the player opens the app to read what happened, occasionally drops in to watch a scene live.

**Core loop:** open app → read chronicle → see hooks → take an action (cast, watch battle, set focus, intervene) → action produces chronicle → close app. ADHD-targeted dopamine on every timescale, with the curator-spectator hybrid as the unique pull.

## §2 The Showrunner Reframe

Inverts the toy model. Where Dot War positioned the player as god-watching-ants with patron mechanics, this engine positions the player as showrunner-running-a-writers-room. Curatorial dopamine + spectator dopamine compounded.

Player's primary actions:
- **Cast** dots into the show
- **Set season focus** (romance / rivalry / redemption / chaos)
- **Pin or block arcs**
- **Soft-ship** pairs
- **Force events** (1-2 per season, big-ticket)
- **Watch** live battles or fast-sim
- **Write off** characters

The Director handles everything else.

## §3 Engagement Architecture

| Timescale | Hook |
|-----------|------|
| Frame (16ms) | Hit tiers slot machine, particles, color trails |
| Second | Action commitment hesitation, confession bubbles, transformation moments |
| 10-30s | Win-prob swing, drama spikes, witnessed reveals |
| Battle (1-3min) | Chronicle line, cliffhanger, items |
| Session | Pull-to-refresh fast-sim, drama queue, binge-reveal |
| Showrunner | Cast curation, season focus, comeback orchestration |
| Generation | Dynasty arcs, multi-season storylines, transformation chains |

## §4 Non-Goals

- Pure simulation without player curation (defeats the showrunner premise)
- Player-piloted combat (combat is content, not gameplay)
- Multiplayer / online
- Monetization
- Behavior gene editor
- 1,440-dot scale (cap at 64-128 for v1)
- Pannable battlefield (fit-to-screen single view)
- Custom team builder UI (cast IS the custom team)
- TypeScript (defer to v2)
- Backend or server (localStorage only)

---

# PART II — THE CAST & SHOWRUNNER LAYER

## §5 Cast Slots & XP

| Slots | XP Unlock |
|-------|-----------|
| 5 | Default |
| 10 | 2,500 XP |
| 15 | 10,000 XP |
| 25 | 30,000 XP |

Above 25 not planned for v1. More cast = more drama density to manage; soft cap is also dramatic.

## §6 Casting Events

Adding a dot to cast:
- `cast_history.joined: currentBattle`
- `casting_call_battles: 3` (priority subject for next 3 battles)
- Chronicle event: "Helia (ε) joins the cast." Light fanfare.
- Existing relationships involving this dot surface in casting view

## §7 Write-Off Mechanics

Three flavors:
- **Quiet exit** — `drama_magnet × 0.3` for 5 battles; easy comeback
- **Dramatic exit** — chronicle send-off scene; 8-battle cooldown; landmark return
- **Permanent (true death)** — closed; comeback only via descendant

## §8 Cast History & Comeback Debt

Per dot: `cast_history: [{joined, left, reason, arc, battles_active}]`. Director scans on every drama-seeding pass; weights former cast for re-entry.

Comeback debt: every 5 battles, dormant cast >8 battles is candidate. Director picks strongest hook (mid-arc when they left, surviving rivals/lovers, etc.).

## §9 Showrunner Toolbox

| Action | Effect |
|--------|--------|
| Set season focus | Multiplies director payoff scores by category |
| Pin arc | Director cannot suppress this thread |
| Block arc | Suppress for 5 battles |
| Soft-ship pair | +0.05 affinity nudge per battle, director compatibility-checks |
| Force event | 1-2/season; triggers immediate confession/reconciliation/comeback |

## §10 Season System

30 battles per season. Cast snapshot. End-of-season recap weighted to current cast. Player chooses next season focus on transition. Pin/unpin arcs across seasons.

---

# PART III — THE DRAMA DIRECTOR

The director runs once per battle pre-roll (and once per social pre-roll), takes ~5-15ms, and outputs a **dramatic plan** that biases the upcoming engagement. It's not in-the-loop — combat AI doesn't query the director per tick. It pre-stages the battle to be dramatic, then watches what emerges.

## §11 The 5-Phase Pipeline

```
1. AUDIT       — score current world state across drama dimensions
2. DEFICIT     — identify which dimensions are below quota
3. CANDIDATES  — generate possible interventions ranked by ROI
4. SELECT      — pick 1-3 interventions weighted by season focus
5. STAGE       — apply biases, plant seeds, schedule reveals
```

## §12 Audit Dimensions

Scan world state, compute scores across 8 dimensions:

| Dimension | Healthy band | Why it matters |
|-----------|--------------|----------------|
| Active triangles | 2-5 | Shape with built-in tension |
| Open grudges (mutual < -0.4) | 3-8 | Future combat motivation |
| Pending reveals (hidden state ≥ threshold) | 2-4 | Loaded chambers |
| Cliffhanger arcs | 2-3 | Return-engagement hooks |
| In-progress transformations | 1-2 | Mid-arc love-type changes |
| Cast utilization | ≥80% appeared in last 5 | Player-curated must matter |
| Comeback debt | <3 long-dormant cast | Forgotten dots accumulate |
| Drama freshness | Last 5 chronicles distinct | No repeating beats |

Each dimension produces a score and a deficit flag. Cheap to compute — operates on metadata, not simulation.

### §12.1 Deficit Selection

```
deficits = [d for d in dimensions if d.below_band]
deficits.sort(key=severity, reverse=True)
```

If no deficits: director is in **maintenance mode** — light bias toward existing arcs, no new seeds. The show is healthy.

If multiple deficits: top 2-3 get addressed. Don't over-correct in a single battle; drama compounds across battles.

## §13 Intervention Catalog

For each deficit, generate intervention candidates. Each candidate is a structured object:

```js
{
  type: 'seed_triangle' | 'force_meeting' | 'promote_reveal' |
        'orchestrate_comeback' | 'plant_witness' | 'trigger_transformation' |
        'inject_rival' | 'compatibility_test' | 'cliffhanger_setup',
  participants: [dotIds],
  precondition_score: 0-1,    // how plausible
  payoff_score: 0-1,           // expected drama
  cast_weight: 0-1,            // % of participants in cast
  novelty_score: 0-1,          // freshness vs recent chronicles
  cost: 1-3,                   // budget consumed
  preview: "Akros learns Bora's betrayal mid-battle"
}
```

### §13.1 Intervention Types

**seed_triangle**: pick a high-affinity pair, find compatible third per MBTI matrix, give them `secret_crush` flag toward one of the pair, increase deploy proximity, add to drama-watch list.

**force_meeting**: temporarily boost `w_engage_nearest` between two specific dots, deploy them within 200px, ensure neither has obvious-flee path early.

**promote_reveal**: take a hidden flag past threshold, mark `imminent_reveal: true` with trigger conditions (proximity + witness + drama-spike-eligible moment).

**orchestrate_comeback**: pull a dormant cast member into starting roster, give them inflated drama-magnet for this battle, plant a hook (their old rival is present, their secret target appears, etc.).

**plant_witness**: ensure a specific third dot is positioned to witness a likely event — Telos must be nearby when Bora and Akros engage. Director places him in deploy slot.

**trigger_transformation**: a relationship is past threshold for transformation (eros→mania, ludus→eros). Director increases trigger event probability by stacking conditions (proximity + low HP + witness present).

**inject_rival**: low-grudge team gets a fabricated incident — micro-event in pre-battle ("Bora claims Akros stole her glory at B14"). Adds -0.3 mutual, witnessed by 1-2 others.

**compatibility_test**: pair two dots whose MBTI predicts strong reaction (positive or negative), force proximity, see what emerges.

**cliffhanger_setup**: identify a state that's about to resolve, *prevent it from fully resolving*. The convert-or-die roll gets nudged to convert (relationship continues). The kill blow gets interrupted by a third party.

## §14 ROI & Budget

**ROI = payoff × (1 + cast_weight × 2) × novelty / cost.** Cast members count triple — they're player-curated, so anything involving them is high-value.

Budget per battle: **3 director points.** Most interventions cost 1, big ones cost 2-3.

```
selected = []
budget = 3
candidates.sort(by ROI)
for c in candidates:
  if c.cost <= budget AND not_conflicts(c, selected):
    selected.append(c)
    budget -= c.cost
  if budget <= 0: break
```

Conflict check: don't seed a triangle and break the same triangle in one battle. Don't force two reveals about the same dot. Keep it readable.

Season focus modifies ROI scores: "more romance" doubles `seed_triangle` and `trigger_transformation:eros` payoffs. "More rivalry" doubles `inject_rival` and `promote_reveal:grudge`.

## §15 Cast Utilization Subsystem

This deserves its own pass because it's the player-facing core:

```
cast_health = Σ(cast member appeared in last 5 battles) / cast.size
```

If `cast_health < 0.8`: deficit fires. Director must include 1+ cast member in stage operations.

**Casting events**: when a dot is added to cast, they get `casting_call_battles: 3` — the next 3 battles, director treats them as priority subject. Plants events around them. This is what makes "I just cast Helia" feel immediate.

**Comeback debt:** every 5 battles, scan for cast members dormant >8 battles. If 2+ exist, fire `comeback_debt` deficit. Director picks the one with strongest hook (mid-arc when they left, surviving rivals/lovers, etc.).

## §16 Tunable Knobs

```js
DIRECTOR_BUDGET_PER_BATTLE = 3       // higher = more chaos
CAST_WEIGHT_MULTIPLIER = 2           // how much cast > non-cast
NOVELTY_DECAY_BATTLES = 5            // recency window
MAINTENANCE_MODE_THRESHOLD = 0       // deficits to enter active mode
COMEBACK_COOLDOWN_DRAMATIC = 8
SEASON_FOCUS_MULTIPLIER = 2.0
DEFICIT_SEVERITY_WEIGHT = {
  triangles: 1.0,
  grudges: 1.2,
  reveals: 1.3,
  cliffhangers: 1.4,
  transformations: 1.0,
  cast_utilization: 1.5,
  comeback_debt: 1.1,
  freshness: 0.8
}
```

These are the dials you'll tune most during playtest. Keep them in one config block.

## §17 What the Director Does NOT Do

- Doesn't pilot dots in combat. AI runs on its own genes.
- Doesn't override player decisions. Player force-events stack on top.
- Doesn't fabricate impossible events. Every intervention has plausibility check (MBTI compatible, proximity feasible, history non-contradictory).
- Doesn't run mid-battle. Mid-battle drama spikes use pre-staged conditions, not director re-runs.
- Doesn't act on dots outside cast unless deficit forces it. Off-cast dots run their own lives quietly.

---

# PART IV — PERSONALITY (MBTI)

## §18 The 16 Types

Each dot rolls a 4-letter type at birth. Inheritable: 30% pick from one parent, 30% other parent, 40% recombine letter-by-letter with 5% mutation per letter.

## §19 MBTI → Behavior Defaults

| Axis | Behavior bias |
|------|---------------|
| E | +cluster_with_allies, +engage_nearest |
| I | +avoid_cluster, +kite_at_range |
| S | +kite_at_range, +pickup_item (present-focus) |
| N | +ambush_strike, +hunt_grudge (pattern-read) |
| T | +hunt_strongest |
| F | +protect_buddy, +avenge_buddy |
| J | +hold_position, +stick_to_leader |
| P | wider gene variance (improvisation) |

## §20 MBTI → Love Propensity

Per-type love propensity (which loves they give easily, which they receive well):

| Type | Profile |
|------|---------|
| **INFP** | Romantic idealist. Eros (idealized), agape, mania risk. Bad at ludus. |
| **INFJ** | Quiet caretaker. Agape, philia, deep storge. Eros rare and reverent. |
| **INTJ** | Strategic loyalist. Pragma, philautia. Eros rare, intense when it lands. |
| **INTP** | Distant thinker. Philautia, philia with select few. Pragma slow, eros rare. |
| **ISFJ** | Devoted helper. Storge, agape, sturdy eros. |
| **ISFP** | Quiet romantic. Eros within close circle, philia loyal. Ludus uncomfortable. |
| **ISTJ** | Dutiful anchor. Pragma, storge. Eros guarded slow burn. |
| **ISTP** | Solitary operator. Philautia. Pragma functional. Eros rare and physical. |
| **ENFP** | Charismatic connector. Eros + ludus + philia simultaneously. Mania risk. |
| **ENFJ** | The mentor. Agape, philia, pragma. Eros idealistic. |
| **ENTJ** | Commanding partner. Pragma, philautia. Eros intense, structured. |
| **ENTP** | Provocateur. Ludus, broad philia, intellectual eros that changes. |
| **ESFJ** | Social glue. Philia, storge, community-agape. Pragma earnest. |
| **ESFP** | Performer. Ludus, frequent bright eros. Pragma elusive. Mania flares. |
| **ESTJ** | Organizer. Pragma, provider-storge. Philia loyal. Eros functional. |
| **ESTP** | Adventurer. Ludus, fast physical eros. Mania possible after loss. |

## §21 Pairing Tendencies

```
NF + NF        → eros / agape (idealized)
ST + ST        → pragma (stable)
NT + NF        → eros struggling (mania risk)
SF + SF        → storge / philia (easy)
3-letter match → philia readily
4-letter match → twin-flame OR echo-chamber (50/50)
opposing 4     → antagonism OR magnetic eros (rare, intense)
```

These are the director's compatibility heuristics. ENFPs cause drama wherever they go. ISTPs forming philia is a meaningful event. INTJ-ESFP eros is a classic disaster pairing.

**Predictability + variance = anticipation = dopamine.**

---

# PART V — RELATIONSHIPS (8 LOVES)

## §22 Relationship Object

```js
{
  type: 'eros'|'philia'|'agape'|'storge'|'pragma'|'ludus'|'philautia'|'mania',
  intensity: 0..1,
  health: -1..1,
  publicType: same enum,           // what others perceive
  publicIntensity: 0..1,
  history: [{type, transitionTrigger, atBattle}],
  events: [last 5],
  firstMet: {battle, t}
}
```

A relationship isn't `affinity: 0.7` — it's typed, intensity-weighted, asymmetric, and history-bearing. Same number, totally different stories.

## §23 The 8 Loves

| Love | Healthy | Shadow |
|------|---------|--------|
| **Eros** | Passionate fire | Obsession |
| **Philia** | Loyal friendship | Codependency |
| **Agape** | Selfless devotion | Martyrdom |
| **Storge** | Familial warmth | Smothering / duty without feeling |
| **Pragma** | Committed partnership | Stale arrangement |
| **Ludus** | Playful flirtation | Leading-on / heartbreak |
| **Philautia** | Self-respect | Narcissism |
| **Mania** | (always unhealthy) | Possessive obsession |

## §24 Asymmetric Loves

Two dots can have different love types FOR EACH OTHER. Akros feels ludus toward Bora (just having fun). Bora feels eros toward Akros (devoted). Asymmetry is the engine. The director prioritizes asymmetric pairs for drama because they're pre-loaded with payoff.

## §25 Love Transformations

Transformations between types = the major dramatic arcs. Each needs a trigger event + intensity threshold + MBTI plausibility check. Each is a chronicle peak.

| Transformation | Trigger conditions |
|----------------|---------------------|
| **Ludus → Eros** | high intensity sustained 3+ battles + witnessed proximity moment |
| **Eros → Pragma** | shared survival of crisis + 5+ battles |
| **Eros → Mania** | rejection or beloved death + low philautia |
| **Philia → Eros** | shared trauma + MBTI compatibility check |
| **Storge → Pragma** | co-leadership of structure |
| **Agape → Mania** | martyrdom unrecognized + low philautia |
| **Pragma → Philautia** | identity crisis (loss of beloved, faction shift) |
| **Mania → exit** | violent resolution required (death, conversion, exile) |

## §26 Hidden vs Public

`type` + `intensity` are true. `publicType` + `publicIntensity` are what witnessing dots and chronicle perceive. Divergence drives drama. Reveal triggers in §51.

---

# PART VI — SOCIAL STRUCTURES

## §27 Structures

| Structure | Size | Definition |
|-----------|------|------------|
| **Pair** | 2 | Any love |
| **Triangle** | 3 | Geometric (love-triangle, mentor-w/-disciples, etc.) |
| **Inner Circle** | 3-6 | Mutual philia, internal politics |
| **House** | 5-15 | Family + spouses + adopted close |
| **Faction** | 8-30 | Ideological grouping |
| **Dynasty** | unlimited | Multi-generational line |

## §28 Position

Per dot per structure: peripheral / member / core / leader. Position weights director's event significance.

## §29 Structure-Aware Drama

House Head's confession > peripheral's. Faction-level rupture cascades to all members. Dynasty events span generations.

---

# PART VII — EVENTS

## §30 Battle Events

Standard / Skirmish / Duel (grudge) / Royale / Hunt (cast member targeted)

## §31 Social Events

Mixer / Gathering (clique-focused) / Memorial / Vow / Confrontation / Reunion

## §32 Drama Spike Events (mid-anything)

Confession / Betrayal / Recognition (transformation) / Reveal / Comeback

## §33 Casting Events (player-driven)

Casting call / Renewal / Write-off / Recall / Recast

## §34 Lifetime Events

Birth / True death / Conversion / Title / Generation milestone

---

# PART VIII — DISCORD & ACCORD

## §35 Discord Catalog

Each entry has a love-type-specific impact and a follow-up flag for the director:

- **Betrayal witnessed** — hidden grudge → public. Hammers eros/philia/agape; pragma weathers; mania feeds.
- **Boundary mismatch** — A pursues eros, B offers philia. Pain in A, suffocation in B. Mania risk.
- **Triangle activation** — third party introduces alternate love. Resolution triggers transformation.
- **Loss of beloved** — high-intensity target dies/converts. Grief; mania risk if eros was high.
- **Public failure** — humiliation in front of cast. Philautia damage. Reputational shift.
- **Inherited rejection** — feuding lines' children forced together. Romeo-Juliet potential.
- **Stagnation** — pragma without renewal drifts; ludus-types wander.
- **Asymmetric reveal** — hidden eros revealed; target only feels philia. Devastates secret-bearer.
- **Ideological rupture** — faction conflicts split friends. Tests philia.
- **Resource competition** — two dots want same kill / item / position. Rivalry feed.

## §36 Accord Catalog

- **Sacrifice witnessed** — A takes a hit for B. Strongest accord. Transforms philia → agape, eros → pragma.
- **Confession accepted** — hidden → manifest, reciprocated. Major chronicle moment.
- **Reconciliation** — estranged find peace via shared trauma or mediator.
- **Recognition of debt** — A acknowledges what B did. Pragma-feeder.
- **Shared trauma survived** — universal philia builder, MBTI-agnostic.
- **Mentorship begun** — asymmetric storge, slow build.
- **Vow taken** — pragma formalized.
- **Forgiveness offered** — grudge consciously released. Rare, chronicle-worthy.
- **Self-recognition** — dot reaches a philautia milestone. Changes how they relate going forward.
- **Mutual return** — written-off cast member reunites with old friend. Comeback accord.

## §37 Magnitude Tables

Per discord/accord × love-type → affinity Δ + transformation likelihood. Scaled by intensity, witnessed status, MBTI compatibility. (Detailed tables to be specced before S3.)

## §38 Witness Propagation

Within 80px of an event: third party gains -0.05 to -0.20 affinity to perpetrator (scaled by their existing affinity to victim). Witness count amplifies public-vs-true divergence.

---

# PART IX — COMBAT (CONTENT LAYER)

## §39 Inherited Combat Substrate

From Dot War: damage formula, conversion mechanics, hit tier slot machine, particle/bubble visual layer, divine intervention (compressed to 3 actions: bless / curse / heal). All retained.

## §40 Behavior Modules (8)

`engage_nearest`, `flee_threat`, `retreat_low_hp`, `hunt_healer`, `hunt_grudge`, `protect_buddy`, `avenge_buddy`, `pickup_item`. Decision aggregation per Dot War §12 (vector-sum movement + winner-take-all action with hysteresis).

## §41 Roles (4)

Frontline, Ranged, Healer, Skirmisher.

## §42 Hit Tiers Slot Machine

Glance 15% / Normal 70% / Solid 12% / Crit 2.5% / Landmark 0.5% with multipliers 0.5/1.0/1.4/1.8/2.5. Slow-mo on landmark per Dot War §10.3. **This is the frame-level dopamine — do not compromise.**

## §43 Conversion

Per Dot War §11. Conversion conversation when buddy alive nearby — now uses love-type for dialogue tone (eros buddy: "stay with me"; philia buddy: "we need you"; pragma buddy: "the work isn't done").

## §44 Items & Loot Piñata

Compressed inventory: T1 stat tokens + 6 hand-picked T3/T4 items:
- Champion's Wreath (+5% all stats)
- Phoenix Heart (50% revive on death, one-time)
- Soul of [team] (signature behavior module)
- Heart of a Hunter (+0.6 hunt_commanders)
- Avenger's Token (+0.7 avenge_buddy)
- Lineage Seal ("Patriarch"; descendants +5% all stats)

T2 cut. Piñata at 6+ items per Dot War §39.

---

# PART X — CHRONICLE

## §45 Chronicle as Home

App opens to chronicle. Battle button is one of several actions from there. Pull-to-refresh = fast-sim 1-3 events. Pinned ★ entries.

## §46 Pull-to-Refresh Fast-Sim

Drag down → "simming…" → director runs N battles in <2s, returns 3-5 chronicle entries. Always produces something. Variable reward — occasionally a 🔥 reveal.

## §47 Cliffhanger Generation

Every chronicle line ends with one of:
- **Open question** — "Akros lived but Bora's grudge is now public."
- **Dangling reveal** — "Telos saw something he wasn't meant to."
- **Asymmetric tease** — "She still doesn't know what he feels."

Director enforces ≥2 active cliffhangers across last 5 entries.

## §48 Notifications

Local notifications scheduled on app close: backgrounded >2h triggers "Drama brewing — Bora and Telos haven't spoken in 6 battles." No server, just `setTimeout` on close. Tap → opens straight to that thread.

## §49 Chronicle Entry Templates

Per event type, parameterized templates. MBTI-flavored phrasing options. Love-type-aware adjective sets. Director picks template + fills slots. (Catalog to be specced before S5.)

---

# PART XI — HIDDEN STATE

## §50 True vs Public Layer (Layer-1)

True relationship state hidden until events surface it. Player sees `publicType` / `publicIntensity` in chronicle and inspector unless reveal has fired.

## §51 Reveal Triggers

Hidden flag promotes to public when:
- Witnessed proximity event past intensity threshold
- Drama spike (confession, betrayal-witnessed, etc.) fires
- Director's `promote_reveal` intervention stages it
- Threshold-crossing transformation occurs

## §52 Layer-2 Hooks (Future)

Hidden state has `known_by: Set<dotId>` field, currently unused (everyone "knows" public state in Layer-1). For Layer-2 (POV restriction): player only sees state where their patroned dots are in `known_by`. Implementation deferred.

---

# PART XII — UI

## §53 Tab Structure

Bottom tab bar, 4 tabs:
- **Chronicle** (home)
- **Battle**
- **Cast**
- **Relationships**

Tab switch is the primary gesture, not back button.

## §54 Bottom-Sheet Inspector

Pull up from any dot. Half-screen, dismissable. Don't push to a new view — keeps continuity.

## §55 Battle View

Portrait. Single-column:

```
┌─────────────────────────┐
│ HUD: ★patron HP/kills   │  ~64px
│ XP: 1,247 ▶ ✦✦✦ charges │
├─────────────────────────┤
│                         │
│   battlefield 360×400   │  fit
│   (no pan, no zoom)     │
│                         │
├─────────────────────────┤
│ [BLESS] [CURSE] [HEAL]  │  ~80px
│ [BATTLE] [CHRONICLE]    │
└─────────────────────────┘
```

Battles 60-90 seconds. Two-finger tap toggles 1×/2×/4× speed, default 2×.

## §56 Cast Management View

Slots filled / empty. Tap to add (filter by team / role / love-status / drama-level). Tap to write off (3 flavors). Cast history visible per slot.

## §57 Relationship Inspector

Per relationship: love type, intensity, public-vs-true divergence indicator if revealed, history of transformations, event log (last 5).

---

# PART XIII — BUILD & PERSISTENCE

## §58 Build Sequence

| Session | Adds | Closing dopamine layer |
|---------|------|------------------------|
| **S1** | Combat, hit tiers, win-prob, basic AI | Slot machine |
| **S2** | Patron, divine, XP, chronicle stub | Battle layer |
| **S3** | Affinity ledger, buddy detection, conversion conversation | First soap moment |
| **S4** | Hidden state, confessions, witnesses | Reveal mechanic |
| **S5** | Chronicle home, pull-refresh, drama digest | Session-binge |
| **S6** | Drama director (full pipeline) | Self-sustaining drama |
| **S7** | Items, loot piñata, slow-mo polish | Variable-reward visual |
| **S8** | MBTI substrate, love types | Personality + relationship typology |
| **S9** | Family graph, inheritance | Generational hooks |
| **S10** | Mixer social, social events | Non-combat drama |
| **S11** | Cliques + structures | Position-aware drama |
| **S12** | Showrunner toolbox (cast UI, season focus, force events) | Curatorial layer |

**S6 is the keystone** — engine becomes self-sustaining. **S12 is the layer that makes the player a showrunner.**

After S6 you have a complete addictiveness engine. S7+ deepen it. The honest checkpoint is around S5 — if the loop doesn't have pull by then, something's off.

## §59 Persistence

All persistence via `engine/persistence.js`, single localStorage key `showrunner_save_v1`. Aggregate JSON object:

```js
{
  saveVersion: 1,
  roster: [...],            // 64-128 dots
  relationships: {...},     // keyed by `${dotIdA}-${dotIdB}` (sorted)
  chronicle: [...],         // events + compiled lines, capped to last 500
  cast: {...},              // active cast + cast_history per dot
  director: {...},          // recent interventions, deficit history
  season: {...},            // focus, pinned arcs, blocked arcs
  hidden: {...},            // per-dot hidden flags, reveal_progress
  xp: {...},
  settings: {...}
}
```

**Save migration policy:** never silently change schema. Bump `saveVersion`, add migration function in `persistence.js` keyed on old version. Migration runs on load.

## §60 Save Export/Import

Aggregate `showrunner_save_v1` localStorage value as JSON for portability. Player can back up via copy-to-clipboard, restore via paste-and-load. Export/import UI in settings (S5+).

---

# PART XIV — DECISIONS

## §61 Locked Decisions

1. Showrunner is the player role; cast curation is primary action
2. Chronicle is the home screen
3. Drama Director is pre-roll only, not in-the-loop
4. Director budget = 3 points/battle
5. Cast slots: 5 / 10 / 15 / 25 via XP
6. Three write-off flavors: quiet / dramatic / permanent
7. Cast history tracked permanently for comeback orchestration
8. 16 MBTI types as personality substrate
9. 8 love types with healthy/shadow expressions
10. Asymmetric loves are first-class (different per direction)
11. Love transformations are chronicle peaks
12. Hidden vs public state: Layer-1 (chronicle reveal) for v1
13. Layer-2 (POV restriction) deferred but data shape preserved
14. Witness propagation within 80px
15. Combat substrate inherited from Dot War, compressed
16. 8 behavior modules / 4 roles / 64-128 dots
17. Pull-to-refresh = fast-sim 3-5 events
18. Cliffhanger enforced every chronicle line
19. Local notifications only, no server
20. Vite + React multi-file project, built via Claude Code; mobile-first portrait UI

## §62 Deferred Questions (data shape preserved)

- Layer-2 POV restriction
- Breeding (gene-level inheritance for personality already specced; mechanic deferred)
- Dynasty UI / family tree visualization
- Faction-level events
- Multi-season storylines beyond 1 season
- Wedding / Funeral event types

## §63 Open Questions

- Director intervention preview to player? (transparency vs mystery)
- How visible is MBTI to player? (always / via inspector / never)
- Should season focus be hard cap or soft bias?
- Can player rename dots? (feels right, but forces name field everywhere)
- Inheritance of MBTI: pure parent-pick or recombine letter-by-letter (currently recombine)
- True death rate: 100% on convert-fail or scaled?
- Cast above 25?

---

# PART XV — FILE ARCHITECTURE

## §64 Repo layout

```
showrunner/
├── CLAUDE.md                         project conventions for Claude Code
├── README.md                         human orientation
├── package.json
├── vite.config.js
├── index.html
├── docs/
│   ├── SPEC_SHOWRUNNER_v0.2.md       this file
│   ├── SESSION_S<n>_OPENING_PROMPT.md per-session implementation specs
│   └── DIGEST_S<n>.md                per-session post-mortem and line maps
├── src/
│   ├── main.jsx
│   ├── App.jsx                       root, tab routing
│   ├── engine/
│   │   ├── constants.js              all tunable knobs
│   │   ├── dots.js                   Dot factory, naming, traits
│   │   ├── combat.js                 damage, hit tiers, conversion rolls
│   │   ├── ai.js                     behavior modules, decision aggregation
│   │   ├── sim.js                    battle tick loop
│   │   ├── relationships.js          S3+ love-typed relationship objects
│   │   ├── hidden.js                 S4+ hidden state, reveal triggers
│   │   ├── chronicle.js              S5+ event recording, line composition
│   │   ├── director.js               S6+ 5-phase pipeline
│   │   ├── interventions.js          S6+ intervention type implementations
│   │   ├── items.js                  S7+ item drops, piñata
│   │   ├── mbti.js                   S8+ type axis math, propensity lookup
│   │   ├── family.js                 S9+ family graph, inheritance
│   │   ├── social.js                 S10+ non-combat events
│   │   ├── structures.js             S11+ pairs, triangles, cliques, houses
│   │   ├── season.js                 S12+ season management
│   │   └── persistence.js            localStorage I/O, migrations
│   ├── data/
│   │   ├── names.js                  name pool
│   │   ├── loves.js                  S8+ 8 love types, transformations
│   │   ├── templates.js              S5+ chronicle line templates
│   │   └── mbti-table.js             S8+ 16-type behavior + propensity
│   └── ui/
│       ├── BattleView.jsx
│       ├── ChronicleView.jsx         S5+
│       ├── CastView.jsx              S12+
│       ├── RelationshipsView.jsx     S3+
│       ├── Inspector.jsx             S2+ bottom-sheet
│       ├── TabBar.jsx                S2+ tab routing
│       ├── HUD.jsx
│       └── widgets/
│           ├── WinProbBar.jsx
│           ├── DotSwatch.jsx
│           └── ChronicleEntry.jsx    S5+
└── public/
```

Earlier sessions only have files for layers shipped. Don't pre-create empty modules.

## §65 Module boundaries

- **engine/** — pure game logic, no React imports, no DOM. Testable in isolation. Returns plain data.
- **data/** — static lookup tables. No logic.
- **ui/** — React components. Read state via props, dispatch via callbacks. Game logic stays in engine.
- **persistence.js** — only file in engine/ that reads/writes localStorage.
- **director.js** — never queried mid-tick. Pre-roll only.

## §66 Inter-module rules

- UI never imports from another UI component's internals — only public exports
- Engine modules can import from `constants.js` and `data/` freely
- Circular imports forbidden; if you reach for one, the boundary is wrong
- Cross-cutting concerns (logging, save) live in their own module; don't sprinkle

## §67 Build & run

- **Dev:** `npm run dev` — Vite hot-reload server. Works on phone via network URL.
- **Build:** `npm run build` — outputs to `dist/`.
- **Preview:** `npm run preview` — serves built assets locally.

No CI, no deploys, no tests in v1. Manual playtest is the test.


---

## Constraints (carried over from prior projects, encoded in CLAUDE.md)

- **No `?.[]` syntax** in JS/JSX (caused crashes in StableNet)
- **Hooks must come before any early returns** (hard rule)
- **Mobile-first portrait UI**, single-developer solo build
- **Coded by Sonnet via Claude Code, designed by Opus** in claude.ai chat sessions
- **Multi-file Vite + React** project; no single-file artifact constraint

---

*End of Specification v0.2.*
