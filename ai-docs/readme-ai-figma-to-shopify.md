# Figma to Shopify — Pixel-Perfect Conversion Rules

When I share a Figma design (screenshot, frame, or via Figma MCP), follow these rules
to produce pixel-perfect, responsive Shopify sections that match the design exactly.

---

## 1. Before writing any code — read the design first

* Study the full Figma frame before touching any code.
* Identify every distinct component: heading, subheading, image, button, card, slider, badge, icon, tag, etc.
* Identify layout type: flex row, flex column, CSS grid, or mixed.
* Note all spacing values: padding, margin, gap between elements.
* Note all border-radius values per element.
* Note all font sizes, font weights, line-heights, letter-spacing per text element.
* Note all colors: backgrounds, text, borders, overlays, gradients.
* Note shadow values if any (box-shadow or drop-shadow).
* If anything is unclear or missing (mobile design, hover states, spacing), ask before writing code.
* Never assume or guess design values — always read from Figma or ask.

---

## 2. Figma units to CSS mapping

Always map Figma values to CSS exactly as follows:

| Figma property        | CSS property                        |
|-----------------------|-------------------------------------|
| Frame width           | `max-width` or `width`              |
| Frame padding         | `padding`                           |
| Auto layout gap       | `gap` (flexbox or grid)             |
| Corner radius         | `border-radius`                     |
| Fill (solid)          | `background-color`                  |
| Fill (gradient)       | `background: linear-gradient(...)`  |
| Stroke                | `border`                            |
| Stroke (inside)       | `box-shadow: inset`                 |
| Drop shadow           | `box-shadow`                        |
| Layer blur            | `filter: blur()`                    |
| Background blur       | `backdrop-filter: blur()`           |
| Opacity               | `opacity`                           |
| Font family           | `font-family`                       |
| Font size             | `font-size` in px (convert to rem if needed) |
| Font weight           | `font-weight`                       |
| Line height           | `line-height`                       |
| Letter spacing        | `letter-spacing` (Figma uses px, CSS uses px or em) |
| Text transform        | `text-transform`                    |
| Text decoration       | `text-decoration`                   |
| Image fit (fill)      | `object-fit: cover`                 |
| Image fit (fit)       | `object-fit: contain`               |
| Clip content (on)     | `overflow: hidden`                  |
| Auto layout direction | `flex-direction: row` or `column`   |
| Align items           | `align-items`                       |
| Justify content       | `justify-content`                   |

---

## 3. Layout and spacing accuracy

* Always extract the exact `padding` and `gap` values from Figma — do not use approximate values.
* If the Figma frame uses auto layout, map it directly to `display: flex` with the correct `gap`, `align-items`, and `justify-content`.
* If the Figma frame uses a grid, map it to `display: grid` with the correct `grid-template-columns` and `gap`.
* Container widths: use `max-width` matching the Figma frame width, centered with `margin: 0 auto`.
* Section padding should match the Figma frame padding — add these as default values in the schema `padding_top` and `padding_bottom` range settings.
* Do not add extra padding or margin that is not in the design.
* Do not remove spacing that is in the design.

---

## 4. Typography accuracy

* Match font size exactly in `px` as shown in Figma.
* Match font weight exactly (400, 500, 600, 700, etc.).
* Match line-height exactly. If Figma shows a percentage (e.g. 140%), convert to decimal (1.4).
* Match letter-spacing exactly. Figma shows it in px — use the same in CSS.
* Match text color exactly using the hex or rgba value from Figma.
* Match text-transform (uppercase, capitalize, none).
* If Figma uses a custom font not in Dawn, note it and ask whether to use Google Fonts or an uploaded font asset.
* Never use a fallback font in place of the design font without asking.

Typography CSS example (extracted from Figma):

```css
.section-heading { font-size: 48px; font-weight: 700; line-height: 1.15; letter-spacing: -0.5px; color: #1a1a1a; }
.section-subtext { font-size: 16px; font-weight: 400; line-height: 1.6; color: #6b6b6b; }
```

---

## 5. Colors and backgrounds

* Always use the exact hex or rgba color value from Figma.
* If a background is a gradient, extract both color stops, angle, and positions from Figma exactly.
* If an overlay is used on an image, match the color and opacity exactly using a pseudo-element or absolute div.
* Do not substitute similar colors — if Figma shows `#F5F0EB`, do not use `#f5f5f5`.

Overlay example:

```css
.section-banner { position: relative; }
.section-banner::after { content: ''; position: absolute; inset: 0; background: rgba(0, 0, 0, 0.4); }
.section-banner .banner-content { position: relative; z-index: 1; }
```

---

## 6. Responsive breakpoints — my standard

Always use these breakpoints unless Figma shows something different:

| Breakpoint label | Screen width    | CSS media query                  |
|------------------|-----------------|----------------------------------|
| Mobile           | 0 – 749px       | `@media screen and (max-width: 749px)`  |
| Tablet           | 750px – 989px   | `@media screen and (min-width: 750px) and (max-width: 989px)` |
| Desktop          | 990px+          | `@media screen and (min-width: 990px)` |
| Large desktop    | 1400px+         | `@media screen and (min-width: 1400px)` |

