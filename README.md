# Showrunner

A casting-director soap-opera engine. The player curates a cast of dots; an algorithmic Drama Director generates intertwining arcs across battles, socials, and generations. Combat is the medium; relationships are the show.

Built with Vite + React, mobile-first, single-developer solo project.

---

## Status

Pre-S1. Repo just initialized. No code yet.

See `docs/SPEC_SHOWRUNNER_v0.2.md` for full design.

## Build sequence

| Session | Layer |
|---------|-------|
| S1 | Combat substrate + hit tiers + basic AI |
| S2 | Patron + divine + XP + chronicle stub |
| S3 | Affinity + buddy detection + conversion convo |
| S4 | Hidden state + confessions + witnesses |
| S5 | Chronicle home + pull-refresh fast-sim |
| S6 | Drama director (full pipeline) ← **keystone, v1.0 ship checkpoint** |
| S7 | Items + loot piñata + slow-mo polish |
| S8 | MBTI substrate + 8 love types |
| S9 | Family graph + inheritance |
| S10 | Mixer social + non-combat events |
| S11 | Cliques + social structures |
| S12 | Showrunner toolbox (cast UI, season focus, force events) |

## Conventions

See `CLAUDE.md` in repo root. Hard rules: no `?.[]`, hooks before returns, save migrations on shape changes.

## Run

After S1 lands:

```
npm install
npm run dev
```

Open the printed local URL on a phone (use the network URL from Vite's output if testing on device, not localhost).

## Workflow

Designs happen in claude.ai chats with Opus. Implementation happens in this repo via Claude Code (Sonnet). Each session ends with a `DIGEST_S<n>.md` and an opening prompt for the next session.
