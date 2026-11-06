---
name: stardip-design-system
description: The StarDip design system foundation — color, typography, spacing, radius, elevation and focus tokens as CSS variables, plus the rules for using them. Use this skill for ANY UI work in a StarDip project — building or editing components, pages, layouts, styles, CSS, themes, dark mode, or reviewing UI code — even when the request doesn't mention the design system, tokens or StarDip by name. Also use it when choosing a color, font size, spacing value, corner radius or shadow, when fixing contrast or accessibility issues, or when converting a design or mockup to code.
---

# StarDip design system

StarDip's foundation is one CSS file of custom properties (`stardip-foundation.css`, reproduced in full in **Appendix A**). Every visual decision in product code resolves to one of those variables. This skill tells you which variable to use, how to apply it, and how to check your work.

Brand at a glance: **indigo** primary (`#161E85`), **green** secondary, **gold** accent, **paper** — an indigo-tinted neutral used for every surface, border and line of text. Display and headings are set in **Petrona** (serif), everything else in **Urbanist** (sans).

---

## Workflow

Follow these steps for every UI task.

1. **Find the tokens file.** Search the project for `stardip-foundation.css` or the string `--color-indigo-900`. If it is missing, create it from Appendix A (default path `src/styles/stardip-foundation.css`), import it once at the app root before any other styles, and load the fonts (see *Setup*).
2. **Classify each element** — page, surface, text, action, status, accent — and pick tokens with the *Decision guide*. Use the *Recipes* when building a common component.
3. **Write code with layer 2 and layer 3 tokens only** (semantic colors and scales). Never write a hex value, a raw px font size, an ad-hoc shadow or a primitive `--color-*` variable in component code.
4. **Run the verification checklist** at the end of this file before you finish.
5. **Report** which tokens you used if the change is non-trivial, and flag any value the system could not express (see *When no token fits*). Do not invent values silently.

---

## The rules

1. **Components use semantic tokens and scales only.** `--color-*` primitives exist to build tokens; a component that references `--color-indigo-900` is a bug. Use `--action` or `--accent` instead.
2. **No hard-coded values** for anything the system defines: colors, font sizes, font weights, line-heights, letter-spacing, spacing, radius, shadows.
3. **Every fill has an `--on-*` partner.** Text or icons placed on a fill use the token named after that fill: `--action` → `--on-action`, `--success-soft` → `--on-success-soft`, `--accent` → `--on-accent`. Never put `--text` on a colored fill.
4. **A type style is five properties applied together:** family, size, weight, line-height, letter-spacing. Never mix the size of one style with the weight of another.
5. **Radius encodes category, not size.** `--radius-full` means *pressable*. Cards are `--radius-md`; inputs are `--radius-x-sm`; floating layers are `--radius-lg`.
6. **Elevation encodes height.** Pick the shadow by what the element is (resting control, card, dropdown, modal), not by how it looks.
7. **Focus is always visible:** `box-shadow: var(--focus-ring); outline: 2px solid transparent;` on `:focus-visible`. Never `outline: none` without this replacement.
8. **Both modes are automatic.** Color tokens already carry light and dark values. Never write `@media (prefers-color-scheme: dark)` or `[data-theme="dark"]` overrides for individual components.
9. **Gold is never text.** `--accent-tertiary` is for fills and icons only.

---

## Token layers

| Layer | Pattern | Example | Who uses it |
|---|---|---|---|
| 1 · Primitive | `--color-{hue}-{step}` | `--color-indigo-900` | Only the tokens file |
| 2 · Semantic color | `--{role}[-{variant}][-{state}]` | `--action-secondary-hover` | Components |
| 2 · Text on fill | `--on-{fill}` | `--on-success-soft` | Components |
| 3 · Font family | `--font-{family}` | `--font-display` | Components |
| 3 · Type style | `--{style}-{property}` | `--heading-2-font-size` | Components |
| 3 · Spacing | `--space-{n}` · `--space-{role}` | `--space-5`, `--space-gutter` | Components |
| 3 · Radius | `--radius-{size}` | `--radius-full` | Components |
| 3 · Elevation | `--shadow-{size}` · `--focus-ring` | `--shadow-md` | Components |

Primitive ramps run 50–950 in eleven steps (50, 100, 200 … 900, 950); there are no other steps. Ramps: `indigo`, `green`, `gold`, `paper` (brand and neutral) and `leaf`, `yellow`, `red`, `blue` (status: success, caution, danger, info).

**Modes:** light by default, dark through `prefers-color-scheme`, forced with `data-theme="light"` or `data-theme="dark"` on `<html>`. Colors switch through `light-dark()`; shadows switch through an override block. Components need do nothing.

---

## Semantic color tokens

Light and dark columns name the primitive each token resolves to.

**Backgrounds and surfaces**

| Token | Light | Dark | Use for |
|---|---|---|---|
| `--paper` | paper-100 | paper-900 | The page. |
| `--paper-sunken` | paper-200 | paper-950 | Recessed ground: table headers, code bars, the well behind a card. |
| `--surface` | paper-50 | paper-800 | Cards, panels, inputs. |
| `--surface-raised` | paper-50 | paper-700 | A surface stacked on another surface: menus, popovers, modals. Pair with a shadow in light mode. |
| `--surface-hover` | paper-100 | paper-700 | Row and list-item hover. |
| `--surface-selected` | indigo-50 | indigo-950 | Selected row, active nav item. |
| `--surface-inverse` | paper-900 | paper-50 | Tooltips and toasts that flip against the mode. |

