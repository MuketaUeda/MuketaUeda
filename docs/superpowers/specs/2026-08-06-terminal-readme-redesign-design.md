# README redesign — terminal/dev-log style

## Context

The current `README.md` (this repo doubles as the GitHub profile page for
`MuketaUeda`) is a straightforward Markdown page: header with badges, About
paragraph, Stack table, Featured Projects table, and a Stats section (GitHub
profile summary cards + snake contribution animation).

The user saw `Sharann-del/README.md` and liked its terminal/dev-log
aesthetic: a custom SVG header banner, numbered section tags ("01 — whoami",
"02 — ...") rendered as SVG, and several sections (whoami, ecosystem/system
map, projects, telemetry, timeline, experience, stack, footer) each rendered
as a bespoke SVG image with light/dark variants swapped via
`<picture><source media="(prefers-color-scheme: dark)">`.

The user wants that visual language adapted to their own README, but more
concise than the reference — not a 1:1 clone.

## Decisions (confirmed with user)

1. **Hybrid visual approach.** Full bespoke SVG-per-section (as in the
   reference) is high effort and brittle to maintain — every content change
   (new project, new stack item) would require hand-editing an SVG. Instead:
   - SVG is used only for the "chrome": the header banner and the numbered
     section-label tags.
   - Actual content (about text, projects table, stack table, stats images)
     stays as normal Markdown/HTML, styled to read as a dark terminal
     (monospace headings, thin dividers, monochrome badges).

2. **4 numbered sections**, down from the reference's 6:
   - `01 — whoami` (About)
   - `02 — projects` (Featured Projects)
   - `03 — stack` (Tech stack)
   - `04 — stats` (GitHub stats + snake animation)

   Cut relative to the reference: the "ecosystem/system map" diagram and a
   separate "timeline" section. Professional experience stays folded into
   the `whoami` paragraph, as it already is today.

3. **Strict monochrome palette** — black/white only, no accent color,
   matching the reference. Light/dark variants swap via `<picture>`.

4. **Projects section**: keep all 6 existing projects, but shorten each
   description to a single direct line (current descriptions are 1-2
   sentences).

## Content per section

### Header
- Name: "Gabriel Rosati"
- Tagline: "AI Engineer · Cofounder @ Urutaus Tech · CS @ USP"
- Badges (monochrome pill style, light/dark swapped): LinkedIn, Portfolio,
  Email — same 3 links as today, restyled to match the reference's
  monochrome badge look (dark badge background flips light/dark).

### 01 — whoami
Single tight paragraph (~3 lines): AI Engineer, cofounder at Urutaus Tech
(customer-facing AI agents + AI-adoption consulting for a PE firm),
previously 4flow/Accenture/The Mome. CS student at USP with a Granada
exchange semester. OCI Generative AI Professional + OCI AI Foundations
Associate certifications.

### 02 — projects
Same 6 projects as today (Ursão, MapeIA, Task Exception Prediction, Playing
Card Classifier, IA-Addon, AboutME), same repo links and stack column,
descriptions shortened to one line each, e.g.:
- Ursão — The Big Bear: "RAG chatbot com Next.js + LangChain"
- MapeIA: "Mapeia projetos SAS e gera docs com GPT-4o"
- Task Exception Prediction: "Predição de exceções logísticas com XGBoost"
- Playing Card Classifier: "Classificador de imagens com PyTorch"
- IA-Addon: "Extensão Chrome que resume texto com IA"
- AboutME: "Portfólio pessoal em React + Vercel"

### 03 — stack
Same table structure as today (AI & Machine Learning, Full-Stack, Data &
Databases, Cloud & Infra, Tools), unchanged content, restyled to match the
terminal theme (monospace row labels).

### 04 — stats
Reuse existing images unchanged:
- `github-profile-summary-cards` stats + top-languages cards (from
  `.github/workflows/stats.yml`, `output` branch)
- Snake contribution animation (from `.github/workflows/snake.yml`,
  `output` branch)

### Footer
Repeat contact badges (LinkedIn, Portfolio, Email) + one closing terminal-
style status line, e.g. `$ status: open to interesting problems`.

## Section-label SVGs ("01 — whoami" etc.)

- Small banner, ~32px tall, full content width.
- Monospace text (`font-family="ui-monospace, SFMono-Regular, Menlo,
  Consolas, monospace"`), left-aligned, prefixed with the two-digit section
  number.
- Thin horizontal rule or left-side tick mark as the only decoration — no
  illustration — to keep these cheap to maintain and quick to re-theme.
- Two color variants per label: black-on-white (light) and white-on-black
  (dark), stored as `assets/s01-whoami.svg` / `assets/dark/s01-whoami.svg`
  (and equivalent for 02/03/04), matching the reference's asset naming
  convention.

## Header banner SVG

- Bordered box (1px monochrome rule), name in bold monospace, tagline
  below in regular weight, sized to span the content width used by the
  rest of the README.
- Two variants: `assets/header.svg` (light), `assets/dark/header.svg`
  (dark).

## Out of scope

- No animated telemetry graphic (reference's `telemetry.svg`) — the
  existing GitHub stats/snake images already cover this need.
- No ecosystem/system-map diagram.
- No separate timeline/experience section.
- No new GitHub Actions or asset-generation tooling — all SVGs are static
  files hand-authored once and committed directly; content changes (e.g.
  adding a 7th project) are plain Markdown edits and don't require
  regenerating any image.

## Files touched

- `README.md` — rewritten per the structure above.
- `assets/header.svg`, `assets/dark/header.svg` — new.
- `assets/s01-whoami.svg` … `assets/s04-stats.svg` and their `assets/dark/`
  counterparts — new (8 files total).
