# CLAUDE.md - Assessment Portal Template

## What This Is

A self-contained HTML presentation system for client assessments, strategy work, and discovery phases. Built for consultants who need to present research, mockups, and strategic recommendations in a polished, interactive format.

**Key features:**
- Sidebar navigation hub with iframe content viewer
- Self-contained HTML (no build step, no dependencies beyond Google Fonts)
- One-click deploy to Cloudflare Pages
- Professional look that impresses clients
- Works offline once loaded

## Origin Story: DEWA Assessment (Jan-Feb 2026)

Built for Wildfire's assessment of DEWA (Danish digital wallet, 50% owned by e-Boks). The engagement needed:
- Business canvas and strategic analysis
- Competitor research (AltID, Paradym, Lissi, Idura)
- 13 concept ideas across 3 strategic lanes
- Landing page mockups (consumer, government, B2B)
- Meeting agenda and live notes
- Press coverage compilation

The portal let us present 2 weeks of research in a single URL that Lorenz (DEWA) could explore before and after our 3-hour assessment meeting. It became the living document for the engagement.

**Result:** 65.000 kr/month retainer starting Feb 2026.

## Architecture

```
/
├── portal/
│   └── index.html      # Navigation hub (sidebar + iframe viewer)
├── index.html          # Default content page (often consumer landing)
├── canvas.html         # Business/strategy canvas
├── competitors.html    # Competitor analysis
├── concepts.html       # Concept ideas / recommendations
├── agenda.html         # Meeting agenda
├── notes.html          # Meeting notes (update live during meeting)
├── [custom].html       # Any additional pages
├── assets/             # Screenshots, logos, mockups
└── charts/             # Generated diagrams
```

### How Navigation Works

The portal (`/portal/index.html`) contains:
1. **Sidebar** - Dark themed, with sections and nav items
2. **URL bar** - Shows current page title (fake browser chrome feel)
3. **Iframe viewer** - Loads content pages

```javascript
function navigate(file, title, el) {
    document.getElementById('viewport-frame').src = file;
    document.getElementById('url-display').textContent = title;
    // Update active state
}
```

External sites (competitor websites, live client sites) open in new tabs via `navigateExternal()` since they block iframe embedding.

### Path Convention

Portal is in `/portal/` subfolder, so all content references use `../`:
- `navigate('../canvas.html', 'Business Canvas', this)`
- `<iframe src="../index.html">`

## Creating a New Client Portal

### 1. Copy the Template

```bash
cp -r assessment-portal-template/ client-assessment/
cd client-assessment/
```

### 2. Update Brand Colors

Edit `portal/index.html` CSS variables:

```css
/* Example: DEWA colors */
--sidebar-bg: #1a1a2e;
--accent-pink: #E91E63;
--deep-purple: #3D1A54;
--client-red: #C41230;  /* e-Boks red */
```

Each content page has its own `<style>` block - update colors there too.

### 3. Update Sidebar Navigation

In `portal/index.html`, modify the nav sections:

```html
<div class="nav-section">
    <div class="nav-section-label">Strategy</div>
    <div class="nav-item" onclick="navigate('../canvas.html', 'Business Canvas', this)">
        <span class="dot" style="background: var(--accent);"></span>
        Business Canvas
        <span class="meta">Full</span>
    </div>
</div>
```

**Nav item anatomy:**
- `dot` - Color-coded indicator (use gradients for multi-lane items)
- Label - Page name
- `meta` - Optional badge (count, "live", "NEW", etc.)

### 4. Create Content Pages

Each page is self-contained HTML. Template structure:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>[Page Title] - [Client] Assessment</title>
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
    <style>
        /* Page-specific styles */
        :root {
            --primary: #3D1A54;
            --accent: #E91E63;
        }
        /* ... */
    </style>
</head>
<body>
    <!-- Content -->
</body>
</html>
```

### 5. Deploy

```bash
# First time - create project
wrangler pages project create client-assessment

