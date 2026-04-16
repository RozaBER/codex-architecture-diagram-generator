---
name: architecture-diagram
description: Generate professional, dark-themed architecture diagrams as standalone HTML files with inline SVG. Use when the user asks for system architecture diagrams, infrastructure diagrams, cloud architecture visualizations, security diagrams, network topology diagrams, or technical diagrams showing components and relationships.
license: MIT
metadata:
  version: "2.0"
  author: Cocoon AI (adapted for Codex)
---

# Architecture Diagram Skill (Codex Edition)

Generate professional technical architecture diagrams as self-contained HTML files with inline SVG graphics and CSS styling.

## How this skill should behave in Codex

1. Understand the user's architecture description (components, boundaries, protocols, flows).
2. Create **one self-contained `.html` file** using `assets/template.html` as the base.
3. Save the file in the current working directory (unless the user asks for a specific path).
4. If the user requests updates, edit the same HTML file in place.
5. Keep output deterministic, production-friendly, and readable.

## Design System

### Color Palette

Use these semantic colors for component types:

| Component Type | Fill (rgba) | Stroke |
|---------------|-------------|--------|
| Frontend | `rgba(8, 51, 68, 0.4)` | `#22d3ee` (cyan-400) |
| Backend | `rgba(6, 78, 59, 0.4)` | `#34d399` (emerald-400) |
| Database | `rgba(76, 29, 149, 0.4)` | `#a78bfa` (violet-400) |
| AWS/Cloud | `rgba(120, 53, 15, 0.3)` | `#fbbf24` (amber-400) |
| Security | `rgba(136, 19, 55, 0.4)` | `#fb7185` (rose-400) |
| Message Bus | `rgba(251, 146, 60, 0.3)` | `#fb923c` (orange-400) |
| External/Generic | `rgba(30, 41, 59, 0.5)` | `#94a3b8` (slate-400) |

### Typography

Use JetBrains Mono for all text (monospace technical aesthetic):
```html
<link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;500;600;700&display=swap" rel="stylesheet">
```

Font sizes: 12px for component names, 9px for sublabels, 8px for annotations, 7px for tiny labels.

### Visual Elements

**Background:** `#020617` (slate-950) with subtle grid pattern:
```svg
<pattern id="grid" width="40" height="40" patternUnits="userSpaceOnUse">
  <path d="M 40 0 L 0 0 0 40" fill="none" stroke="#1e293b" stroke-width="0.5"/>
</pattern>
```

**Component boxes:** Rounded rectangles (`rx="6"`) with 1.5px stroke and semi-transparent fills.

**Security groups:** Dashed stroke (`stroke-dasharray="4,4"`), transparent fill, rose color.

**Region boundaries:** Larger dashed stroke (`stroke-dasharray="8,4"`), amber color, `rx="12"`.

**Arrows:** Use SVG marker for arrowheads:
```svg
<marker id="arrowhead" markerWidth="10" markerHeight="7" refX="9" refY="3.5" orient="auto">
  <polygon points="0 0, 10 3.5, 0 7" fill="#64748b" />
</marker>
```

**Arrow z-order:** Draw connection arrows early in the SVG (after the background grid) so they render behind component boxes.

**Masking arrows behind transparent fills:** Since component boxes use semi-transparent fills (`rgba(..., 0.4)`), draw an opaque background rect first:
```svg
<!-- Opaque background to mask arrows -->
<rect x="X" y="Y" width="W" height="H" rx="6" fill="#0f172a"/>
<!-- Styled component on top -->
<rect x="X" y="Y" width="W" height="H" rx="6" fill="rgba(76, 29, 149, 0.4)" stroke="#a78bfa" stroke-width="1.5"/>
```

**Auth/security flows:** Dashed lines in rose color (`#fb7185`).

**Message buses / Event buses:** Small connector elements between services:
```svg
<rect x="X" y="Y" width="120" height="20" rx="4" fill="rgba(251, 146, 60, 0.3)" stroke="#fb923c" stroke-width="1"/>
<text x="CENTER_X" y="Y+14" fill="#fb923c" font-size="7" text-anchor="middle">Kafka / RabbitMQ</text>
```

### Spacing Rules

**CRITICAL:** When stacking components vertically, ensure proper spacing to avoid overlaps.

- Standard component height: 60px for services, 80-120px for larger components
- Minimum vertical gap between components: 40px
- Inline connectors (message buses): place inside the gap, not overlapping component boxes

### Legend Placement

**CRITICAL:** Place legends outside all boundary boxes.

- Compute where all boundaries end (`y + height`)
- Place legend at least 20px below the lowest boundary
- Expand SVG `viewBox` height if needed

### Layout Structure

1. Header (title and subtitle)
2. Main SVG diagram in a rounded border card
3. Summary cards (3 cards below diagram)
4. Footer metadata line

## Template Usage

Start from `assets/template.html` and customize:

1. Update document title and header text
2. Adjust SVG `viewBox` dimensions when needed
3. Add/reposition components and boundaries
4. Draw connection arrows and labels
5. Update three summary cards
6. Update footer metadata

## Output Contract

Always output a single `.html` artifact that is:

- Fully self-contained (embedded CSS + inline SVG)
- Browser-openable without build steps
- Free of JavaScript unless explicitly requested
- Easy to edit for iterative follow-up requests
