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

### Sports Context
- **Hockey**: Recreational/fitness-focused. Key frustrations: speed/confidence on edge (issues #1, #3, #4 from original survey). Skating push power compromised by right leg weakness and knee compensation.
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

## Program Architecture Decisions

### Two-Tool System (established March 7, 2026)
- **`index.html`** = Execution environment. Mobile home screen app. Checklist, Tonight Mode, confidence rating, exercise cues. Used *during* sessions.
- **Notion** = Reflection + knowledge environment. Session log, deep content pages, resource library, weekly review. Used *between* sessions. HTML embeds inside Notion via iframe.

**Rationale**: Execution mode and reflection mode are different mental states. Conflating them is why Notion was abandoned previously. Keeping jobs separate protects both tools.

### Notion Architecture (designed March 7, 2026)
- Hub page → 4 sub-pages:
  1. Session Log (database, 60-second entry: date, pain, confidence, one sentence)
  2. Knowledge Base (Hockey page + Golf page + Injury deep-dives)
  3. Resource Library (YouTube, drill clips, LLM chats, articles — tagged, searchable)
  4. Weekly Review (one prompt, one metric snapshot, ~5 minutes)
- Implementation guide: `inputs/notion-setup.docx`

### HTML App Features (as of v2, March 7, 2026)
- 6 tabs: Program, Golf, On Ice, Progress, Milestones, Gear
- Tonight Mode: 3-exercise minimum, low-stakes re-entry, accessible from header
- Witness cues on each exercise (what to observe, not just do)
- Milestones as acknowledgements (not goals to chase)
- Confidence pip scale (1–10)
- localStorage persistence for session data
- CSV export for Excel
- Dark default / light toggle, WCAG AAA
- Band-primary exercises, home equipment only

---

## Program Content

### Phases
1. **Breathing & TVA Activation** (10–12 min): Supine TVA breathing, Deadbug with leg extension
2. **Serratus & Scapular Stability** (10 min): Wall Y raises, Plank with serratus push, Serratus wall press hold
3. **Lower Body Strength & Knee Alignment** (15–20 min): Bulgarian split squats, Spanish squats, Lateral step downs
4. **Hip Control & Skating Power** (10 min): Golf driver lateral chain push, Banded monster walks, Lateral skater bounds, Single-leg RDL

### Tracking Metrics
- Quad circumference (right vs left, measured 6" above kneecap)
- Single-leg balance time (per leg)
- Bulgarian split squat load
- Skater bound distance
- One-leg glide time on ice
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

### March 7, 2026 (source chat)
- Initial program build session
- Rehab plan constructed from scratch based on original exercise list
- v1 HTML built (impersonal tone, rejected)
- User profiling completed — key insight: introspective/proprioceptive motivation, night training, recede pattern
- v2 HTML rebuilt with witness cues, tonight mode, quieter tone
- Notion architecture designed and approved
- Word document with full Notion setup + Hockey knowledge page + Golf knowledge page created

### April 5, 2026 (current session)
- User requested: CLAUDE.md (session protocol, testing gate, Feynman+Karpathy refinement model)
- User requested: MEMORY.md (persistent profile + project history)
- User requested: Skill commands — hockey, golf, body-movement, breathwork specializations
- Design decision pending: skills vs CLAUDE.md for domain intelligence (see Recommendation below)

---

## Open Decisions & Recommendations

### Skills vs. CLAUDE.md for Domain Intelligence

**Recommendation: Use skills (slash commands), not CLAUDE.md.**

CLAUDE.md is always-on context — it loads every session whether or not that session involves hockey mechanics. Keeping it lean makes every session faster and more focused.

Domain skills (hockey, golf, body movement, breathwork) carry deep, specialized knowledge that would make CLAUDE.md unwieldy. More importantly, that depth is only needed situationally — when analyzing a stride, designing a drill, or diagnosing a breathing pattern.

Slash commands (`/hockey`, `/golf`, `/body-movement`, `/breathwork`) are invoked when needed, allow focused domain reasoning, and can be updated independently as knowledge deepens.

**Hybrid exception**: CLAUDE.md keeps a one-paragraph domain summary (context anchors) so any session has enough baseline to be useful. The skills go deep when invoked.

---

## Key Insights to Preserve

1. The user's body is a "door back to self" — not a performance metric. Never frame the program as athletic achievement.
2. The recede pattern is not failure — it's a known state. The program's job is to lower the cost of re-entry, not prevent withdrawal.
3. Witness mode is the primary engagement mechanism. Something to observe > something to do.
4. Tonight Mode is the most important single feature in the app. Protect it in every iteration.
5. Both sports are deeply integrated with the same postural system — any TVA/breathing/serratus work has direct carry-over to both skating and golf swing. Lead with this connection when explaining exercises.
6. The left-handed fade in golf is a stable, natural pattern — do not try to fix it. Build strength and stability around it.
