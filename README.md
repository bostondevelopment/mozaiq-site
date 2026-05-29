# Mozaiq — color logic puzzles

A daily color logic puzzle game for iPhone. Three colors mix into six — figure out which section gets which paint by reading the intersections, beat the clock, climb the leaderboard.

→ **[The app + how to play](https://bostondevelopment.github.io/mozaiq-site/)**
→ **[Engineering deep-dive](https://bostondevelopment.github.io/mozaiq-site/engineering.html)** — solver, content pipeline, agent workflow

---

## About this repo

This repository hosts the public-facing site for Mozaiq — landing page, engineering write-up, privacy/terms/support. The Mozaiq app itself (React Native / Expo / TypeScript on Supabase) lives in a separate, private repository.

## About the app

Mozaiq is a daily color logic puzzle. Every board is split into connected sections; the cells where two sections cross show the *mixed* color of the two — yellow + blue = green, red + yellow = orange, red + blue = purple. Read the mix, work backward to the section colors, fill the board before time runs out.

The shipping bundle contains **~3,187 machine-validated puzzles** across 7×7, 9×9, and 15×15 boards, produced by a backtracking constraint solver and an automated validation loop that regenerates puzzles until they pass solvability, uniqueness, and no-guess audits.

**Status:** TestFlight beta (not the App Store, by choice).

## How it was built

The Mozaiq codebase was built solo by **directing AI coding agents (Claude Code, Cursor)** through a documented 6-phase prompt workflow — not by hand-writing the code. The interesting artifact isn't lines typed; it's the system the agents produced under direction:

- A **shared `@crosscolor/core` TypeScript package** that runs the same solver on the phone and in the validation pipeline — no logic drift between what generates puzzles and what plays them.
- An **industrial-grade procedural content factory** — 41 pipeline scripts covering ingest, layout extraction, generation, difficulty rating, curation, and a convergence-loop validator that re-runs until the bundle passes audits.
- A **~37K-line TypeScript codebase** across a monorepo (`packages/core`, `mobile`, `src`, `scripts`) with a Supabase backend, a Vite/React web evaluation tool, and the React Native player.
- A **self-built local iOS build-sign-submit pipeline** — full Apple code-signing chain, `xcodebuild` archive → IPA, EAS submit to TestFlight — no paid CI services.

The **[engineering page](https://bostondevelopment.github.io/mozaiq-site/engineering.html)** walks through all of it.

---

## Author

Built by **Michael Finneran** — Boston, MA
[linkedin.com/in/michaelfinneran](https://linkedin.com/in/michaelfinneran) · [MRFinneran@gmail.com](mailto:MRFinneran@gmail.com)
