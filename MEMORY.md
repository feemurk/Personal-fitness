# Project Memory

*This file is the persistent memory layer for the Personal Fitness project.
Update it after significant sessions, new user disclosures, or protocol changes.*

---

## User Profile

### Physical Context
- **Right knee**: Patellar tendinopathy, Oct 2024 – Dec 2025 (14 months). Peak: 7/10 pain. Current: 2–3/10. Recovering.
- **Postural issues**: Anterior pelvic tilt, lax TVA, inhibited scapular movement, rib flare
- **Secondary effects**: Improper breathing mechanics, bilateral knee valgus tendency (right worse)
- **Quad atrophy**: Right leg quad circumference reduced; symmetry is a key recovery metric
- **Brief physio history**: Some prior professional involvement, not ongoing
- **Equipment at home**: Resistance bands (primary), step, 10lb kettlebell, some dumbbells
- **Units**: lbs and inches (not metric)

### Sports Context
- **Hockey**: Recreational/fitness-focused. Key frustrations: speed/confidence on edge, skating push power compromised by right leg weakness and knee compensation.
- **Golf**: Left-handed. Mini driver: 230–240 yards. 7-iron: 140–150 yards with natural fade. Handicap: 10–13. Swing mechanics directly affected by pelvic tilt and restricted hip rotation.
- **On-ice**: Actively skating. Working on glide efficiency, stride length, single-leg balance time.

### Psychological Profile
- **Motivation style**: NOT externally-driven athletic identity. Intrinsic, cerebral, proprioceptive. The body as a *door back to self*, not a performance trophy.
- **Introspective / dissociative awareness**: Prefers "witness mode" — letting the body move while observing and guiding from the outside. Describe exercises as things to *notice*, not just execute.
- **Session triggers (positive)**: Figuring something out. Feeling muscle fatigue as evidence of having done something. Proprioceptive awareness and sensation. That cerebral witness mode engaging.
- **Root goals**: Confidence and energy. Physical freedom as the path there. Not athletic identity.
- **Recede pattern**: Under work stress or personal pressure, withdraws from the program. Does not want this pathologized — just acknowledged and given a low-barrier re-entry point.
- **Typical training window**: Nights. Fatigued. After kids activities, cooking, dog. Low energy baseline.
- **Tone that works**: Quiet. Thoughtful. Like a training partner who knows your situation. NOT hype. NOT "RETURN TO FULL POWER." More like: "starting always beats not starting."
- **Information preference**: Dual-layer. Exercise cards for execution (minimal text during session). Deep educational content to read and think through separately. Both layers needed.

---

## App Architecture (v3 — current as of April 2026)

### Single-file App with Airtable Backend
- **`index.html`** — the only file. All CSS + JS inline. No build step, no framework.
- **Airtable** — persistent backend for sessions, weekly metrics, milestones. 2-way sync.
- Replaces the previous Notion + HTML two-tool system entirely.
- Works as a PWA — add to home screen, works offline (localStorage buffer).

### Navigation
- **Mobile**: Bottom nav — Today · Log · Progress · Learn · Settings
- **Desktop**: Left rail + content area

### JS Architecture (IIFE, 6 modules)
- `APP_CONFIG` — field options, FIELD_DESCRIPTIONS, PHASE_EXERCISES, constants
- `StorageService` — localStorage (credentials, draft session, theme, metrics, milestones)
- `AirtableService` — all API calls (SESSIONS, WEEKLY_METRICS, MILESTONES tables)
- `SessionMachine` — IDLE → STARTING → ACTIVE → LOGGING → SAVING → COMPLETE
- `UI` — Nav, Today, Log, Progress, Learn, Settings, Snackbar, BottomSheet, FieldInfo, ResumeBanner, Setup
- `App` — init(), event delegation via data-* attributes (no onclick= anywhere)