# Deploy
wrangler pages deploy . --project-name=client-assessment
```

URL: `https://client-assessment.pages.dev/portal`

## Design System

**Read STYLE-GUIDE.md for the full design reference.** Key rules:

1. **18px minimum body text.** No exceptions.
2. **680px max content width.** Classic readable column.
3. **No emojis.** Use inline SVG icons (see STYLE-GUIDE.md for library).
4. **No em dashes.** Use -- (double hyphen).
5. **Mermaid diagrams** for flows, relationships, timelines. Not decoration.
6. **Generous whitespace.** 72px between sections, 20px between paragraphs.

Use `template-content-page.html` as the starting point for all new pages. It includes the full CSS, nav, mermaid setup, and examples of every component (callouts, tables, flow lists, diagrams).

The design is inspired by clean editorial layouts (see asger.me/resources for reference). Think article, not dashboard.

## Content Page Types

### Business Canvas (`canvas.html`)

Strategic overview. Use the standard template layout with sections, tables, and mermaid diagrams for strategic maps.

### Competitor Analysis (`competitors.html`)

For each competitor: key facts, strengths/weaknesses, how client differs. Use tables for comparison, callouts for key insights.

### Meeting Agendas and Notes

Use the template layout with numbered sections (h2), time allocations in section-meta, and callout boxes for decisions needed. Mermaid diagrams for flows and relationships. Numbered flow-lists for processes.

### Research Pages

Deep dives on specific topics. Same template, same style. Use h3 subsections within each h2 section. Tables for data. Mermaid for market maps.

### Landing Page Mockups

Full HTML mockups of proposed pages. These are separate from the content template -- they have their own styling to match the proposed design. Move to Archive section in sidebar when no longer current.

## Tips From DEWA Build

### What Worked Well

1. **Charts as images** - Generated via canvas/HTML, exported as PNG. Easier than live charts.

2. **Fake browser chrome** - The URL bar showing page titles adds polish.

3. **Color-coded dots** - Instant visual grouping of related items.

4. **External site links** - Showing competitor sites live (in new tab) is more credible than screenshots.

5. **Section counts** - "Concept Ideas (13)" tells client there's depth.

6. **Press compilation** - Gathering all press coverage in one place shows thoroughness.

### What to Avoid

1. **Too many pages** - Keep it focused. 8-12 pages max.

2. **Incomplete mockups** - Better to have 3 polished mockups than 10 rough ones.

3. **Stale notes** - Update notes.html during/after meeting or remove it.

4. **Generic templates** - Customize heavily. Client should feel it was built for them.

## File Naming Convention

- `index.html` - Default/consumer landing
- `canvas.html` - Business canvas
- `competitors.html` - Competitor analysis  
- `concepts.html` - Ideas/recommendations
- `agenda.html` - Meeting agenda
- `notes.html` - Meeting notes
- `[segment].html` - Segment-specific landing (e.g., `government.html`, `b2b.html`)
- `[topic].html` - Topic deep-dives (e.g., `press.html`, `research.html`)

## Cloudflare Pages Notes

- Auto-redirects `.html` to clean URLs (`/canvas.html` → `/canvas`)
- Root `index.html` serves as 404 fallback
- Free tier is plenty for client portals
- Custom domains easy to add

## Repo Structure

This template repo:
```
assessment-portal-template/     # Template (this repo)
```

Client implementations:
```
humainasger/client-assessment-portal    # DEWA (private)
humainasger/[client]-assessment         # Future clients
```

## Quick Reference

| Task | Command |
|------|---------|
| Local preview | `open portal/index.html` (won't work due to CORS - use Live Server) |
| Deploy | `wrangler pages deploy . --project-name=NAME` |
| Update | Same deploy command (overwrites) |
| Custom domain | Cloudflare dashboard → Pages → Custom domains |

---

*Template created Feb 2026 from DEWA assessment portal. Contact: asger@wildfire.business*
