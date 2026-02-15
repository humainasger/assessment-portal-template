# Portal Style Guide

Last updated: 2026-02-15

## Design Principles

1. **Readability first.** Generous whitespace, large body text, narrow content column. The page should feel like a well-typeset article, not a dashboard.
2. **Clean typography.** Inter font, 18px body minimum, 1.7 line-height. Let the content breathe.
3. **No emojis.** Use inline SVG icons instead. Keep it professional.
4. **No em dashes.** Use -- (double hyphen) in content.
5. **Visuals where they help.** Mermaid diagrams for flows, relationships, and timelines. Not decoration.
6. **Direct language.** No corporate speak, no jargon. Specific numbers over vague claims.

## Typography

```
Body text:     18px / 1.7 line-height / Inter 400
Bold:          Inter 600-700, darker color than body
H1:            42px / 1.15 line-height / Inter 700 / -1px letter-spacing
H2:            28px / Inter 700 / -0.5px letter-spacing
H3:            20px / Inter 600
Section meta:  14px / muted color / uppercase for labels
Table text:    16px body, 13px uppercase headers
```

## Colors

```css
:root {
    --purple: #3D1A54;         /* Primary brand */
    --purple-light: #F8F5FB;   /* Purple tint backgrounds */
    --accent: #C41230;         /* Callouts, emphasis */
    --text: #1a1a2e;           /* Headings, bold text */
    --text-secondary: #555;    /* Body text */
    --text-muted: #999;        /* Meta, labels */
    --border: #e8e8ec;         /* Dividers, table borders */
    --bg: #fafaf9;             /* Page background */
}
```

## Layout

- **Max content width:** 680px (classic readable column)
- **Page padding:** 80px top, 120px bottom, 24px horizontal
- **Section spacing:** 72px between sections
- **Paragraph spacing:** 20px margin-bottom
- **List item spacing:** 8px margin-bottom

## Components

### Callout

Left-bordered box for key points, decisions, and questions.

```html
<div class="callout">
    <p><strong>Decision needed:</strong> What ships Feb 18 vs. what can wait?</p>
</div>

<!-- Purple variant for strategic questions -->
<div class="callout callout-purple">
    <p><strong>Question:</strong> How do we cascade this?</p>
</div>
```

Red left border by default (accent). Purple variant for strategic/brand questions.

### Section structure

```html
<div class="section">
    <span id="s1" class="section-anchor"></span>
    <h2>1. Section Title</h2>
    <div class="section-meta">30 minutes</div>
    
    <p>Introductory paragraph explaining the section.</p>
    
    <h3>Subsection heading</h3>
    <ul>
        <li><strong>Bold lead</strong> -- explanation text</li>
    </ul>
</div>

<hr>
```

### Tables

Minimal styling, white background, subtle borders.

```html
<div class="table-wrap">
    <table>
        <thead><tr><th>Column</th><th>Column</th></tr></thead>
        <tbody>
            <tr><td>Data</td><td>Data</td></tr>
        </tbody>
    </table>
</div>
```

### Numbered flow list

For step-by-step processes. Numbered circles on the left.

```html
<ol class="flow-list">
    <li>Customer scans wine at self-checkout kiosk</li>
    <li>Kiosk flags age-restricted item, displays QR code</li>
    <li>Customer opens app, scans QR with wallet</li>
</ol>
```

### Mermaid diagrams

Use for relationships, flows, and timelines. Not for decoration.

```html
<div class="mermaid-wrap">
    <pre class="mermaid">
graph LR
    A["Node A"] --> B["Node B"]
    style A fill:#3D1A54,stroke:#3D1A54,color:#fff
    style B fill:#F8F5FB,stroke:#3D1A54,color:#1a1a2e
    </pre>
</div>
```

Include mermaid.js in the head:
```html
<script src="https://cdn.jsdelivr.net/npm/mermaid@11/dist/mermaid.min.js"></script>
```

Initialize with brand theme:
```javascript
mermaid.initialize({
    startOnLoad: true,
    theme: 'base',
    themeVariables: {
        primaryColor: '#F8F5FB',
        primaryTextColor: '#1a1a2e',
        primaryBorderColor: '#3D1A54',
        lineColor: '#3D1A54',
        fontFamily: 'Inter, sans-serif',
        fontSize: '14px'
    }
});
```

### SVG icons (instead of emojis)

Clock:
```html
<svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
    <circle cx="12" cy="12" r="10"/><polyline points="12 6 12 12 16 14"/>
</svg>
```

Check:
```html
<svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
    <polyline points="20 6 9 17 4 12"/>
</svg>
```

Arrow right:
```html
<svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
    <line x1="5" y1="12" x2="19" y2="12"/><polyline points="12 5 19 12 12 19"/>
</svg>
```

Warning:
```html
<svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
    <path d="M10.29 3.86L1.82 18a2 2 0 0 0 1.71 3h16.94a2 2 0 0 0 1.71-3L13.71 3.86a2 2 0 0 0-3.42 0z"/>
    <line x1="12" y1="9" x2="12" y2="13"/><line x1="12" y1="17" x2="12.01" y2="17"/>
</svg>
```

## Sticky nav

Minimal top bar with section links. Frosted glass background.

```html
<nav class="topnav">
    <div class="topnav-brand">Page Title</div>
    <div class="topnav-links">
        <a href="#s1" class="active">Section 1</a>
        <a href="#s2">Section 2</a>
    </div>
</nav>
```

## What NOT to do

- No emojis in content (use SVG icons)
- No em dashes (use --)
- No body text smaller than 16px
- No dense card grids or dashboard layouts
- No colored backgrounds on the main page (white/near-white only)
- No stock illustrations or decorative images
- No more than 680px content width
- No walls of text without headings breaking it up
