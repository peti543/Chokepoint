# CHOKEPOINT

> Mining is cheap. **Refining is the gate.** Whoever holds it holds everything.

A mobile-first, installable idle / incremental game themed on the real
critical-minerals mining-and-refining supply chain. It ships as a single
self-contained, offline HTML file plus a PWA manifest and service worker, no
external assets, no network required after first load.

## Play it

- **On a phone:** open `index.html` from any static host (or your device), then
  **Add to Home Screen**. It launches fullscreen, portrait, and keeps running
  while closed.
- **Locally:** just open `index.html` in a browser. The game is fully playable
  from the single file; the manifest/service worker only add installability and
  offline caching (service workers require `http(s)://`, not `file://`).

## The game

You operate three real production chains. Each stage's output feeds the next
stage's input. Mining is fast and cheap; **refining is the slow, capital-heavy
chokepoint.**

- **Silicon:** quartz → metallurgical silicon → polysilicon → Czochralski ingot
  → wafer → finished chip
- **Aluminium + Gallium:** bauxite → alumina → aluminium. **Gallium is a
  byproduct**, it only flows while you run the aluminium smelter, and chips
  need it, so scaling chips forces you to run aluminium too.
- **Rare earth:** REE ore → crack/leach → **solvent-extraction separation (the
  true chokepoint, slowest, most expensive)** → oxides → rare-earth metals →
  NdFeB magnets

**Final sink:** chips + magnets + power → **Datacenter** AI-compute capacity,
the top currency the prestige multiplier scales.

### Core systems

- **Idle accrual:** stages produce per second while you play *and* while the app
  is closed. Tap mining nodes to bootstrap, then buy machines to automate.
- **Waste meter (a real cost, not decoration):** every refining step emits waste
  (radioactive residue + acid from rare-earth separation; high energy + SiCl₄
  from silicon; CO₂, tailings, acid in general). Pollution drops your efficiency.
  Tolerate it for throughput, or invest in **Treatment Plants** and **Green
  Refits**, slower and costlier, but cleaner.
- **Offline earnings:** the refineries keep running while you're away (capped at
  8 hours) with a "while you were away" summary on return.
- **Prestige, New Fab Generation:** retool the whole operation. Wipes the run
  but mints permanent fab credits from the datacenter capacity you built, which
  **compound** your output forever.
- **Coming soon:** zinc/germanium, graphite, and antimony nodes are visible-but-
  locked so the tech tree reads whole.

## Files

| File | Purpose |
|------|---------|
| `index.html` | The entire game, logic, UI, styling, save/load, offline sim |
| `manifest.webmanifest` | PWA metadata (name, portrait, standalone, icons) |
| `sw.js` | Offline-first service worker (cache-first, local assets only) |
| `icon.svg`, `icon-maskable.svg` | App icons |

## Tech notes

- Pure vanilla JS/CSS/HTML, no build step, no dependencies.
- Portrait-only, no horizontal scroll, ≥44px tap targets, safe-area insets
  respected, high-contrast dark industrial theme readable at arm's length.
- Saves to `localStorage` every 10s and on every close (`pagehide` /
  `visibilitychange`), which is what makes offline earnings accurate.
- Append `#debug` to the URL for a small testing panel.
