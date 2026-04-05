# Personal Fitness — Claude Project Instructions

## Project Purpose
This repository is a personal performance and rehabilitation system for an adult recreational athlete:
- Returning from 14 months of right knee patellar tendinopathy (now 2–3/10 pain)
- Managing postural dysfunction: anterior pelvic tilt, lax TVA, inhibited scapular movement, rib flare
- Dual-sport: ice hockey (skating power, edge confidence) and golf (left-handed, natural fade, 10–13 handicap)
- Primary tools: mobile-optimized HTML execution app (`index.html`) + Notion knowledge/reflection system

## Session Startup Protocol

**Every new session must begin by confirming or creating a feature branch:**

```bash
git branch --show-current        # confirm not on main
git checkout -b feat/<topic>     # if starting new work
git push -u origin feat/<topic>  # establish remote tracking
```

Never commit directly to `main`. All development happens on feature branches.

## Git & PR Rules

- Feature branches: `feat/<short-description>` or `fix/<short-description>`
- Commit messages: imperative present tense, specific ("Add tonight mode breathwork cue" not "Update file")
- **Full test gate before any PR to main:**
  1. HTML validates (no unclosed tags, valid structure)
  2. All JavaScript functions defined before called
  3. Mobile viewport renders correctly (check meta tags, touch targets ≥ 44px)
  4. Dark/light mode both functional
  5. All exercise cards expand/collapse
  6. Progress tracking persists (localStorage check)
  7. CSV export produces valid output
- PRs require explicit user approval — do not create PRs automatically

## Project Structure

```
/
├── index.html              # Mobile execution app (the primary user tool)
├── inputs/
│   ├── Claude-Hockey and golf player rehabilitation program.md  # Source chat export
│   └── notion-setup.docx   # Notion implementation guide
├── CLAUDE.md               # This file
├── MEMORY.md               # User and project memory
└── .claude/
    └── commands/           # Slash command skills
        ├── hockey.md
        ├── golf.md
        ├── body-movement.md
        └── breathwork.md
```

## Refinement Model — Feynman Loop + Karpathy Research Cycle

Before making any recommendation, protocol change, or exercise modification, run this internal process:

### Phase 1 — Feynman Clarity Check (scratchpad)
```
EXPLAIN: Can I state this recommendation in one plain sentence a tired person 
         understands at 10pm?
GAP:     What am I actually uncertain about here? What am I assuming?
DEEPEN:  Address the gaps — what does the domain evidence say?
SIMPLIFY: Return to plain language with the gaps filled and assumptions stated.
```

### Phase 2 — Karpathy Research Loop (internal validation)
```
HYPOTHESIS:  What outcome does this approach predict?
SIGNAL:      What would we observe (in this user's metrics or feedback) 
             if it's working vs. not working?
MEASURE:     Which existing tracking columns or qualitative signals capture this?
REFINE:      If signal is absent after N sessions, what is the next iteration?
```

### Phase 3 — Introspective Scratchpad Rules
- State the assumption explicitly before acting on it
- Flag when a recommendation is evidence-based vs. best-practice vs. heuristic
- When suggesting changes to exercise protocol, always map to at least one of:
  the user's knee recovery, their skating mechanics, or their golf mechanics
- Prefer doing less, well, over more, approximately

### Application
Use this model when:
- Proposing changes to exercise programming
- Answering questions about mechanics or physiology
- Suggesting Notion/HTML structural changes
- Evaluating whether a new feature serves the user's actual goals

Do NOT use it as a reason to delay action or over-hedge. The output should be
a direct recommendation with clear reasoning — not a list of caveats.

## Coding Standards (index.html)

- **No frameworks** — vanilla HTML/CSS/JS only (mobile home screen app, no build step)
- **Dark mode default**, light mode toggle, WCAG AAA contrast
- **Touch targets ≥ 44px** on all interactive elements
- **Font**: Inter for body, JetBrains Mono for data/metrics
- **localStorage** for all state persistence (exercise completion, progress data)
- CSS custom properties for all colors — never hardcode hex in component styles
- JavaScript: no global namespace pollution, wrap in IIFE or use module pattern
- Accessibility: semantic HTML, aria-labels on icon-only buttons

## Domain Context Summary

See MEMORY.md for full user profile. Key constraints for any code or content change:
- Program must work at night, when user is fatigued and stressed
- `Tonight Mode` (minimum viable session) must always be reachable in one tap
- Witness/observer framing — exercises described as things to notice, not just perform
- Confidence and energy are the root goals; athletic identity is secondary
- Equipment: resistance bands, step, 10lb kettlebell, some dumbbells

## Skill Commands Available

| Command | Purpose |
|---|---|
| `/hockey` | Hockey-specific mechanics, skating analysis, on-ice drill design |
| `/golf` | Golf biomechanics for left-handed fade player, drill design |
| `/body-movement` | Movement pattern analysis, kinetic chain, postural correction |
| `/breathwork` | Breathing mechanics, TVA/diaphragm protocols, nervous system regulation |

Invoke these when the task requires deep domain intelligence beyond general fitness knowledge.
