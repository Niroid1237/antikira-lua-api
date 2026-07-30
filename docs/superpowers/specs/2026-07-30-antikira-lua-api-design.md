# Antikira Lua API — HTML Design Spec

## Overview
Redesign the standalone HTML documentation page for the Antikira Lua API. The page is a single-file HTML documentation site with sidebar navigation, code examples, and collapsible API cards.

## Layout
- Fixed sidebar on the left (280px) with glassmorphism (`backdrop-filter: blur`, reduced opacity background, thin border)
- Main content area centered with `max-width: 960px`
- Floating "On This Page" table of contents — sticky on the right, shown only at viewport > 1280px
- Footer with repo link and version badge

## Visual Style
- **Palette**: Dark theme (`#0a0c0f` base, `#111418` secondary, `#161b22` cards). Accent: `#58a6ff` blue.
- **Glow**: `box-shadow` with blue tint on hover for cards and interactive elements
- **Hero**: Full-width gradient header with dot-grid background pattern (CSS `radial-gradient`), subtle glow behind badges, larger title (clamp 28–40px)
- **Typography**: Inter for body, JetBrains Mono for code
- **Cards**: Collapsible with smooth `max-height` transition (replace display:none/block with max-height animation), hover border-highlight with glow shadow
- **Code blocks**: Darker background (`#0d1117`), tab bar showing "Lua" / "Output" where relevant, improved syntax highlighting (consistent token colors)
- **Info/warning boxes**: Colored left border + tinted background, consistent with card radius

## Sections
1. **Hero** — Title, description, badge row
2. **Getting Started** — Folder setup, menu workflow, example cards (First Script, Event, Create Move, Config)
3. **Runtime** — Error handling, FFI, search paths, code example
4. **Callbacks** — register/unregister, callback constants, supported kinds as module-cards
5. **API Overview** — Global helpers, tables, callback names, Color type
6. **Modules** — antikira, globals, engine, entitylist, render, menu, environment, config, buttons
7. **Objects** — entity, cmd, event

## Components
- **Badges** — inline colored pill elements (blue, green, purple, orange)
- **Func-tags** — clickable monospace tags for function names
- **Module cards** — non-collapsible cards with function tag lists
- **Quick links** — horizontal link grid
- **Links grid** — card-style link grid for related pages

## Interactive Features
- **Client-side search**: Input field in sidebar header, live filters cards by title/content match
- **Collapsible cards**: Smooth open/close with max-height CSS transition (not display toggle)
- **Scroll spy**: Active nav item updates based on current scroll position via IntersectionObserver
- **Scroll-to-top button**: Appears after 300px scroll
- **On This Page nav**: Right sidebar with anchor links to each `<h2>`

## Responsive
- **Mobile (< 900px)**: Sidebar slides in as overlay, hamburger toggle top-left, content full-width, cards stack vertically
- **Tablet (900–1280px)**: Sidebar still visible, On This Page hidden
- **Desktop (> 1280px)**: Full layout with On This Page
- All spacing uses `clamp()` for fluid scaling

## Animations
- Sections fade-in-up on scroll (IntersectionObserver + CSS `fadeInUp` keyframe)
- Card open/close: max-height transition (300ms ease)
- Sidebar slide: transform translateX (300ms ease)
- Hover: cards lift 1–2px, border color + glow transition (150ms)

## Icons
Replace all HTML entity icons (`&#9679;`, `&#9654;`, `&#9881;`, etc.) with **Lucide** SVG icons, loaded from CDN.
