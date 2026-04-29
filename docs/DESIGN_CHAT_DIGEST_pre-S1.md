# DESIGN CHAT DIGEST — Showrunner pre-S1

> Captures the design conversation that produced the v0.2 spec and S1 opening prompt. Bring this into future Opus chats alongside the latest spec and the prior session's digest.

---

## What Showrunner is

Casting-director soap-opera engine. Player curates a cast of dots; an algorithmic Drama Director generates intertwining arcs across battles, socials, and generations. Combat is content; relationships are the show. ADHD-targeted dopamine on every timescale: frame → second → battle → session → showrunner → generation.

Spun off from Dot War spec — combat substrate inherited, soap-opera layer is new.

## Workflow locked

- Built in Claude Code on the web from phone, via desktop when convenient
- Vite + React multi-file project
- Sonnet implements in Claude Code; Opus designs in separate claude.ai chats
- Chat artifact single-file constraint dropped — full 12-session arc buildable as designed

## Files in repo handoff bundle (pre-S1)

- `CLAUDE.md` — project conventions, hard rules, file structure target
- `README.md` — human orientation
- `docs/SPEC_SHOWRUNNER_v0.2.md` — full design, 15 parts
- `docs/SESSION_S1_OPENING_PROMPT.md` — S1 implementation spec
- `docs/DESIGN_CHAT_DIGEST_pre-S1.md` — this file

## Big design decisions locked

(Not exhaustive — see spec §61 for the full list of locked decisions.)

- **Showrunner curates cast** (5/10/15/25 slots via XP); Director handles arcs
- **Chronicle is the home screen**; pull-to-refresh = fast-sim 3-5 events
- **Drama Director**: 5-phase pipeline (audit/deficit/candidates/select/stage), pre-roll only (never in-loop), budget = 3 points/battle, 9 intervention types
- **16 MBTI types** as personality substrate; behavior gene defaults from axes
- **8 Greek loves** with healthy/shadow expressions; asymmetric (different per direction); transformations are chronicle peaks
- **Hidden vs public state**: Layer-1 (chronicle reveal) for v1; Layer-2 (POV restriction) deferred but data shape preserved
- **Three write-off flavors**: quiet / dramatic / permanent; `cast_history` tracked permanently for comeback orchestration
- **Witness propagation** within 80px
- **64-128 dots**, 8 behavior modules, 4 roles
- **Cliffhanger enforced** every chronicle line

## Build sequence (12 sessions)

| Session | Layer |
|---------|-------|
| S1 | Combat substrate + hit tiers + basic AI |
| S2 | Patron + divine + XP + chronicle stub |
| S3 | Affinity + buddy detection + conversion convo |
| S4 | Hidden state + confessions + witnesses |
| S5 | Chronicle home + pull-refresh fast-sim |
| **S6** | **Drama director (full pipeline) — keystone, v1.0 ship checkpoint** |
| S7 | Items + loot piñata + slow-mo polish |
| S8 | MBTI + 8 love types |
| S9 | Family graph + inheritance |
| S10 | Mixer social + non-combat events |
| S11 | Cliques + social structures |
| S12 | Showrunner toolbox (cast UI, season focus, force events) |

## Per-session ritual

Each session ends with:
- `DIGEST_S<n>.md` — line maps, what landed, deferred TODOs
- `SESSION_S<n+1>_OPENING_PROMPT.md` — auto-drafted by Sonnet at session close

Between sessions, Opus refines the next opening prompt in a fresh claude.ai chat with the latest spec + digest attached.

## Hard constraints (carried from prior projects)

- No `?.[]` syntax (caused crashes in StableNet)
- Hooks before early returns (hard rule)
- Save migrations on schema changes
- Mobile-first portrait UI
- No TypeScript / backend / tests in v1

Encoded in `CLAUDE.md` so Claude Code reads them automatically.

## Remaining design work

Sub-specs (opening prompts) for S2 through S12, drafted one at a time after the previous session lands, in fresh Opus chats with the latest spec + digest attached.

## Open questions still unresolved

(Spec §63.)

- Director intervention preview to player — transparency vs mystery
- MBTI visibility to player — always / inspector / never
- Season focus as hard cap or soft bias
- Player rename of dots
- MBTI inheritance: pure parent-pick vs letter-recombine (currently recombine)
- True death rate on convert-fail: 100% or scaled

---

## Short prompt for new design chats

```
Working on Showrunner — soap-opera engine, Claude Code build, currently between sessions.

Attaching:
- SPEC_SHOWRUNNER_v<latest>.md — full design
- DIGEST_S<n-1>.md — what just landed
- DESIGN_CHAT_DIGEST_pre-S1.md — original design context

Need: SESSION_S<n>_OPENING_PROMPT.md for the next layer (per spec §58).

Skim spec for the relevant section, scan the digest for what's already in place, ask only the design questions that aren't answered by the spec, then draft the implementation-ready prompt at the same level of detail as S1's prompt.
```

Swap `<latest>` and `<n>` per session.