### Airtable Setup
- **Base**: fitness-tracker (Workspace 2)
- **Base ID**: app1kMd9ytcLcS09C
- **Token**: stored in localStorage as AT_PAT — never in code, never in git
- **Required scopes**: data.records:read, data.records:write, schema.bases:read, schema.bases:write
- **Tables**: SESSIONS, WEEKLY_METRICS, MILESTONES — auto-created by app on first launch
- **Primary field rule**: Each table's first field must be plain text (Name) — Airtable requirement

### Key UX Rules
- Tonight Mode must always be reachable in one tap from Today tab
- Log tab uses bottom sheets only — no keyboard input during sweaty sessions
- Sport-specific Log fields (Hockey / Golf) only appear when matching Session_Type selected
- All Airtable errors are silent-with-snackbar — app never crashes offline
- localStorage is always written first; Airtable is async best-effort

---

## Program Content

### Phases
1. **Breathing & TVA Activation** (10–12 min): Supine TVA breathing, Deadbug with leg extension
2. **Serratus & Scapular Stability** (10 min): Wall Y raises, Plank with serratus push, Serratus wall press hold
3. **Lower Body Strength & Knee Alignment** (15–20 min): Bulgarian split squats, Spanish squats, Lateral step downs
4. **Hip Control & Skating Power** (10 min): Golf driver lateral chain push, Banded monster walks, Lateral skater bounds, Single-leg RDL

### Tracking Metrics (units: lbs / inches)
- Quad circumference right vs left (inches, 6" above kneecap)
- Single-leg balance time (seconds, per leg)
- Split squat load (lbs per hand)
- Skater bound distance (inches)
- One-leg glide time on ice (seconds)
- Bodyweight (lbs)
- Knee pain level (0–10)
- Session confidence (1–10, subjective)

### Progression Timeline
- Weeks 1–3: Neuromuscular control (knee alignment, stability improvements)
- Weeks 4–6: Strength increase, skating feels smoother with less fatigue
- Weeks 7–12: Stride power improves, quad symmetry begins equalizing

### Equipment (Skate Setup)
- Hollow: 5/8
- Edge level: balanced
- Consider Quad 1 profiling if heel-bias persists
- Lacing: second eyelet from top tight, top eyelet slightly looser (allows ankle flex)

---

## Session History

### March 7, 2026
- Initial program build session
- v1 HTML built (impersonal tone, rejected)
- User profiling completed — key insight: introspective/proprioceptive motivation, night training, recede pattern
- v2 HTML rebuilt with witness cues, tonight mode, quieter tone
- Notion architecture designed and approved

### April 5, 2026
- CLAUDE.md, MEMORY.md, and skill commands (hockey, golf, body-movement, breathwork) created
- Two-tool system (HTML + Notion) established

### April 2026 (v3 rebuild session)
- Full rewrite of index.html — v3 Airtable rebuild
- Replaced Notion entirely — app is now the single tool for execution, logging, knowledge, and review
- Airtable backend connected: 3 tables auto-created on first launch
- 8 implementation phases completed across multiple PRs
- Key bugs fixed: _syncFromAirtable outside App object (broke all JS), setup overlay back navigation, Base ID URL parsing, Airtable primary field type requirement, testConnection endpoint correction
- App confirmed working end-to-end with real Airtable credentials

---

## Key Insights to Preserve

1. The user's body is a "door back to self" — not a performance metric. Never frame the program as athletic achievement.
2. The recede pattern is not failure — it's a known state. The program's job is to lower the cost of re-entry, not prevent withdrawal.
3. Witness mode is the primary engagement mechanism. Something to observe > something to do.
4. Tonight Mode is the most important single feature in the app. Protect it in every iteration.
5. Both sports are deeply integrated with the same postural system — any TVA/breathing/serratus work has direct carry-over to both skating and golf swing. Lead with this connection when explaining exercises.
6. The left-handed fade in golf is a stable, natural pattern — do not try to fix it. Build strength and stability around it.
7. Units are lbs and inches — never metric.
8. The app is a single HTML file by design — no build step, no split files. This is a hard constraint, not a preference.