**Strokes**

| Token | Light | Dark | Use for |
|---|---|---|---|
| `--border` | paper-200 | paper-700 | Default card, input and divider stroke. |
| `--border-subtle` | paper-100 | paper-800 | Dividers inside a surface. |
| `--border-strong` | paper-500 | paper-500 | Input stroke and controls that must meet 3:1. |
| `--border-focus` | indigo-700 | indigo-300 | Focus ring. |
| `--border-selected` | indigo-900 | indigo-400 | Selected card or option. |

**Text**

| Token | Light | Dark | Use for |
|---|---|---|---|
| `--text` | paper-950 | paper-50 | Body and headings. |
| `--text-muted` | paper-700 | paper-300 | Secondary text, descriptions. |
| `--text-subtle` | paper-600 | paper-400 | Captions, placeholders, metadata. |
| `--text-disabled` | paper-400 | paper-600 |  |
| `--text-link` | indigo-700 | indigo-300 |  |
| `--text-link-hover` | indigo-900 | indigo-200 |  |

**Action**

| Token | Light | Dark | Use for |
|---|---|---|---|
| `--action` | indigo-900 | indigo-400 | Primary button fill. |
| `--action-hover` | indigo-800 | indigo-300 |  |
| `--action-pressed` | indigo-950 | indigo-200 |  |
| `--action-secondary` | paper-200 | paper-700 | Secondary button fill. |
| `--action-secondary-hover` | paper-300 | paper-600 |  |
| `--action-danger` | red-700 | red-400 | Destructive button fill. |
| `--action-danger-hover` | red-800 | red-300 |  |
| `--action-disabled` | paper-200 | paper-700 |  |

**Text on actions**

| Token | Light | Dark | Use for |
|---|---|---|---|
| `--on-action` | paper-50 | indigo-950 | Label on --action. |
| `--on-action-secondary` | paper-950 | paper-50 | Label on --action-secondary. |
| `--on-action-danger` | paper-50 | red-950 | Label on --action-danger. |
| `--on-action-disabled` | paper-500 | paper-400 | Label on --action-disabled. |

**Text on fills**

| Token | Light | Dark | Use for |
|---|---|---|---|
| `--on-accent` | paper-50 | indigo-950 | Text on an --accent fill: hero, brand band. |
| `--on-accent-secondary` | paper-50 | green-950 | Text on an --accent-secondary fill. Large or bold text only in light mode. |
| `--on-accent-tertiary` | gold-950 | gold-950 | Text on gold. Dark in both modes; white fails on gold. |
| `--on-inverse` | paper-50 | paper-950 | Text on --surface-inverse. |

**Accent**

| Token | Light | Dark | Use for |
|---|---|---|---|
| `--accent` | indigo-900 | indigo-400 | Brand indigo for non-interactive moments: hero, illustration, badges. |
| `--accent-soft` | indigo-50 | indigo-950 |  |
| `--accent-soft-border` | indigo-200 | indigo-800 |  |
| `--accent-secondary` | green-600 | green-400 | Brand green. |
| `--accent-secondary-soft` | green-50 | green-950 |  |
| `--accent-tertiary` | gold-400 | gold-300 | Brand gold. Fills and icons only, never text. |
| `--accent-tertiary-soft` | gold-50 | gold-950 |  |

**Status**

| Token | Light | Dark | Use for |
|---|---|---|---|
| `--success` | leaf-700 | leaf-400 | Icon, text and solid fill. |
| `--on-success` | paper-50 | leaf-950 | Text on a solid --success fill. |
| `--success-soft` | leaf-50 | leaf-950 | Banner fill. |
| `--success-soft-border` | leaf-200 | leaf-800 |  |
| `--on-success-soft` | leaf-800 | leaf-200 | Text on --success-soft. |
| `--caution` | yellow-700 | yellow-400 |  |
| `--on-caution` | paper-50 | yellow-950 |  |
| `--caution-soft` | yellow-50 | yellow-950 |  |
| `--caution-soft-border` | yellow-200 | yellow-800 |  |
| `--on-caution-soft` | yellow-800 | yellow-200 |  |
| `--danger` | red-700 | red-400 |  |
| `--on-danger` | paper-50 | red-950 |  |
| `--danger-soft` | red-50 | red-950 |  |
| `--danger-soft-border` | red-200 | red-800 |  |
| `--on-danger-soft` | red-800 | red-200 |  |
| `--info` | blue-700 | blue-400 |  |
| `--on-info` | paper-50 | blue-950 |  |
| `--info-soft` | blue-50 | blue-950 |  |
| `--info-soft-border` | blue-200 | blue-800 |  |
| `--on-info-soft` | blue-800 | blue-200 |  |

---

## Typography

Families: `--font-display` = Petrona (display and headings), `--font-body` = Urbanist (everything else).

Every style below exposes five variables: `--{style}-font-family`, `-font-size`, `-font-weight`, `-line-height`, `-letter-spacing`. Fluid sizes interpolate between 428px and 1280px viewports with `clamp()`.

