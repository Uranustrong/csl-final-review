# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a single-file HTML study note for the NTU CSIE CSL (Creative Studio Lab) course final exam. The only artifact is `CSL_期末複習.html` (~3000 lines). There is no build system, no package manager, no tests.

## File Structure

```
CSL_期末複習.html   ← the only file you edit
pdf/               ← original lecture PDFs (read-only reference)
pptx/              ← original lecture slides (read-only reference)
```

Source PDFs:
- `pdf/CSL_Dynamics.pdf` — Ch1 (89 pages)
- `pdf/CSL_Early HCI.pdf` — Ch2 (74 pages)
- `pdf/CSL_Mechanisms, friction, transmission.pdf` — Ch3 (135 pages)
- `pdf/CSL_trusses&springs.pdf` — Ch4 (156 pages)
- `pdf/CSL_Small and Large Actuation.pdf` — Ch5 (96 pages)
- `pdf/CSL_Lasercutter connections.pdf` — Ch6 (227 pages)

TA lab file referenced in Ch1: `/Users/songhejun/Downloads/CSL/CSL Final/Slides/lab04_Stabilizer.ino`

## HTML Architecture

The file is **self-contained** (no external JS files, only CDN links). Structure:

1. **CSS** (lines ~8–180): CSS variables (`--bg`, `--surface`, etc.), chapter/deepdive/self-test `<details>` styles
2. **HTML body** (lines ~181–270): sticky nav with 6 control buttons, chapter `<details class="chapter">` wrappers each containing a `<div class="chapter-body" data-md="md-chN">`
3. **Markdown source blocks** (lines ~368–2736): six `<script type="text/markdown" id="md-chN">` blocks holding the actual content
4. **CDN scripts**: KaTeX, marked.js v12
5. **Init script** (last `<script>` block): renders markdown → DOM, wraps deep-dive headings into `<details class="deepdive">`, classifies blockquotes, renders KaTeX, wires nav buttons

## Content Conventions

**Chapter structure inside each markdown block:**
- `## Section name` — course-outline level, always visible
- `### N. Topic name` — numbered course sections (e.g. `### 1. 電動馬達基礎`)
- `### 🧠/EX1/EX2... ` — supplementary h3 → **auto-collapsed** into deepdive panel
- `#### 🔬/📐/🆚/📁/🚲/🎯/⚙/🔧` — supplementary h4 → **auto-collapsed** into deepdive panel
- `#### N.x Sub-topic` — course sub-sections (no emoji → NOT collapsed)

The JS `wrapDeepDives()` function auto-wraps any h3/h4 that starts with one of these emojis: `🎯📐🆚📁🔬🚲⚙🔧🧠`. Worked examples starting with `EX[0-9]` are also auto-wrapped.

**Standard section tail:**
Every chapter ends with:
1. `## 公式整理表` or similar summary table (if applicable)
2. `## 易混淆 / 易考點` — common mistakes / high-frequency exam points
3. `## 自我測驗` — self-test questions with `<details><summary>答案</summary>...</details>`

**Blockquote callouts** (classified by leading emoji in JS):
- `> 💡` → green left-border (`remember`)
- `> ⚠` → red left-border (`warning`)
- `> 📦` → amber left-border (`definition`)
- `> ❓` → purple left-border (`thinking`)

## SVG Rules (Critical)

marked.js v12 has two hard constraints for inline SVGs:

1. **No blank lines inside SVG** — blank lines terminate the HTML block; SVG only renders up to the first blank line. Use single-line breaks between elements.
2. **No `<style>` blocks inside SVG** — CSS classes get stripped; all elements appear black on dark background. Use **inline attributes only**: `stroke="#79c0ff"` `fill="#7ee787"` etc.

Verified SVG template:
```html
<svg viewBox="0 0 720 420" xmlns="http://www.w3.org/2000/svg" style="background:#161b22; border:1px solid #30363d; border-radius:8px; max-width:100%; height:auto; display:block; margin:1em 0;">
  <line x1="..." y1="..." x2="..." y2="..." stroke="#6e7681" stroke-width="1"/>
  <text x="..." y="..." fill="#c9d1d9" font-family="ui-monospace,monospace" font-size="13">...</text>
</svg>
```

Dark theme color palette:
- Background: `#161b22` (SVG) / `#0d1117` (page)
- Border: `#30363d` / `#6e7681`
- Text primary: `#c9d1d9` / secondary: `#8b949e`
- Green (positive/small): `#7ee787`
- Blue (process/medium): `#79c0ff`
- Red (setpoint/warning): `#f85149` / `#ff7b72`
- Orange (intermediate): `#ffa657`
- Purple (secondary): `#d2a8ff`

## Writing Style

Every supplementary section should follow this structure:
1. **直覺類比** — everyday analogy first
2. **完整推導** — full mathematical derivation (no skipped steps)
3. **數字例** — worked example with concrete numbers
4. **對照表** — comparison table as summary
5. **易混淆** — ⚠ callout marking terminology traps

The user has EE/CS background and follows second-order ODE derivations, Nyquist stability, bearing kinematics, rigid body mechanics. Assume graduate-level physics/math literacy.

## Nav Buttons

| Button ID | Behavior |
|---|---|
| `btn-expand` | Opens all `details.chapter` |
| `btn-collapse` | Closes all `details.chapter` |
| `btn-show-ans` | Toggles open/close all self-test answer `<details>` |
| `btn-deepdive` | Toggles open/close all `details.deepdive` |

## Chapter Expansion Status

| Chapter | Lines (approx) | Status |
|---|---|---|
| Ch1 Dynamics | ~820 | Heavily expanded — PID derivations, SVG response curves, bang-bang vs critical comparison, P→D→I rationale, lab04_Stabilizer.ino walkthrough, 3 worked examples |
| Ch2 Early HCI | ~200 | Complete for history chapter — 8 people/events, timeline table, augmentation philosophy |
| Ch3 Mechanisms | ~650 | Expanded — wheel/axle $W=Fd$ derivation, bicycle energy chain, ball bearing half-speed rule + SVG, backlash 5-method rationale, 5 transmission "why" deep-dive (planetary/worm/rack/chain/differential) |
| Ch4 Trusses & Springs | ~350 | Expanded — Grübler formula for truss rigidity, living hinge spring mechanics, snap-fit $k \propto t^3/L^3$ full derivation with PLA numbers |
| Ch5 Actuation | ~270 | Expanded — SMA martensite/austenite phase transformation, full actuator comparison table |
| Ch6 Lasercutter | ~380 | Expanded — kerf compensation direction with worked example, 18-family catalog, teacher's strong opinion on finger joints |
