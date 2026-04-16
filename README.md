# Architecture Diagram Generator (Codex Skill)

**Need an architecture diagram? Let Codex generate one for you.**

This repository provides a Codex-compatible skill that turns system descriptions into professional, dark-themed architecture diagrams as standalone HTML files.

- **No design work required** — describe architecture in plain language
- **Fast iteration** — ask Codex to add components, adjust flows, or restyle
- **Portable output** — a single HTML file that opens in any browser

![Version](https://img.shields.io/badge/version-2.0-blue)
![License](https://img.shields.io/badge/license-MIT-green)
![Codex](https://img.shields.io/badge/Codex-Skill-purple)

## Quick Start

1. Keep `architecture-diagram/SKILL.md` and `architecture-diagram/assets/template.html` in your workspace.
2. In Codex, ask it to use the architecture diagram skill.
3. Provide your architecture description.
4. Open the generated `.html` file in a browser.

Example prompt:

```text
Use the architecture-diagram skill to create an architecture diagram HTML for:
- React frontend
- Node.js API
- PostgreSQL database
- Redis cache
- AWS CloudFront in front
```

## Repository Layout

```text
architecture-diagram/
├── SKILL.md
└── assets/
    └── template.html
examples/
├── web-app.html
├── aws-serverless.html
└── microservices.html
```

## What the skill enforces

- Consistent dark design system
- Semantic colors by component type
- SVG layering so arrows render cleanly behind components
- Clear spacing and legend placement rules
- Three summary cards and footer metadata

## Output

The skill generates one self-contained HTML document with:

- Embedded CSS
- Inline SVG diagram
- No external runtime dependencies

## License

MIT