| Style | Family | Size | Weight | Line-height | Tracking | Use for |
|---|---|---|---|---|---|---|
| `--display` | display | 48–64px fluid | 600 | 1 | −0.02em | Hero statement, one per view |
| `--heading-1` | display | 44–56px fluid | 600 | 1.1 | −0.02em | Page title |
| `--heading-2` | display | 36–44px fluid | 600 | 1.15 | −0.015em | Major section |
| `--heading-3` | display | 28–36px fluid | 600 | 1.2 | −0.01em | Subsection |
| `--heading-4` | display | 24–28px fluid | 600 | 1.25 | −0.005em | Card and panel titles |
| `--heading-5` | display | 18–20px fluid | 600 | 1.35 | 0 | Dialog titles, small panel headers |
| `--heading-6` | display | 16px | 600 | 1.45 | 0 | Group titles in dense UI |
| `--body-large-{regular,medium,bold}` | body | 18–20px fluid | 400 / 500 / 700 | 1.5 | 0 | Lead paragraphs, intros |
| `--body-medium-{regular,medium,bold}` | body | 16px | 400 / 500 / 700 | 1.5 | 0 | Default reading text |
| `--body-small-{regular,medium,bold}` | body | 14px | 400 / 500 / 700 | 1.5 | 0 | Dense UI, tables, secondary content |
| `--caption` | body | 14px | 500 | 1.5 | +0.005em | Image captions, helper text (pair with `--text-subtle`) |
| `--label-semibold` | body | 14px | 600 | 1.5 | +0.01em | Buttons, tabs, chips — labels that act |
| `--label-medium` | body | 14px | 500 | 1.5 | +0.01em | Field labels, table headers — labels that name |
| `--footnote` | body | 12px | 400 | 1.5 | +0.02em | Fine print, timestamps, legal |

Weight choice inside body: **regular** for running text, **medium** for emphasis and UI copy, **bold** for strong emphasis and key figures.

Apply a style with a class that sets all five properties. If the project has no type classes yet, add them once next to the tokens file:

```css
.text-heading-1 {
  font-family: var(--heading-1-font-family);
  font-size: var(--heading-1-font-size);
  font-weight: var(--heading-1-font-weight);
  line-height: var(--heading-1-line-height);
  letter-spacing: var(--heading-1-letter-spacing);
}
/* Repeat for every style: .text-display, .text-heading-2 … .text-body-medium-regular … .text-footnote */
```

Semantic HTML first: use `<h1>`–`<h6>` for document structure and pick the type style for its visual role; they do not have to match one to one.

---

## Spacing

| Token | Value | | Token | Value |
|---|---|---|---|---|
| `--space-1` | 4px | | `--space-6` | 32px |
| `--space-2` | 8px | | `--space-7` | 48px |
| `--space-3` | 12px | | `--space-8` | 64px |
| `--space-4` | 16px | | `--space-9` | 96px |
| `--space-5` | 24px | | `--space-10` | 128px |

| Fluid token | 428px → 1280px | Use for |
|---|---|---|
| `--space-section` | 48 → 96px | Vertical gap between page sections |
| `--space-page-margin` | 16 → 80px | Left/right page margin, viewport edge to content |
| `--space-gutter` | 16 → 32px | Gap between grid columns |

Defaults: inside a control `--space-2`–`--space-3`; inside a card `--space-5`; between related items `--space-2`–`--space-4`; between groups `--space-6`–`--space-7`.

---

## Radius

| Token | Value | Use for |
|---|---|---|
| `--radius-none` | 0 | Swatches and color chips |
| `--radius-2x-sm` | 2px | Inline marks, focus outlines, checkboxes, small indicators |
| `--radius-x-sm` | 4px | Inputs, tags, code blocks, tooltips |
| `--radius-sm` | 8px | Compact containers: menu items, list rows, segmented controls, small cards |
| `--radius-md` | 12px | Cards, panels, tables |
| `--radius-lg` | 16px | Modals, popovers, menus, toasts |
| `--radius-xl` | 20px | Thumbnails, previews, media |
| `--radius-2-xl` | 28px | Sheets, full-width panels on small screens |
| `--radius-3xl` | 32px | Feature cards, promotional banners |
| `--radius-4xl` | 44px | Hero media, onboarding and empty-state illustrations |
| `--radius-full` | 999px | Anything pressable: buttons, pills, toggles |

---

## Elevation and focus

| Token | Use for |
|---|---|
| `--shadow-x-sm` | Resting controls: buttons, inputs, toggles |
| `--shadow-sm` | Cards and panels at rest |
| `--shadow-md` | Hovered cards, dropdowns, popovers, sticky headers |
| `--shadow-lg` | Modals, dialogs, drawers |
| `--focus-ring` | Keyboard focus on every interactive element |

Shadows are tinted with paper-950 and indigo-950, never black. Raise elevation one step on hover (`--shadow-sm` → `--shadow-md`); do not skip steps.

---

## Decision guide

| You are styling… | Background | Text / icon | Border | Radius | Shadow |
|---|---|---|---|---|---|
| Page | `--paper` | `--text` | — | — | — |
| Recessed area (table header, code bar) | `--paper-sunken` | `--text-muted` | — | — | — |
| Card / panel | `--surface` | `--text`, `--text-muted` | `--border` | `--radius-md` | `--shadow-sm` |
| Menu / popover / modal | `--surface-raised` | `--text` | `--border` | `--radius-lg` | `--shadow-md` / `--shadow-lg` |
| Primary button | `--action` → `-hover` → `-pressed` | `--on-action` | — | `--radius-full` | `--shadow-x-sm` |
| Secondary button | `--action-secondary` | `--on-action-secondary` | — | `--radius-full` | — |
| Destructive button | `--action-danger` | `--on-action-danger` | — | `--radius-full` | `--shadow-x-sm` |
| Disabled control | `--action-disabled` | `--on-action-disabled` | — | as enabled | none |
| Text input | `--surface` | `--text`; placeholder `--text-subtle` | `--border-strong`; focus `--border-focus` | `--radius-x-sm` | — |
| Link | — | `--text-link` → `--text-link-hover` | — | — | — |
| Selected row / nav item | `--surface-selected` | `--text` | `--border-selected` | — | — |
| Tooltip / toast | `--surface-inverse` | `--on-inverse` | — | `--radius-x-sm` / `--radius-lg` | `--shadow-md` |
| Status banner | `--{status}-soft` | `--on-{status}-soft`; icon `--{status}` | `--{status}-soft-border` | `--radius-md` | — |
| Solid status badge | `--{status}` | `--on-{status}` | — | `--radius-full` | — |
| Brand band / hero | `--accent` | `--on-accent` | — | — | — |

