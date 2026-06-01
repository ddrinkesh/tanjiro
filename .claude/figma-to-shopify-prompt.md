# Figma to Shopify — Master Prompt Template

Copy and paste this prompt every time you share a Figma design.
Replace the [...] parts with your actual details.

---

## PROMPT — Standard Section (no slider)

```
You are my Shopify expert engineer. Follow ALL rules from:
- readme.md (main rules)
- readme-ai-custom-section.md (section format)
- readme-ai-figma-to-shopify.md (pixel-perfect rules)

STRICT RULES REMINDER — read before coding:
1. CSS must be ONE LINE per selector — no multiline properties
2. All CSS grouped inside shared media query blocks — no repeated @media blocks
3. Section wrapper class must scope ALL CSS — no global selectors
4. Use my exact spacing structure with section.id (scoped style block)
5. Use my exact heading structure (sec-head / sec-title / sec-text)
6. Use my exact button structure from readme.md rule 16
7. Schema JSON must be expanded multiline — no one-line objects
8. Use inline_richtext for headings, richtext for descriptions
9. JavaScript must be scoped to section id — no global JS
10. Output order: Design Breakdown → Questions → Liquid → CSS → JS → Schema

I am sharing a Figma design. The section name is: [SECTION NAME]
Section file should be: [section-file-name.liquid]
CSS file should be: [section-file-name.css]

DESIGN DETAILS (extracted from Figma):
- Layout: [flex row / flex column / grid - X columns]
- Desktop container width: [e.g. 1200px]
- Desktop section padding: [top Xpx / bottom Xpx]
- Mobile section padding: [top Xpx / bottom Xpx]
- Gap between elements: [Xpx]
- Background color: [#hex]

TYPOGRAPHY:
- Heading: [font-family], [size]px, weight [400/500/600/700], line-height [x.x], color [#hex]
- Body text: [font-family], [size]px, weight [400/500/600/700], line-height [x.x], color [#hex]

IMAGES:
- Image ratio: [W:H — e.g. 16:9 or 4:3]
- Image border-radius: [Xpx]
- Image position: [left / right / background / card]
- Hero image (above fold): [yes / no]

SPECIAL ELEMENTS:
- Has slider: NO — use readme-ai-custom-section.md
- Has button: [yes / no] — label: "[Button Text]"
- Has overlay: [yes / no] — color + opacity: [rgba(0,0,0,0.4)]
- Has badge/tag: [yes / no]
- Has icon: [yes / no]

MOBILE DESIGN:
- Mobile Figma frame provided: [yes / no]
- If no — apply standard collapse rules and tell me assumptions made

Now read the Figma design I am sharing and build the full section.
```

---

## PROMPT — Section With Slider

```
You are my Shopify expert engineer. Follow ALL rules from:
- readme.md (main rules)
- readme-ai-custom-slider.md (slider section format)
- readme-ai-figma-to-shopify.md (pixel-perfect rules)

STRICT RULES REMINDER — read before coding:
1. CSS must be ONE LINE per selector — no multiline properties
2. All CSS grouped inside shared media query blocks — no repeated @media blocks
3. Section wrapper class must scope ALL CSS — no global selectors
4. Use my exact spacing structure with section.id (scoped style block)
5. Use my exact heading structure (sec-head / sec-title / sec-text)
6. Use my exact button structure from readme.md rule 16
7. Use Swiper only — never native Shopify slider
8. Slider options via data-slider-options capture block — no trailing commas
9. Always include grid fallback when slider is disabled
10. Schema JSON must be expanded multiline — no one-line objects
11. JavaScript must parse data-slider-options and scope to section id
12. Output order: Design Breakdown → Questions → Liquid → CSS → JS → Schema

I am sharing a Figma design. The section name is: [SECTION NAME]
Section file should be: [section-file-name.liquid]
CSS file should be: [section-file-name.css]

DESIGN DETAILS (extracted from Figma):
- Layout: slider / carousel
- Desktop container width: [e.g. 1200px or full-width]
- Desktop visible slides: [X]
- Desktop gap between slides: [Xpx]
- Mobile visible slides: [1 / 2]
- Mobile gap: [Xpx]
- Desktop section padding: [top Xpx / bottom Xpx]
- Mobile section padding: [top Xpx / bottom Xpx]
- Background color: [#hex]

SLIDE / CARD:
- Card background: [#hex]
- Card border-radius: [Xpx]
- Card padding: [Xpx]
- Card shadow: [yes / no — value if yes]
- Image ratio inside card: [W:H]
- Image border-radius: [Xpx]

TYPOGRAPHY:
- Heading: [font-family], [size]px, weight [x], line-height [x.x], color [#hex]
- Body text: [font-family], [size]px, weight [x], line-height [x.x], color [#hex]

SLIDER CONTROLS:
- Navigation arrows: [yes / no]
- Pagination dots: [yes / no]
- Autoplay: [yes / no]

MOBILE DESIGN:
- Mobile Figma frame provided: [yes / no]
- If no — apply standard collapse rules and tell me assumptions made

Now read the Figma design I am sharing and build the full section.
```

---

## QUICK PROMPT — When you just share a screenshot fast

```
You are my Shopify expert engineer.
Follow readme.md + readme-ai-custom-section.md + readme-ai-figma-to-shopify.md rules strictly.

Section name: [NAME]
Files: [name.liquid] + [name.css]

Before coding:
1. Give me a design breakdown of what you see
2. List any assumptions for mobile (no mobile frame provided)
3. Then write the full code

Strict reminders:
- One-line CSS per selector
- Shared media query blocks
- My heading structure (sec-head/sec-title/sec-text)
- My button structure (readme.md rule 16)
- Scoped JS only
- Expanded schema JSON

Here is the design:
[PASTE SCREENSHOT OR SHARE FIGMA FRAME]
```
