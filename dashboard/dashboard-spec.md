# Dashboard Specification — CTC Director Meeting Facilitation Tool

## Purpose
An interactive, single-screen facilitation dashboard used during the 60-minute director meeting. Designed to replace a linear slide deck with a navigable, modular display that allows facilitators to move between sections fluidly in response to the conversation — while maintaining a visible meeting structure that keeps the director oriented.

---

## Display Requirements
- **Primary use:** Laptop screen across a table (intimate setting, close viewing distance)
- **Secondary use:** Boardroom display / projected large screen
- **Resolution target:** Works at 1280x800 minimum; scales cleanly to 1920x1080 and larger
- **Interaction:** Mouse/trackpad driven by one facilitator while the other leads conversation
- **No internet dependency during meeting:** Should work as a local file or be fully loaded before the meeting begins
- **No audio or animation dependencies**

See `display-requirements.md` for technical detail.

---

## Architecture

### Layout
```
┌─────────────────────────────────────────────────────────┐
│  HEADER: Meeting title + elapsed time indicator         │
├──────────────┬──────────────────────────────────────────┤
│              │                                          │
│  LEFT NAV    │         MAIN CONTENT AREA                │
│  (sections)  │         (changes on nav click)           │
│              │                                          │
│              │                                          │
│              │                                          │
│              │                                          │
└──────────────┴──────────────────────────────────────────┘
```

### Persistent Elements (always visible)
- **Header:** Initiative name, CCIU branding (minimal), current section title
- **Left navigation rail:** All section labels visible at all times, current section highlighted, completed sections visually marked
- **Time indicator:** Suggested time allocation per section visible in nav (not a countdown clock — a guide)

### Navigation Rail Sections
```
○  Welcome + Agenda         (3 min)
○  What We Know             (10 min)
○  The Bridge               (5 min)
○  The Framework            (20 min)
   ├── Pillar 1: Infrastructure
   └── Pillar 2: Protocol + PD
○  Discussion               (10 min)
○  Decisions                (7 min)
○  Next Steps               (5 min)
```

---

## Section Specifications

### Section 1 — Welcome + Agenda
**Content:** Clean agenda display
- List of 7 segments with time allocations
- The three outcomes for the hour (bullet points)
- Minimal — this is mostly verbal

**Design note:** Should feel like a professional agenda card, not a slide title

---

### Section 2 — What We Know
**Content:** Two-part display

**Part A — Audit Findings**
- 2–3 headline findings displayed as distinct, readable cards
- Each finding: short bold label + 1–2 sentence description
- Visual indicator connecting finding to the solution it motivates (subtle — an arrow or color link to the pillar that addresses it)

**Part B — Curriculum Artifact Display**
- A placeholder panel where an audit artifact (lesson plan, curriculum map) can be displayed or referenced
- Label: "Current state — [program], [campus]"
- Note: actual artifact may be printed rather than displayed digitally

**Part C — Focus Group Finding**
- Single prominent callout: the unit/lesson finding
- Designed to be left on screen while the facilitator reads it aloud and discusses it

**Interactive element:** Toggle between Audit Findings / Focus Group Finding views

---

### Section 3 — The Bridge
**Content:** Transitional panel — simple, verbal-forward
- Two-pillar summary (brief — one line each)
- Parallel district work callout (one sentence)
- This section should be on screen briefly — the facilitator is talking, not pointing at content

---

### Section 4A — Pillar 1: Infrastructure
**Content:** Three-option spectrum display

**Visual design:**
- Three option cards displayed side by side (or stacked on smaller screens)
- Each card: option letter + name + 3–4 bullet points of key characteristics
- Color coding:
  - Option A (Low-tech): neutral gray
  - Option B (Mid-tech): blue
  - Option C (Purpose-built): teal
- Recommendation indicator: a subtle badge on the recommended option (or options depending on context)

**Interactive element:**
- Click each card to expand detail view (pros, cons, best fit)
- "Our recommendation" toggle that highlights the recommended option and displays rationale

**Non-negotiable callout:** A persistent banner or sidebar note stating what stays consistent regardless of option chosen

---

### Section 4B — Pillar 2: Protocol + Teacher Learning
**Content:** Three-option spectrum display + PL arc visual

**Part A — Protocol Options**
- Same card structure as Pillar 1
- Three options: DACUM-primary / DACUM-UbD hybrid / UbD-primary
- Color coding consistent with Pillar 1 card system
- Recommendation indicator on Option B (hybrid)

**Part B — Professional Learning Arc**
- Visual flow diagram: Foundational PD → Task Analysis → Collaborative Writing → Housing Output
- Each phase: name + brief description + estimated time
- Designed to make the arc feel sequential and tangible, not abstract

**Part C — Unit Plan Template Preview**
- A simplified view of the unit plan template fields (Stage 1, 2, 3 headers with brief descriptions)
- Or a link/button: "View sample unit" that opens a full-screen template view

**Interactive element:**
- Toggle between Protocol Options view and PL Arc view
- Expandable option cards for detail

---

### Section 5 — Discussion
**Content:** Facilitation support panel — not for display to director
- Anticipated objections and responses (from `run-of-show.md`)
- OR: clean "open space" panel — minimal content, signals listening mode

**Design note:** Consider whether this section should show the director a visual or be essentially blank (white panel with just the section label). The facilitator is listening, not presenting.

**Option:** Display a simple "What's landing?" prompt on screen as a visual anchor for the conversation

---

### Section 6 — Decisions
**Content:** Two-question decision display

**Question 1 — Infrastructure**
- The three options from Pillar 1 displayed as a compact spectrum
- Visual selector (clickable — not for data capture, just for visual focus)

**Question 2 — Pilot Starting Point**
- Program area options (Building Trades visible, others as generic placeholders)
- Campus options

**Design note:** This is not a form — it is a visual anchor for a verbal conversation. Selections made here should be noted separately.

---

### Section 7 — Next Steps
**Content:** Proposed next step display
- Description of the teacher working session (the proposed pilot)
- What it involves, who should be there, what it produces
- Space for confirming: owner, timeline, information needed

**Leave-behind reminder:** List of items being left with the director

---

## Technical Implementation Notes

### File type
Single HTML file — self-contained, no external dependencies except CDN resources loaded at runtime. Should function offline once loaded.

### Responsive behavior
- At laptop width (~1280px): left nav + main content side by side
- At projector/large screen width (1920px+): content scales up, margins increase, text remains readable from distance
- No mobile optimization needed

### Navigation behavior
- Clicking a section in the left nav loads that section's content instantly (no animation delay)
- Sections 4A and 4B are sub-navigable from within Section 4
- No "back / next" buttons required — navigation is always available in the left rail

### Color and typography
- Follow design system in `display-requirements.md`
- Optimize for readability at distance (large screen use) — minimum 16px body text, 20px+ for key content
- High contrast for boardroom projection

### No tracking, no data submission
This is a facilitation tool. Nothing is saved or transmitted.