`{status}` is one of `success`, `caution`, `danger`, `info`.

---

## Recipes

```css
.button {
  display: inline-flex; align-items: center; gap: var(--space-2);
  padding: var(--space-3) var(--space-5);
  border: 0; border-radius: var(--radius-full);
  font-family: var(--label-semibold-font-family);
  font-size: var(--label-semibold-font-size);
  font-weight: var(--label-semibold-font-weight);
  line-height: var(--label-semibold-line-height);
  letter-spacing: var(--label-semibold-letter-spacing);
  background: var(--action); color: var(--on-action);
  box-shadow: var(--shadow-x-sm);
  cursor: pointer;
}
.button:hover   { background: var(--action-hover); }
.button:active  { background: var(--action-pressed); }
.button:focus-visible { box-shadow: var(--focus-ring); outline: 2px solid transparent; }
.button:disabled { background: var(--action-disabled); color: var(--on-action-disabled); box-shadow: none; cursor: not-allowed; }

.button--secondary { background: var(--action-secondary); color: var(--on-action-secondary); box-shadow: none; }
.button--secondary:hover { background: var(--action-secondary-hover); }
.button--danger { background: var(--action-danger); color: var(--on-action-danger); }
.button--danger:hover { background: var(--action-danger-hover); }

.card {
  background: var(--surface); color: var(--text);
  border: 1px solid var(--border); border-radius: var(--radius-md);
  padding: var(--space-5); box-shadow: var(--shadow-sm);
}

.input {
  background: var(--surface); color: var(--text);
  border: 1px solid var(--border-strong); border-radius: var(--radius-x-sm);
  padding: var(--space-3) var(--space-4);
  font-family: var(--body-medium-regular-font-family);
  font-size: var(--body-medium-regular-font-size);
  line-height: var(--body-medium-regular-line-height);
}
.input::placeholder { color: var(--text-subtle); }
.input:focus-visible { border-color: var(--border-focus); box-shadow: var(--focus-ring); outline: 2px solid transparent; }
.input[aria-invalid="true"] { border-color: var(--danger); }

.banner--success {
  background: var(--success-soft); color: var(--on-success-soft);
  border: 1px solid var(--success-soft-border); border-radius: var(--radius-md);
  padding: var(--space-4) var(--space-5);
}
.banner--success .icon { color: var(--success); }

.modal {
  background: var(--surface-raised); color: var(--text);
  border-radius: var(--radius-lg); box-shadow: var(--shadow-lg);
  padding: var(--space-6);
}

.page {
  background: var(--paper); color: var(--text);
  padding-inline: var(--space-page-margin);
}
.page > section + section { margin-top: var(--space-section); }
.grid { display: grid; gap: var(--space-gutter); }
```

---

## Using the tokens in frameworks

**Plain CSS, CSS Modules, Sass, Vue/Svelte `<style>`:** use `var(--token)` directly, as in the recipes.

**React inline styles / CSS-in-JS:** pass the variable as a string — `style={{ background: "var(--surface)" }}`. Never copy the resolved hex into JS.

**No utility-CSS frameworks.** This project does not use Tailwind or any other utility-class framework. Do not install one or build single-property utility classes (`.p-4`, `.bg-indigo`); style components with CSS that references the tokens. The type-style classes in *Typography* are the one exception, because each applies a complete token set.

---

## Accessibility contract

- All `--text*`, `--text-link`, `--on-*` and status pairings pass WCAG AA (4.5:1) on their intended background in both modes, **with one exception:** `--on-accent-secondary` on `--accent-secondary` in light mode is 4.1:1 — use it only for text ≥ 18.66px bold or ≥ 24px regular.
- `--text-disabled` and `--on-action-disabled` are intentionally low contrast; never use them for meaningful content.
- `--border-strong` meets 3:1 for input and control boundaries; `--border` and `--border-subtle` are decorative only.
- Never use color alone to convey status: pair `--{status}` with an icon or text.
- Every interactive element must show `--focus-ring` on `:focus-visible`.
- Respect `prefers-reduced-motion` for any transition you add.

---

## When no token fits

Do not hard-code a value and do not repurpose a token with the wrong meaning. Instead:

1. Check whether an existing token covers the job under a different name (the *Decision guide* and the descriptions in Appendix A).
2. If not, propose a new semantic token that follows the layer pattern, maps to a primitive for **both** modes, and stays inside the 50–950 ramps. Example: `--surface-highlight: light-dark(var(--color-gold-50), var(--color-gold-950));  /* Highlighted search result */`
3. Add it to the tokens file in the right group with a one-line comment, and tell the human you added it so it can be reviewed. Never add new primitive steps (no 25, 925, 975) and never add pure white or black.

---

## Verification checklist

Run before finishing. Replace `src` with the project's source folder; exclude the tokens file itself.

