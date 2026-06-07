# AGENTS.md

Agent instructions for AI assistants working in this repository.

## What This Repo Is

A single-file HTML exam review note (`CSL_期末複習.html`) for NTU CSIE CSL course. The "codebase" is one file. There are no commands to run, no tests, no build step. Open the HTML file directly in a browser.

## How to Make Changes

All content lives in `<script type="text/markdown" id="md-chN">` blocks (Ch1–Ch6). Edit those blocks. The page renders on load via marked.js + KaTeX.

## What NOT to Do

- Do not create additional HTML files or split the single-file architecture.
- Do not add npm/yarn/pip dependencies or a package.json.
- Do not add comments explaining what sections do — the content is self-documenting through headings.
- Do not change the CSS variable names or color palette without checking all SVGs (inline attributes will be out of sync).

## Adding a New Deep-Dive Section

1. Add a `#### 🔬` (or `📐`, `🔧`) heading inside the relevant markdown block.
2. The JS `wrapDeepDives()` function auto-collapses it — no other changes needed.
3. Follow the sequence: analogy → derivation → worked example with numbers → comparison table.
4. SVG rules: no blank lines inside SVG, no `<style>` blocks, inline attributes only. See CLAUDE.md for the verified template and color palette.

## Adding a Self-Test Question

Append to the `## 自我測驗` section at the end of the chapter:

```markdown
**QN.** Question text here.

<details><summary>答案</summary>Answer text here.</details>
```

## Verified Emoji Set for Auto-Collapse

The JS regex `/^[🎯📐🆚📁🔬🚲⚙🔧🧠]/u` determines which h3/h4 headings become collapsible deep-dive panels. Only headings starting with one of these emojis (or matching `^EX[0-9]` for worked examples) will be wrapped. Other headings remain always-visible course structure.

## Key Files

| Path | Purpose |
|---|---|
| `CSL_期末複習.html` | The only artifact — edit this |
| `pdf/CSL_*.pdf` | Source lecture slides — read-only reference |
| `/Users/songhejun/Downloads/CSL/CSL Final/Slides/lab04_Stabilizer.ino` | TA's PD stabilizer code — referenced in Ch1 EX2 |
| `CLAUDE.md` | Full architecture reference for Claude Code |