These match Dawn theme breakpoints exactly. Always use these — do not invent other values.

---

## 7. When Figma only shows desktop — how to handle mobile

If Figma only has a desktop design and no mobile frame:

* Stack flex rows into columns on mobile (`flex-direction: column`).
* Make fixed widths `width: 100%` on mobile.
* Reduce font sizes by approximately 20–30% on mobile unless I specify otherwise.
* Reduce padding/gap by approximately 30–40% on mobile unless I specify otherwise.
* Images go full width on mobile.
* Multi-column grids collapse to 1 column on mobile, 2 columns on tablet.
* Always tell me what mobile assumptions you made — do not apply silently.

Mobile typography scale example:

```css
.section-heading { font-size: 48px; }
@media screen and (max-width: 749px) {
.section-heading { font-size: 32px; }
}
```

---

## 8. When Figma shows both desktop and mobile

* Extract spacing, font size, layout, and column count from each breakpoint separately.
* Do not average the values — apply each exactly at its breakpoint.
* Check if any element is hidden on mobile or desktop and apply `display: none` at the right breakpoint.
* Check if element order changes on mobile — use CSS `order` property if needed.

---

## 9. Components — how to handle each type

### Images
* Identify the image dimensions (W × H) in Figma.
* Use `aspect-ratio` matching those dimensions on the image container — never hardcode a pixel height.
* Use `object-fit: cover` inside.
* Use `border-radius` matching Figma exactly.

```css
.card-image { aspect-ratio: 4 / 3; overflow: hidden; border-radius: 12px; }
.card-image img { width: 100%; height: 100%; object-fit: cover; }
```

### Cards
* Identify card width in Figma. If it's part of a grid, calculate column count and gap.
* Match card padding, border, background, shadow, and border-radius exactly.
* On mobile, cards should go full width unless Figma shows 2-column mobile layout.

### Buttons
* Always use my predefined button structure from `readme.md` rule 16.
* Match button padding, border-radius, font-size, font-weight, and color from Figma exactly.
* Match hover state if shown in Figma (use CSS `:hover`).
* Add CSS overrides scoped to the section wrapper — do not modify Dawn global button styles.

Button style override example:

```css
.my-section-wrapper .more-btn { padding: 14px 32px; border-radius: 4px; font-size: 14px; font-weight: 600; letter-spacing: 0.5px; }
```

### Icons / SVGs
* If icons are used in the design, ask whether they exist as SVG assets in the Shopify theme or need to be added.
* Use `inline_asset_content` for SVGs already in the theme assets folder.
* Size icons using `width` and `height` in CSS — never use `font-size` for SVG icons.

### Sliders / Carousels
* If the design shows a slider, always follow my Swiper slider format from `readme-ai-custom-slider.md`.
* Extract slide width, gap, and visible slide count from Figma.
* Use those as default values in `slidesPerView` and `spaceBetween` in the slider options.

### Badges / Tags / Labels
* Match background color, text color, font size, font weight, padding, and border-radius exactly from Figma.
* These are usually `<span>` elements — keep them inline unless the design shows block layout.

---

## 10. What to output after reading a Figma design

When I share a Figma design and ask to build it, always output in this order:

1. **Design breakdown** — brief bullet list of what you identified in the design (layout, components, colors, fonts, spacing). This confirms you read it correctly before writing code.
2. **Questions** (if any) — list anything that is unclear or missing (e.g. "Mobile design not shown — I will apply standard collapsing rules. Confirm?").
3. **Section Liquid file** — full ready-to-paste code.
4. **CSS file** — full ready-to-paste code in my one-line format.
5. **JS file** — only if needed.
6. **Schema** — always included inside the Liquid file.

Do not skip step 1 and 2. They prevent wrong assumptions and save revision rounds.

---

## 11. Pixel-perfect checklist — self-check before outputting code

Before giving me the final code, mentally verify:

- [ ] Font size matches Figma exactly at desktop
- [ ] Font weight matches Figma exactly
- [ ] Line-height and letter-spacing match
- [ ] Colors match exactly (no approximations)
- [ ] Padding and gap match exactly
- [ ] Border-radius matches exactly
- [ ] Image aspect ratio is preserved using `aspect-ratio` CSS
- [ ] Shadows match (if any)
- [ ] Button style matches with scoped CSS override
- [ ] Mobile layout is handled with correct breakpoint
- [ ] No hardcoded pixel heights on fluid containers
- [ ] No layout shift risks (explicit width/height on images)
- [ ] Section wrapper scoping applied to all CSS
- [ ] Schema has correct default values matching design spacing

---

## 12. Common mistakes to avoid

* Do NOT use `height: 300px` on image wrappers — use `aspect-ratio` instead.
* Do NOT approximate colors — `#F0EDE8` ≠ `#f5f5f5`.
* Do NOT use `margin` where Figma uses `padding` inside a frame.
* Do NOT add spacing that is not in the design "just in case".
* Do NOT use generic font fallbacks without confirming the font is available.
* Do NOT collapse a 3-column grid to 1 column on tablet if Figma shows 2 columns on tablet.
* Do NOT apply a hover style that wasn't in the design without telling me.
* Do NOT skip the design breakdown step — always confirm before coding.