```bash
# 1. Hard-coded colors (hex, rgb, hsl) outside the tokens file
grep -rEn "#[0-9a-fA-F]{3,8}\b|rgba?\(|hsla?\(" src --include=*.{css,scss,tsx,jsx,ts,js,vue,svelte,html} | grep -v stardip-foundation.css

# 2. Primitives used in components
grep -rEn "var\(--color-(indigo|green|gold|paper|leaf|yellow|red|blue)-[0-9]+" src | grep -v stardip-foundation.css

# 3. Raw font sizes, weights and shadows
grep -rEn "font-size:\s*[0-9]|font-weight:\s*[0-9]|box-shadow:\s*[0-9]" src | grep -v stardip-foundation.css

# 4. Focus removed without replacement
grep -rEn "outline:\s*(none|0)" src
```

Then confirm by reading the diff:

- [ ] Every color, size, space, radius and shadow is a `var(--…)` from layers 2–3.
- [ ] Every text-on-fill uses the matching `--on-*` token.
- [ ] Type styles set all five properties.
- [ ] Radius matches the element's category; pressable elements use `--radius-full`.
- [ ] Interactive elements have hover, active, `:focus-visible` and disabled states.
- [ ] Nothing was added that overrides tokens per mode.
- [ ] The UI was checked in light and dark mode (toggle `data-theme` on `<html>`).

---

## Setup

