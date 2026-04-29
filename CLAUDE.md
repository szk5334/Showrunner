# CLAUDE.md

Project conventions and constraints for Showrunner. Claude Code reads this automatically at session start. Honor these without being asked.

---

## Project

**Showrunner** — A casting-director soap-opera engine where the player curates a cast of dots and a Drama Director generates intertwining arcs across battles, socials, and generations. Combat is content; relationships are the show.

Single-developer project (Seth). Solo build via Claude Code on the web from phone. Sonnet implements; Opus designs in separate claude.ai chat sessions.

**Authoritative design source:** `docs/SPEC_SHOWRUNNER_v0.2.md`

---

## Stack

- **Vite + React (JSX)** — not TypeScript for v1
- **Mobile-first** — phone screen, portrait, single column. Desktop is incidental.
- **localStorage** for persistence (no backend, no server)
- **No external state libs** — React useState/useReducer only
- **Canvas 2D** for the battlefield, React for everything else
- **No animation libraries** — direct rAF + canvas

---

## Hard rules (carried over from prior projects, do not violate)

1. **No `?.[]` syntax** — caused crashes in StableNet. Use `obj && obj.foo` or guard before access.
2. **All React hooks must come before any early returns.** A hook-after-early-return ordering caused a DROP GATE crash. Hard rule.
3. **Prefer `function(){}` callbacks** in event handlers and state updaters over arrow functions where readability is comparable.
4. **No localStorage/sessionStorage in artifact-targeted code paths** — for the Vite build it's fine, but if any component will ever ship as a Claude.ai artifact preview, use in-memory only.
5. **Brace/paren/bracket balance check** after any structural edit before considering a change complete.
6. **Save migration when fixing data shape bugs** — never silently change the schema. Bump a `saveVersion` field, write a migration in `engine/persistence.js`.

## Soft conventions

- Files target 300-800 lines each. Past 800, split.
- Single source of truth per system: combat in `engine/combat.js`, director in `engine/director.js`, etc. Don't duplicate logic in UI components.
- UI components are dumb-ish: read state via props, dispatch actions via callbacks. Game logic lives in `engine/`.
- Constants in `engine/constants.js`. Tunable knobs grouped together with comments.
- No inline magic numbers in the director. Every tunable in the constants block.

---

## File structure target

```
showrunner/
├── CLAUDE.md                    ← this file
├── README.md
├── docs/
│   ├── SPEC_SHOWRUNNER_v0.2.md  ← design source of truth
│   ├── SESSION_S1_OPENING_PROMPT.md
│   ├── DIGEST_S1.md             ← created at end of S1
│   ├── DIGEST_S2.md             ← created at end of S2
│   └── ...
├── package.json
├── vite.config.js
├── index.html
├── src/
│   ├── main.jsx
│   ├── App.jsx
│   ├── engine/
│   │   ├── combat.js
│   │   ├── ai.js
│   │   ├── dots.js
│   │   ├── relationships.js     ← S3+
│   │   ├── hidden.js            ← S4+
│   │   ├── chronicle.js         ← S5+
│   │   ├── director.js          ← S6+
│   │   ├── items.js             ← S7+
│   │   ├── mbti.js              ← S8+
│   │   ├── persistence.js
│   │   └── constants.js
│   ├── data/
│   │   ├── names.js
│   │   ├── loves.js             ← S8+
│   │   └── templates.js         ← S5+
│   └── ui/
│       ├── BattleView.jsx
│       ├── ChronicleView.jsx    ← S5+
│       ├── CastView.jsx         ← S9+ (showrunner toolbox)
│       ├── Inspector.jsx
│       └── TabBar.jsx
└── public/
```

This is the *target*. Earlier sessions only have files for layers shipped so far. Don't pre-create empty modules.

---

## Session workflow

Each session lands one complete dopamine layer (per spec §58). Don't ship infrastructure-only sessions. The pattern that's worked across StableNet, Bloodlines, Dot War:

1. **Read** the latest `DIGEST_*.md` and the spec section for the session's target
2. **Scan** existing code that the new layer touches
3. **Edit surgically** — single-purpose changes, brace/paren balance preserved
4. **Test** by running the dev server and watching live
5. **Write the digest** at session end: line maps, system docs, what landed, what's deferred
6. **Update spec** if any decisions changed during implementation

A digest looks like:

```
DIGEST_S1.md
- Lines: 1,247 across 6 files
- Landed: combat, hit tiers, basic AI, win-prob bar, single battle button
- Deferred to S2: patron mechanics, divine actions
- Constraints honored: no ?.[], hooks before returns
- Files: src/engine/{combat,ai,dots,constants}.js, src/ui/BattleView.jsx, src/App.jsx
- Open issues: AI sometimes pathfinds into walls (see ai.js:142 TODO)
- Next session opening prompt: docs/SESSION_S2_OPENING_PROMPT.md
```

---

## Things that are NOT goals

- TypeScript (defer; v2 maybe)
- Tests (manual playtest is the test for v1)
- Performance optimization beyond what hot paths demand
- Backend / server / multiplayer
- Monetization
- Accessibility audits in v1 (good practice, but not blocking)
- Code coverage
- Storybook / component library
- 60fps on every device — target 30fps stable on a 2-year-old phone

---

## When the model is uncertain

- **Design questions** → check spec first; if not answered, defer to Seth (don't invent)
- **Implementation questions** → make the smallest reasonable choice, note in digest
- **Scope creep** → resist. One layer per session. If a "while you're in there" change is tempting, write it as a TODO in the digest.
- **Conflicts between this file and the spec** → spec wins for design, this file wins for conventions

---

## Communication style

Seth prefers:
- Short imperative requests, immediate correction of wrong assumptions
- Direct confirmation when bugs are resolved
- Tap-to-select over typed answers when offering options
- Big redesigns deferred to dedicated sessions to avoid scope creep
- Willingness to paste game state JSON for diagnosis

Match this rhythm. No long preamble, no over-explaining, no "I'll be happy to help!" filler.
