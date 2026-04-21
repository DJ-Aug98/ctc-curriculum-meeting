# Display Requirements

## Use Contexts

### Primary — Laptop (across table)
- Viewing distance: 3–5 feet
- Screen size: 13–16 inch laptop display
- Resolution: 1280x800 to 1920x1200
- Interaction: trackpad or mouse, driven by one facilitator
- Lighting: variable — office, conference room
- Context: intimate, one-on-one or small group

### Secondary — Boardroom Display / Projection
- Viewing distance: 8–20 feet
- Screen size: 65–100 inch display or projected equivalent
- Resolution: 1920x1080 standard
- Interaction: facilitator drives from laptop, display is mirrored
- Lighting: conference room, may have glare from windows
- Context: formal, director + possible staff

---

## Typography Requirements

### Laptop use
- Body text minimum: 15px
- Section headers: 20–22px
- Card labels: 13px minimum
- Navigation rail: 14px

### Boardroom / large screen scaling
- All text should scale up proportionally when viewport is wide
- Target: body text reads at ~24px equivalent at 1920px wide
- Implement via `clamp()` or viewport-relative units for key text sizes
- Navigation rail labels must remain legible at distance — 16px minimum at all sizes

### Font
- System sans-serif stack: `-apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif`
- Or match host application font if embedded in a specific environment

---

## Color and Contrast

### General
- High contrast required for projection readability
- Avoid light gray text on white backgrounds — increases contrast thresholds for large-screen use
- All text should meet WCAG AA contrast minimums at minimum; AAA preferred for large-screen contexts

### Background
- Primary content area: white or near-white
- Navigation rail: subtle off-white or very light gray
- No dark backgrounds on primary content — can be hard to read in variable boardroom lighting

### Color usage
- Use color to encode meaning (option categories, pillar differentiation), not decoration
- Limit to 3–4 colors in any single panel
- Pillar 1 (Infrastructure): blue family
- Pillar 2 (Protocol + PD): teal family
- Audit / grounding content: neutral gray family
- Recommendation indicators: amber or a distinct accent

---

## Layout and Scaling

### Responsive breakpoints
```
< 1024px    Stacked layout (nav on top, content below) — fallback only
1024–1440px Standard laptop layout (nav rail left, content right)
> 1440px    Wide layout — content area expands, margins increase
```

### Navigation rail
- Fixed width: 200–220px on laptop, scales slightly on large display
- Always visible — no hamburger menu or collapse
- Vertically scrollable if needed (unlikely given section count)

### Content area
- Max content width: ~900px even on large screens — prevents excessively long line lengths
- Center content within available space on large displays
- Card grids: 3-column on wide layouts, 1-column fallback on narrow

---

## Interaction Model

### Navigation
- Click nav item: instant section load, no animation delay
- Active section highlighted in nav rail
- No browser history navigation required (single-page behavior)

### Expandable cards
- Click to expand: smooth reveal of additional content (pros/cons, detail)
- One card open at a time within a panel (accordion behavior) or all expandable independently — TBD in build
- Keyboard accessible

### Recommendation toggles
- Click "show recommendation" to highlight recommended option with rationale
- Toggle should be visually obvious — not a subtle color change

---

## File and Delivery

### Format
Single self-contained HTML file

### Dependencies
- No backend, no server required
- External CDN resources (fonts, icons if used) should have local fallbacks
- Should function at the meeting without internet if CDN resources are cached or bundled

### Loading
- Load fully before the meeting begins
- No splash screen or loading state visible to participants

### Printing
- A print stylesheet is a nice-to-have — allows key panels to be printed as leave-behinds if needed
- Not required for MVP
