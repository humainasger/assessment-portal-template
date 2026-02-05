# Assessment Portal Template

A self-contained HTML presentation system for client assessments and strategy work. Built by Wildfire.

## Quick Start

```bash
# Copy template
cp -r assessment-portal-template/ client-assessment/
cd client-assessment/

# Preview (use VS Code Live Server or similar)
open portal/index.html

# Deploy
wrangler pages deploy . --project-name=client-assessment
```

## Documentation

See **CLAUDE.md** for full documentation including:
- Architecture overview
- How to customize for new clients
- Content page templates
- Tips from real client work

## Structure

```
/
├── CLAUDE.md           # Full documentation
├── portal/
│   └── index.html      # Navigation hub with sidebar
├── index.html          # Consumer landing mockup
├── canvas.html         # Business canvas
├── competitors.html    # Competitor analysis
├── concepts.html       # Concept ideas
├── agenda.html         # Meeting agenda
├── notes.html          # Live meeting notes
├── research.html       # Research findings
├── b2b.html           # B2B landing mockup
├── assets/            # Images, screenshots
└── charts/            # Generated diagrams
```

## Origin

Built for the DEWA x e-Boks assessment (Jan-Feb 2026). The portal format helped present 2 weeks of research in a single explorable URL, leading to a 65k kr/month retainer.

## License

MIT - use freely for your own client work.
