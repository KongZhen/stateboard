# Stateboard GitHub Page Design System

English is canonical for this document. Chinese mirror: [page-design-system.zh.md](page-design-system.zh.md).

This design system captures the UI rules for `docs/index.html`, the static GitHub Page for Stateboard.

## Direction

The page uses a newspaper front-page model inspired by the current Washington Post homepage structure: editorial masthead, ruled navigation, multi-column story layout, right-rail briefing, compact tables, and high-contrast serif typography.

This is an original Stateboard page. Do not copy external logos, masthead lettering, article content, imagery, subscription UI, ads, or proprietary visual assets.

## Principles

- Stateboard is a project-state layer, not a generic todo assistant.
- The first viewport must show the masthead, one-line value proposition, `Copy prompt`, `View GitHub`, `Install skill`, a product board preview, and a get-started rail.
- Use newspaper density: strong rules, narrow gutters, clear columns, compact summaries, and tables.
- Keep the product claims bounded. Every integration claim must name a tier or runtime dependency.
- Keep the page static: no external fonts, frameworks, analytics, JavaScript, or remote image dependencies.
- Language switching is its own control group. Do not mix `EN / 中文 / 日本語 / 한국어 / ES` with utility links such as docs, roadmap, or GitHub.

## Tokens

### Typography

- Masthead: `Georgia`, `"Times New Roman"`, `Times`, `ui-serif`, `serif`.
- English body serif: `Georgia`, `"Times New Roman"`, `Times`, `ui-serif`, `serif`.
- Multilingual serif fallback: add `"Songti SC"`, `"STSong"`, `"Noto Serif CJK SC"`, `"Hiragino Mincho ProN"`, `"Yu Mincho"`, and `"Nanum Myeongjo"`.
- UI sans: system sans stack, with `PingFang SC`, `Microsoft YaHei`, `Hiragino Sans`, `Yu Gothic`, and `Apple SD Gothic Neo` for CJK pages.
- Monospace: `ui-monospace`, `SFMono-Regular`, `Menlo`, `Consolas`, `"Liberation Mono"`, `monospace`.
- Masthead sizes:
  - desktop: `168px`
  - medium: `138px`
  - tablet: `112px`
  - mobile: `66px`
  - narrow mobile: `58px`
- Do not use viewport-scaled font sizes or negative letter spacing.

### Color

- Canvas: `#f7f5ee`.
- Paper: `#fffdfa`.
- Ink / strong rule: `#111111`.
- Muted text: `#5d5a52`.
- Quiet text: `#7c776d`.
- Line: `#cac4b7`.
- Soft line: `#e3ded3`.
- Status green: `#15774f`.
- Status amber: `#b36812`.
- Status blue: `#2e638f`.

Accent color is reserved for status and tier meaning only. Avoid purple, indigo gradients, decorative blobs, soft SaaS cards, and generic AI styling.

## Layout

- Container: `min(1390px, calc(100% - 32px))`.
- Header stack:
  - dateline / utility row
  - oversized centered masthead
  - three-action rail
  - sticky section nav
- Topline groups:
  - left: edition state
  - center: short publication line
  - right: utility links and a separate language switcher
- Front page grid:
  - left lead story
  - center board preview
  - right get-started rail
- Secondary grid:
  - four compact brief columns for not-a-todo, workflow, quickstart, integration tiers
- Quickstart:
  - dark monospace panel with horizontal scrolling
- Integration tiers:
  - editorial note plus table in a horizontally scrollable wrapper

## Components

### Language Switcher

- The switcher lives in `.language-switcher`, separated from `.utility-links` by a thin vertical rule.
- Supported public pages:
  - English: `index.html`
  - Simplified Chinese: `index.zh.html`
  - Japanese: `index.ja.html`
  - Korean: `index.ko.html`
  - Spanish: `index.es.html`
- Mark the current language with `aria-current="page"`.
- Each language page must include `hreflang` alternates for all five languages and `x-default`.

### Action Rail

- Always expose `Copy prompt`, `View GitHub`, and `Install skill`.
- Use code-native SVG icons from the Tabler Icons visual model: 24x24 viewBox, no fill, `stroke: currentColor`, `stroke-width: 2`, round caps and joins.
- Links are black, centered, and separated by vertical rules.
- On mobile, stack into three full-width rows.

### Board Preview

- The board is the central product artifact, not decoration.
- Use compact ledger tables for active projects, evidence, next actions, and sync boundary.
- Rows should demonstrate evidence-first judgment, one project with bounded actions, and tiered sync boundaries.
- Mobile behavior: the board may horizontally scroll inside its frame; the whole page must not overflow.

### Right Rail

- Use newspaper briefing items for `Prompt entry`, `Codex skill`, `Markdown fallback`, and `Planned adapters`.
- Each item has one square icon box, a short serif title, one compact paragraph, and one link.

### Quickstart Prompt

- Keep the actual prompt copy visible and copy-ready.
- Use a dark monospace code panel.
- Preserve prompt formatting with `white-space: pre` and allow horizontal scroll.
- Do not claim automation will be created unless frequency and exact time are confirmed.

### Integration Tiers

- Describe `Current`, `Tier 1`, `Tier 2`, and `Tier 3/4`.
- Distinguish task sync, calendar sync, notification delivery, and fallback export.
- Do not write broad platform support claims.

## Responsiveness

- Verify `390px`, `768px`, and `1440px`.
- The masthead must stay readable and not collide with page edges.
- The masthead subhead uses a wider balanced text measure so Chinese, Japanese, Korean, and Spanish do not collapse into single-character or one-word lines.
- Chinese, Japanese, and Korean short UI headings use `word-break: keep-all`, `line-break: strict`, and `text-wrap: balance`; masthead subheads and long story headlines must keep natural CJK wrapping so they do not clip on narrow screens.
- Spanish prose uses `hyphens: auto` for long words.
- Section nav can scroll horizontally on small screens.
- Tables and prompt blocks can scroll horizontally inside their own containers.
- Normal prose must wrap without overflowing.
- Right rail collapses from side rail to two columns and then one column.
- Secondary brief grid collapses from four columns to two and then one.

## Implementation Rules

- Source files:
  - `docs/index.html`
  - `docs/index.zh.html`
  - `docs/index.ja.html`
  - `docs/index.ko.html`
  - `docs/index.es.html`
  - `docs/page-design-system.md`
  - `docs/page-design-system.zh.md`
- English page is canonical; Chinese page mirrors structure and behavior.
- Japanese, Korean, and Spanish pages mirror the same layout and must keep localized reading rhythm rather than inheriting English line-break behavior blindly.
- Keep HTML/CSS self-contained in each page.
- If visual tokens or component rules change, update this design system and the Chinese mirror in the same change.

## Review Checklist

- Masthead and ruled navigation read as an editorial newspaper page.
- First viewport includes all three action links and a product board preview.
- Language switcher is visually grouped separately from docs / roadmap / GitHub.
- The page avoids generic SaaS cards, gradients, blobs, and over-rounded UI.
- Icons share the same 24px/2px stroke visual system.
- The board preview communicates evidence, priority, next action, and sync boundary.
- Integration claims stay tiered and bounded.
- Code block and tables do not force whole-page horizontal overflow.
- Chinese, Japanese, Korean, and Spanish pages do not produce awkward single-character or single-word line breaks in hero/subhead copy.
- `git diff --check` passes.