Load the fonts once (in `<head>` or your framework's font loader):

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Petrona:wght@600&family=Urbanist:wght@400;500;600;700&display=swap" rel="stylesheet">
```

Set the base on the root element:

```css
html { background: var(--paper); color: var(--text); }
body {
  font-family: var(--body-medium-regular-font-family);
  font-size: var(--body-medium-regular-font-size);
  line-height: var(--body-medium-regular-line-height);
}
```

---

## Appendix A · stardip-foundation.css

The complete tokens file. Write it to the project verbatim if it does not exist; never edit token values in component code.

```css
/*
 * StarDip design system · foundation tokens
 *
 * LAYERS
 *   1. Primitives   --color-*                     raw values. Build tokens from these; never use them in components.
 *   2. Semantic     --paper, --text, --action …    what components use. Each carries light and dark.
 *   3. Scales       type, space, radius, shadow   mode-independent, except shadows.
 *
 * RULES FOR PEOPLE AND AGENTS
 *   - Components reference layer 2 and 3 only. If a needed value has no semantic token, add one; do not reach for a primitive.
 *   - Never hard-code a hex, px size or shadow that exists here.
 *   - Every fill has an --on-* partner. Text on a fill uses that partner, nothing else.
 *   - A type style is five properties: family, size, weight, line-height, letter-spacing. Apply all five together.
 *   - Radius encodes category, not size: --radius-full means pressable.
 *   - Focus: box-shadow: var(--focus-ring); outline: 2px solid transparent;
 *
 * MODES   light by default, dark via prefers-color-scheme, forced with [data-theme="light"|"dark"] on <html>.
 * FLUID   clamp() values interpolate between 428px and 1280px viewports.
 */

:root {
  color-scheme: light dark;

  /* ── 1 PRIMITIVE COLOR ──────────────────────────────────────────── */
  /* indigo · brand primary · brand value at 900 */
  --color-indigo-50:  #f0f7ff;
  --color-indigo-100: #e1edff;
  --color-indigo-200: #cadbff;
  --color-indigo-300: #acc1f9;
  --color-indigo-400: #8da4e7;
  --color-indigo-500: #6f88d3;
  --color-indigo-600: #536cbf;
  --color-indigo-700: #3c53ad;
  --color-indigo-800: #27399a;
  --color-indigo-900: #161e85;
  --color-indigo-950: #060946;
  /* green · brand secondary · brand value at 600 */
  --color-green-50:  #edfbef;
  --color-green-100: #d8f7dd;
  --color-green-200: #bbeac4;
  --color-green-300: #97d5a4;
  --color-green-400: #70bd82;
  --color-green-500: #49a563;
  --color-green-600: #1b8c45;
  --color-green-700: #006f30;
  --color-green-800: #00531c;
  --color-green-900: #003908;
  --color-green-950: #001f00;
  /* gold · brand accent · brand value at 400 */
  --color-gold-50:  #fcf6e9;
  --color-gold-100: #fdebc5;
  --color-gold-200: #f4d89b;
  --color-gold-300: #e1bd6a;
  --color-gold-400: #c9a037;
  --color-gold-500: #a9831c;
  --color-gold-600: #8a6800;
  --color-gold-700: #6f5000;
  --color-gold-800: #543a00;
  --color-gold-900: #3a2600;
  --color-gold-950: #221300;
  /* paper · neutral · brand value at 50 */
  --color-paper-50:  #f7f9ff;
  --color-paper-100: #edf2ff;
  --color-paper-200: #dfe7fc;
  --color-paper-300: #cbd4ef;
  --color-paper-400: #98a4c5;
  --color-paper-500: #6e7b9f;
  --color-paper-600: #4d5a7c;
  --color-paper-700: #313b57;
  --color-paper-800: #222a42;
  --color-paper-900: #161d31;
  --color-paper-950: #0e1323;
  /* leaf · status · success · brand value at 600 */
  --color-leaf-50:  #effaf0;
  --color-leaf-100: #ddf6de;
  --color-leaf-200: #c4e9c6;
  --color-leaf-300: #a4d5a7;
  --color-leaf-400: #82be87;
  --color-leaf-500: #61a769;
  --color-leaf-600: #428f4d;
  --color-leaf-700: #2b7137;
  --color-leaf-800: #145421;
  --color-leaf-900: #00380c;
  --color-leaf-950: #001f00;
  /* yellow · status · caution · brand value at 400 */
  --color-yellow-50:  #fcf7e7;
  --color-yellow-100: #fbedc0;
  --color-yellow-200: #f2db91;
  --color-yellow-300: #dfc15b;
  --color-yellow-400: #c8a412;
  --color-yellow-500: #a88700;
  --color-yellow-600: #896b00;
  --color-yellow-700: #6c5300;
  --color-yellow-800: #513d00;
  --color-yellow-900: #372800;
  --color-yellow-950: #1f1400;
  /* red · status · danger · brand value at 700 */
  --color-red-50:  #fff2ed;
  --color-red-100: #ffe3db;
  --color-red-200: #ffcdc1;
  --color-red-300: #faafa1;
  --color-red-400: #e8907f;
  --color-red-500: #d4715f;
  --color-red-600: #be5240;
  --color-red-700: #a93625;
  --color-red-800: #811f11;
  --color-red-900: #5b0500;
  --color-red-950: #370000;
  /* blue · status · info · brand value at 500 */
  --color-blue-50:  #ebf9ff;
  --color-blue-100: #d2f0ff;
  --color-blue-200: #addeff;
  --color-blue-300: #7fc3ff;
  --color-blue-400: #4ea5ef;
  --color-blue-500: #1486d7;
  --color-blue-600: #006bb4;
  --color-blue-700: #005495;
  --color-blue-800: #003e77;
  --color-blue-900: #002959;
  --color-blue-950: #00153a;

  /* ── 2 SEMANTIC COLOR · light-dark(light, dark) ─────────────────── */
  /* Backgrounds and surfaces */
  --paper:            light-dark(var(--color-paper-100), var(--color-paper-900));
  --paper-sunken:     light-dark(var(--color-paper-200), var(--color-paper-950));
  --surface:          light-dark(var(--color-paper-50),  var(--color-paper-800));
  --surface-raised:   light-dark(var(--color-paper-50),  var(--color-paper-700));
  --surface-hover:    light-dark(var(--color-paper-100), var(--color-paper-700));
  --surface-selected: light-dark(var(--color-indigo-50), var(--color-indigo-950));
  --surface-inverse:  light-dark(var(--color-paper-900), var(--color-paper-50));
  /* Strokes */
  --border:          light-dark(var(--color-paper-200), var(--color-paper-700));
  --border-subtle:   light-dark(var(--color-paper-100), var(--color-paper-800));
  --border-strong:   light-dark(var(--color-paper-500), var(--color-paper-500));
  --border-focus:    light-dark(var(--color-indigo-700), var(--color-indigo-300));
  --border-selected: light-dark(var(--color-indigo-900), var(--color-indigo-400));
  /* Text */
  --text:            light-dark(var(--color-paper-950), var(--color-paper-50));
  --text-muted:      light-dark(var(--color-paper-700), var(--color-paper-300));
  --text-subtle:     light-dark(var(--color-paper-600), var(--color-paper-400));
  --text-disabled:   light-dark(var(--color-paper-400), var(--color-paper-600));
  --text-link:       light-dark(var(--color-indigo-700), var(--color-indigo-300));
  --text-link-hover: light-dark(var(--color-indigo-900), var(--color-indigo-200));
  /* Action */
  --action:                 light-dark(var(--color-indigo-900), var(--color-indigo-400));
  --action-hover:           light-dark(var(--color-indigo-800), var(--color-indigo-300));
  --action-pressed:         light-dark(var(--color-indigo-950), var(--color-indigo-200));
  --action-secondary:       light-dark(var(--color-paper-200),  var(--color-paper-700));
  --action-secondary-hover: light-dark(var(--color-paper-300),  var(--color-paper-600));
  --action-danger:          light-dark(var(--color-red-700),    var(--color-red-400));
  --action-danger-hover:    light-dark(var(--color-red-800),    var(--color-red-300));
  --action-disabled:        light-dark(var(--color-paper-200),  var(--color-paper-700));
  /* Text on actions */
  --on-action:           light-dark(var(--color-paper-50),   var(--color-indigo-950));
  --on-action-secondary: light-dark(var(--color-paper-950),  var(--color-paper-50));
  --on-action-danger:    light-dark(var(--color-paper-50),   var(--color-red-950));
  --on-action-disabled:  light-dark(var(--color-paper-500),  var(--color-paper-400));
  /* Text on fills */
  --on-accent:           light-dark(var(--color-paper-50),   var(--color-indigo-950));
  --on-accent-secondary: light-dark(var(--color-paper-50),   var(--color-green-950));
  --on-accent-tertiary:  light-dark(var(--color-gold-950),   var(--color-gold-950));
  --on-inverse:          light-dark(var(--color-paper-50),   var(--color-paper-950));
  /* Accent */
  --accent:                light-dark(var(--color-indigo-900), var(--color-indigo-400));
  --accent-soft:           light-dark(var(--color-indigo-50),  var(--color-indigo-950));
  --accent-soft-border:    light-dark(var(--color-indigo-200), var(--color-indigo-800));
  --accent-secondary:      light-dark(var(--color-green-600),  var(--color-green-400));
  --accent-secondary-soft: light-dark(var(--color-green-50),   var(--color-green-950));
  --accent-tertiary:       light-dark(var(--color-gold-400),   var(--color-gold-300));
  --accent-tertiary-soft:  light-dark(var(--color-gold-50),    var(--color-gold-950));
  /* Status */
  --success:             light-dark(var(--color-leaf-700),   var(--color-leaf-400));
  --on-success:          light-dark(var(--color-paper-50),   var(--color-leaf-950));
  --success-soft:        light-dark(var(--color-leaf-50),    var(--color-leaf-950));
  --success-soft-border: light-dark(var(--color-leaf-200),   var(--color-leaf-800));
  --on-success-soft:     light-dark(var(--color-leaf-800),   var(--color-leaf-200));
  --caution:             light-dark(var(--color-yellow-700), var(--color-yellow-400));
  --on-caution:          light-dark(var(--color-paper-50),   var(--color-yellow-950));
  --caution-soft:        light-dark(var(--color-yellow-50),  var(--color-yellow-950));
  --caution-soft-border: light-dark(var(--color-yellow-200), var(--color-yellow-800));
  --on-caution-soft:     light-dark(var(--color-yellow-800), var(--color-yellow-200));
  --danger:              light-dark(var(--color-red-700),    var(--color-red-400));
  --on-danger:           light-dark(var(--color-paper-50),   var(--color-red-950));
  --danger-soft:         light-dark(var(--color-red-50),     var(--color-red-950));
  --danger-soft-border:  light-dark(var(--color-red-200),    var(--color-red-800));
  --on-danger-soft:      light-dark(var(--color-red-800),    var(--color-red-200));
  --info:                light-dark(var(--color-blue-700),   var(--color-blue-400));
  --on-info:             light-dark(var(--color-paper-50),   var(--color-blue-950));
  --info-soft:           light-dark(var(--color-blue-50),    var(--color-blue-950));
  --info-soft-border:    light-dark(var(--color-blue-200),   var(--color-blue-800));
  --on-info-soft:        light-dark(var(--color-blue-800),   var(--color-blue-200));

  /* ── 3 TYPOGRAPHY ────────────────────────────────────────────────── */
  --font-display: 'Petrona', Georgia, 'Times New Roman', serif;
  --font-body:    'Urbanist', 'Segoe UI', system-ui, sans-serif;
  --display-font-family:    var(--font-display);
  --display-font-size:      clamp(3rem, 2.4977rem + 1.8779vw, 4rem);
  --display-font-weight:    600;
  --display-line-height:    1;
  --display-letter-spacing: -0.02em;
  --heading-1-font-family:    var(--font-display);
  --heading-1-font-size:      clamp(2.75rem, 2.3732rem + 1.4085vw, 3.5rem);
  --heading-1-font-weight:    600;
  --heading-1-line-height:    1.1;
  --heading-1-letter-spacing: -0.02em;
  --heading-2-font-family:    var(--font-display);
  --heading-2-font-size:      clamp(2.25rem, 1.9988rem + 0.939vw, 2.75rem);
  --heading-2-font-weight:    600;
  --heading-2-line-height:    1.15;
  --heading-2-letter-spacing: -0.015em;
  --heading-3-font-family:    var(--font-display);
  --heading-3-font-size:      clamp(1.75rem, 1.4988rem + 0.939vw, 2.25rem);
  --heading-3-font-weight:    600;
  --heading-3-line-height:    1.2;
  --heading-3-letter-spacing: -0.01em;
  --heading-4-font-family:    var(--font-display);
  --heading-4-font-size:      clamp(1.5rem, 1.3744rem + 0.4695vw, 1.75rem);
  --heading-4-font-weight:    600;
  --heading-4-line-height:    1.25;
  --heading-4-letter-spacing: -0.005em;
  --heading-5-font-family:    var(--font-display);
  --heading-5-font-size:      clamp(1.125rem, 1.0622rem + 0.2347vw, 1.25rem);
  --heading-5-font-weight:    600;
  --heading-5-line-height:    1.35;
  --heading-5-letter-spacing: 0;
  --heading-6-font-family:    var(--font-display);
  --heading-6-font-size:      1rem;
  --heading-6-font-weight:    600;
  --heading-6-line-height:    1.45;
  --heading-6-letter-spacing: 0;
  --body-large-regular-font-family:    var(--font-body);
  --body-large-regular-font-size:      clamp(1.125rem, 1.0622rem + 0.2347vw, 1.25rem);
  --body-large-regular-font-weight:    400;
  --body-large-regular-line-height:    1.5;
  --body-large-regular-letter-spacing: 0;
  --body-large-medium-font-family:    var(--font-body);
  --body-large-medium-font-size:      clamp(1.125rem, 1.0622rem + 0.2347vw, 1.25rem);
  --body-large-medium-font-weight:    500;
  --body-large-medium-line-height:    1.5;
  --body-large-medium-letter-spacing: 0;
  --body-large-bold-font-family:    var(--font-body);
  --body-large-bold-font-size:      clamp(1.125rem, 1.0622rem + 0.2347vw, 1.25rem);
  --body-large-bold-font-weight:    700;
  --body-large-bold-line-height:    1.5;
  --body-large-bold-letter-spacing: 0;
  --body-medium-regular-font-family:    var(--font-body);
  --body-medium-regular-font-size:      1rem;
  --body-medium-regular-font-weight:    400;
  --body-medium-regular-line-height:    1.5;
  --body-medium-regular-letter-spacing: 0;
  --body-medium-medium-font-family:    var(--font-body);
  --body-medium-medium-font-size:      1rem;
  --body-medium-medium-font-weight:    500;
  --body-medium-medium-line-height:    1.5;
  --body-medium-medium-letter-spacing: 0;
  --body-medium-bold-font-family:    var(--font-body);
  --body-medium-bold-font-size:      1rem;
  --body-medium-bold-font-weight:    700;
  --body-medium-bold-line-height:    1.5;
  --body-medium-bold-letter-spacing: 0;
  --body-small-regular-font-family:    var(--font-body);
  --body-small-regular-font-size:      0.875rem;
  --body-small-regular-font-weight:    400;
  --body-small-regular-line-height:    1.5;
  --body-small-regular-letter-spacing: 0;
  --body-small-medium-font-family:    var(--font-body);
  --body-small-medium-font-size:      0.875rem;
  --body-small-medium-font-weight:    500;
  --body-small-medium-line-height:    1.5;
  --body-small-medium-letter-spacing: 0;
  --body-small-bold-font-family:    var(--font-body);
  --body-small-bold-font-size:      0.875rem;
  --body-small-bold-font-weight:    700;
  --body-small-bold-line-height:    1.5;
  --body-small-bold-letter-spacing: 0;
  --caption-font-family:    var(--font-body);
  --caption-font-size:      0.875rem;
  --caption-font-weight:    500;
  --caption-line-height:    1.5;
  --caption-letter-spacing: 0.005em;
  --label-semibold-font-family:    var(--font-body);
  --label-semibold-font-size:      0.875rem;
  --label-semibold-font-weight:    600;
  --label-semibold-line-height:    1.5;
  --label-semibold-letter-spacing: 0.01em;
  --label-medium-font-family:    var(--font-body);
  --label-medium-font-size:      0.875rem;
  --label-medium-font-weight:    500;
  --label-medium-line-height:    1.5;
  --label-medium-letter-spacing: 0.01em;
  --footnote-font-family:    var(--font-body);
  --footnote-font-size:      0.75rem;
  --footnote-font-weight:    400;
  --footnote-line-height:    1.5;
  --footnote-letter-spacing: 0.02em;

  /* ── 4 SPACING ───────────────────────────────────────────────────── */
  --space-1:  0.25rem;
  --space-2:  0.5rem;
  --space-3:  0.75rem;
  --space-4:  1rem;
  --space-5:  1.5rem;
  --space-6:  2rem;
  --space-7:  3rem;
  --space-8:  4rem;
  --space-9:  6rem;
  --space-10: 8rem;
  --space-section:     clamp(3rem, 1.493rem + 5.6338vw, 6rem);
  --space-page-margin: clamp(1rem, -1.0094rem + 7.5117vw, 5rem);
  --space-gutter:      clamp(1rem, 0.4977rem + 1.8779vw, 2rem);

  /* ── 5 RADIUS ────────────────────────────────────────────────────── */
  --radius-none:  0px;
  --radius-2x-sm: 2px;
  --radius-x-sm:  4px;
  --radius-sm:    8px;
  --radius-md:    12px;
  --radius-lg:    16px;
  --radius-xl:    20px;
  --radius-2-xl:  28px;
  --radius-3xl:   32px;
  --radius-4xl:   44px;
  --radius-full:  999px;

  /* ── 6 ELEVATION ─────────────────────────────────────────────────── */
  --shadow-x-sm: 0 1px 2px rgba(14, 19, 35, 0.06), 0 1px 1px rgba(6, 9, 70, 0.04);
  --shadow-sm:   0 1px 3px rgba(14, 19, 35, 0.08), 0 2px 6px -1px rgba(6, 9, 70, 0.08);
  --shadow-md:   0 4px 8px -2px rgba(14, 19, 35, 0.08), 0 10px 20px -4px rgba(6, 9, 70, 0.12);
  --shadow-lg:   0 8px 16px -6px rgba(14, 19, 35, 0.10), 0 24px 48px -12px rgba(6, 9, 70, 0.22);
  --focus-ring: 0 0 0 2px var(--surface), 0 0 0 4px var(--border-focus);
}

/* Forced modes */
:root[data-theme="light"] { color-scheme: light; }
:root[data-theme="dark"]  { color-scheme: dark; }

/* Dark shadows */
@media (prefers-color-scheme: dark) {
  :root:not([data-theme="light"]) {
    --shadow-x-sm: 0 1px 2px rgba(14, 19, 35, 0.40), 0 1px 1px rgba(6, 9, 70, 0.30);
    --shadow-sm:   0 1px 3px rgba(14, 19, 35, 0.45), 0 2px 6px -1px rgba(6, 9, 70, 0.40);
    --shadow-md:   0 4px 8px -2px rgba(14, 19, 35, 0.50), 0 10px 20px -4px rgba(6, 9, 70, 0.50);
    --shadow-lg:   0 8px 16px -6px rgba(14, 19, 35, 0.55), 0 24px 48px -12px rgba(6, 9, 70, 0.65);
  }
}
:root[data-theme="dark"] {
  --shadow-x-sm: 0 1px 2px rgba(14, 19, 35, 0.40), 0 1px 1px rgba(6, 9, 70, 0.30);
  --shadow-sm:   0 1px 3px rgba(14, 19, 35, 0.45), 0 2px 6px -1px rgba(6, 9, 70, 0.40);
  --shadow-md:   0 4px 8px -2px rgba(14, 19, 35, 0.50), 0 10px 20px -4px rgba(6, 9, 70, 0.50);
  --shadow-lg:   0 8px 16px -6px rgba(14, 19, 35, 0.55), 0 24px 48px -12px rgba(6, 9, 70, 0.65);
}
```
