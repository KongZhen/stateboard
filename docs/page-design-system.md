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
- Keep the page static: no external fonts, frameworks, analytics, or remote image dependencies. The only allowed JavaScript is the small inline clipboard handler for the quickstart prompt.
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
- CJK UI labels use lighter sans weights than English labels when needed. Avoid faux-heavy rendering that makes Chinese, Japanese, or Korean text look blurred.

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
- Skill install:
  - full-width in-page install module directly after quickstart
  - light command panels with copy buttons for install and run commands
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
- Use code-native SVG icons from an open-source outline set. The right rail uses Heroicons-style 24x24 outline glyphs, no fill, `stroke: currentColor`, and round caps and joins.
- Links are black, centered, and separated by vertical rules. Do not add a bottom double rule under this rail.
- `Install skill` must link to the in-page `#skill-install` module, not to the small right-rail item and not directly to GitHub.
- On mobile, stack into three full-width rows.

### Board Preview

- The board is the central product artifact, not decoration.
- Use compact ledger tables for active projects, evidence, next actions, and sync boundary.
- Rows should demonstrate evidence-first judgment, one project with bounded actions, and tiered sync boundaries.
- Mobile behavior: the board may horizontally scroll inside its frame; the whole page must not overflow.

### Right Rail

- Use newspaper briefing items for `Prompt entry`, `Skill`, `Markdown fallback`, and `Planned adapters`.
- Each item has one unboxed stroke icon, a short serif title, one compact paragraph, and one link.
- Do not label the installable workflow as `Codex skill`; the public-facing name is `Skill` so Claude and other AI-assistant users do not read it as Codex-only.
- The right-rail `Skill` link also points to `#skill-install`.

### Quickstart Prompt

- Keep the actual prompt copy visible and copy-ready.
- The prompt header must use a real `<button>` that copies the visible prompt text in one click; do not use a passive `copy-ready` label.
- Use a dark monospace code panel.
- Preserve prompt formatting with `white-space: pre` and allow horizontal scroll.
- Do not claim automation will be created unless frequency and exact time are confirmed.

### Skill Install

- Place the module immediately below the quickstart prompt.
- Show install instructions on the page; do not require the user to open GitHub to learn how to install.
- Include a copyable install command:
  - `git clone https://github.com/KongZhen/stateboard.git`
  - `mkdir -p ~/.codex/skills/stateboard-codex`
  - `cp -R stateboard/skills/stateboard-codex/. ~/.codex/skills/stateboard-codex/`
- Include a copyable usage command: `$stateboard-codex`.
- Explain that the user still provides the four fields: what to organize, destination, target location, and automatic refresh.

### Integration Tiers

- Describe `Current`, `Tier 1`, `Tier 2`, and `Tier 3/4`.
- Distinguish task sync, calendar sync, notification delivery, and fallback export.
- Do not write broad platform support claims.

## Responsiveness

- Verify `390px`, `768px`, and `1440px`.
- The masthead must stay readable and not collide with page edges.
- The masthead subhead uses a wider balanced text measure so Chinese, Japanese, Korean, and Spanish do not collapse into single-character or one-word lines.
- Chinese, Japanese, and Korean long story headlines and prose must wrap inside their own column with `overflow-wrap: anywhere`, `word-break: normal`, and `line-break: strict`. Do not use `keep-all` on long CJK copy; it causes cross-column overlap on desktop and clipped text on narrow screens.
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
  - `prompts/stateboard-sync-prompt.md`
  - `prompts/stateboard-sync-prompt.zh.md`
  - `prompts/stateboard-sync-prompt.ja.md`
  - `prompts/stateboard-sync-prompt.ko.md`
  - `prompts/stateboard-sync-prompt.es.md`
  - `docs/prompts/stateboard-sync-prompt.md`
  - `docs/prompts/stateboard-sync-prompt.zh.md`
  - `docs/prompts/stateboard-sync-prompt.ja.md`
  - `docs/prompts/stateboard-sync-prompt.ko.md`
  - `docs/prompts/stateboard-sync-prompt.es.md`
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
- Right-rail icons are unboxed; the action rail has no bottom double rule.
- The board preview communicates evidence, priority, next action, and sync boundary.
- Integration claims stay tiered and bounded.
- Code block and tables do not force whole-page horizontal overflow.
- Copy buttons copy the same prompt text that is visible in each language page.
- The top `Install skill` CTA and right-rail `Skill` link land on an in-page install module with copyable commands.
- Chinese, Japanese, Korean, and Spanish pages do not produce awkward single-character or single-word line breaks in hero/subhead copy, and no story, rail, or table text crosses its column boundary.
- `git diff --check` passes.
