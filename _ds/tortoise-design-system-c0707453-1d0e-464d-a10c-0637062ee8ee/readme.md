# Tortoise Design System

Tortoise lets employees pick any device they want — and save up to 40% on it — through a simple employer-enabled leasing benefit.

## Source

- Figma file: **"Design system for Claude Design.fig"** (attached, mounted read-only). One page, "Basics", with two sections: **Colors** (six 10-step ramps + core trio) and **Typography** (heading/body/label scales). It defines **no components, no product screens, no logo, and no imagery** — it is a foundations-only file.
- 52 Figma Variables were also extracted verbatim to `tokens/fig/fig-tokens.css` (generic amber/blue/gray/green/red ramps — these appear to be library defaults; the canvas swatch ramps are the real brand palette and are the primary system in `tokens/colors.css`).

## No logo

The source contains no logo or brand mark. Wherever a mark would go, render "tortoise" in the heading face (Haffer SQ XH SemiBold, lowercase). Do not draw one.

## CONTENT FUNDAMENTALS

The source file contains no product copy, so these rules are derived from the company's one-line proposition ("pick any device you want — and save up to 40%") and should be treated as provisional:

- Voice: plain, direct, benefit-first. Lead with what the employee gets ("Choose your device", "Save up to 40%").
- Second person ("you", "your device"); the employer is referenced in third person.
- Sentence case everywhere — headings, buttons, labels. No title case, no all-caps except short mono codes.
- Numbers stay numerals ("24 months", "£28/mo", "40%"). Money and terms may render in IBM Plex Mono for a data feel.
- No emoji.
- Wordmark renders lowercase: "tortoise".

## VISUAL FOUNDATIONS

- **Color:** white pages, ink text (#191919), and one working accent: green. Primary action/link green is `#167E62` (green-20); `#114036` (green-10) for dark brand surfaces; `#E6FFE6` (green-100) as a wash. Yellow, pink, coral and purple ramps are complementary — use as tints for badges, illustration and data, never as competing accents. Each ramp is 10 steps, 10 = darkest → 100 = lightest. Note: the gray ramp verbatim from the file repeats #4B4B4B at gray-50 and puts #EEEEEE before #E1E1E1 — kept as-is.
- **Type:** Haffer SQ XH SemiBold for all headings (14–32px scale); Inter for body (12/13/14/16/18px × regular/medium/semibold); IBM Plex Mono Medium for labels, token names, prices and codes. Body line-height 1.5.
- **Spacing:** 4px base scale (`--space-1…16`). *Intentional addition — the file defines no spacing variables.*
- **Radii:** 2px on large framing sections (observed in the file); 6px controls, 10px cards, 16px dialogs, pill for badges/tags. *Values above 2px are intentional additions.*
- **Borders & shadows:** hairline 1px borders (`rgba(0,0,0,0.1)` inset observed in the file); shadows are quiet — soft card shadow on hover, larger soft shadow only on overlays. No hard drop shadows.
- **Backgrounds:** flat color only. No gradients, no textures, no background imagery in the source.
- **Hover:** darken (primary → green-10) or subtle gray wash; focus = green border + 3px `--color-primary-tint` ring. Press: no scale effects.
- **Animation:** fast and functional — 120–200ms, `cubic-bezier(0.2,0,0,1)`; color/shadow transitions only, no bounces.
- **Transparency/blur:** only the dialog scrim (`rgba(25,25,25,0.45)`). No glassmorphism.
- **Imagery:** none in the source. Ask for real product photography before shipping imagery; do not generate placeholders styled as brand illustration.
- **Cards:** white, 1px `--border-default`, 10px radius, shadow only on hover/selection; selection = green border + tint ring.

## ICONOGRAPHY

The source contains **no icon set, no icon font, no emoji, and no unicode-as-icon usage**. Components that structurally need a glyph (select chevron, checkbox check, close ×, toast dot) use minimal 1.5px-stroke inline SVGs matching the hairline border language. For anything richer, use **Lucide** (CDN) at 1.5px stroke as the flagged substitute until Tortoise provides a set — document any icon you add.

## FONTS

- **Haffer SQ XH** SemiBold is self-hosted from `fonts/HafferSQXH-SemiBold.otf` (uploaded by the user); `@font-face` in `tokens/fonts.css`. Only weight 600 is available — headings use 600 exclusively.
- Inter and IBM Plex Mono load from Google Fonts.

## Intentional additions

The foundations-only source forced some inventions, all flagged:
- Spacing, radius (>2px), shadow, and motion tokens (`tokens/layout.css`).
- The entire component set (source defines zero components): Button, IconButton, Input, Select, Checkbox, Radio, Switch, Card, Badge, Tag, Tabs, Dialog, Toast, Tooltip — styled strictly from the token system.
- The demo screen in `ui_kits/device-picker/` is a demonstration, not a product recreation.

## Index

- `styles.css` — global entry (imports everything below)
- `tokens/colors.css` — brand ramps + semantic aliases
- `tokens/typography.css` — type tokens + `font-*` utility classes
- `tokens/fonts.css` — webfont loading (+ substitution note)
- `tokens/layout.css` — spacing/radius/shadow/motion + base resets
- `tokens/fig/fig-tokens.css` — 52 Figma Variables, verbatim
- `guidelines/*.card.html` — foundation specimen cards
- `components/actions/` — Button, IconButton
- `components/forms/` — Input, Select, Checkbox, Radio, Switch
- `components/display/` — Card, Badge, Tag, Tabs
- `components/feedback/` — Dialog, Toast, Tooltip
- `ui_kits/device-picker/` — interactive demo screen (disclaimer inside)
- `SKILL.md` — agent skill entry point
