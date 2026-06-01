# Figma Design Extraction Checklist

Fill this out BEFORE sharing your Figma design with Claude.
Copy the filled checklist into your prompt for pixel-perfect results.
The more you fill in, the less AI has to guess.

---

## SECTION INFO

- Section name: _______________
- Liquid file name: _______________
- CSS file name: _______________
- Has slider: [ ] Yes  [ ] No
- Desktop Figma frame provided: [ ] Yes  [ ] No
- Mobile Figma frame provided: [ ] Yes  [ ] No

---

## LAYOUT

- Layout type: [ ] Flex row  [ ] Flex column  [ ] Grid  [ ] Mixed
- Grid columns (desktop): ___
- Grid columns (tablet): ___
- Grid columns (mobile): ___
- Container width (max-width): ___px  [ ] Full width
- Container centered: [ ] Yes  [ ] No

---

## SPACING

- Section padding top (desktop): ___px
- Section padding bottom (desktop): ___px
- Section padding top (mobile): ___px
- Section padding bottom (mobile): ___px
- Gap between items/columns: ___px (desktop) / ___px (mobile)
- Inner card/block padding: ___px

---

## COLORS

- Section background: ___________
- Card/block background: ___________
- Heading color: ___________
- Body text color: ___________
- Subtext / label color: ___________
- Button background: ___________
- Button text color: ___________
- Button hover background: ___________
- Border color (if any): ___________
- Overlay color + opacity (if any): rgba(___, ___, ___, ___)

---

## TYPOGRAPHY — HEADING

- Font family: _______________
- Font size (desktop): ___px
- Font size (mobile): ___px
- Font weight: ___
- Line height: ___ (e.g. 1.2 or 120%)
- Letter spacing: ___px
- Text transform: [ ] None  [ ] Uppercase  [ ] Capitalize
- Color: ___________

## TYPOGRAPHY — SUBHEADING / LABEL

- Font family: _______________
- Font size (desktop): ___px
- Font size (mobile): ___px
- Font weight: ___
- Line height: ___
- Letter spacing: ___px
- Text transform: [ ] None  [ ] Uppercase  [ ] Capitalize
- Color: ___________

## TYPOGRAPHY — BODY / DESCRIPTION

- Font family: _______________
- Font size (desktop): ___px
- Font size (mobile): ___px
- Font weight: ___
- Line height: ___
- Color: ___________

---

## IMAGES

- Image aspect ratio: ___ : ___ (e.g. 16:9 / 4:3 / 1:1)
- Image border-radius: ___px
- Image fit: [ ] Cover  [ ] Contain
- Image position: [ ] Left  [ ] Right  [ ] Top  [ ] Background  [ ] Inside card
- Is this the hero/first image on page: [ ] Yes  [ ] No
- Has overlay on image: [ ] Yes → color + opacity: ___________

---

## BUTTONS

- Has button: [ ] Yes  [ ] No
- Button label: _______________
- Button style: [ ] Primary (filled)  [ ] Secondary (outline)
- Button padding: ___px ___px (top/bottom, left/right)
- Button border-radius: ___px
- Button font size: ___px
- Button font weight: ___
- Button letter spacing: ___px

---

## CARDS (if section has cards)

- Card border-radius: ___px
- Card background: ___________
- Card border: ___px solid ___________
- Card shadow: [ ] Yes → value: _______________  [ ] No
- Card padding: ___px
- Card min-height: ___px  [ ] Auto

---

## SLIDER (if section has slider)

- Visible slides desktop: ___
- Visible slides tablet: ___
- Visible slides mobile: ___
- Space between slides (desktop): ___px
- Space between slides (mobile): ___px
- Show navigation arrows: [ ] Yes  [ ] No
- Show pagination dots: [ ] Yes  [ ] No
- Autoplay: [ ] Yes  [ ] No
- Slide auto width: [ ] Yes  [ ] No

---

## SPECIAL ELEMENTS

- Has badge / tag: [ ] Yes  [ ] No
  → Badge text: ___  Background: ___  Text color: ___  Border-radius: ___px
- Has icon / SVG: [ ] Yes  [ ] No
  → Icon size: ___px  Color: ___
- Has divider / border line: [ ] Yes  [ ] No
- Has background pattern / texture: [ ] Yes  [ ] No
- Has animation / scroll effect: [ ] Yes  [ ] No

---

## NOTES / EXTRA INFO

_______________________________________________
_______________________________________________
_______________________________________________

---

## HOW TO USE THIS CHECKLIST

1. Open your Figma design
2. Select the frame/section you want to build
3. Fill in this checklist by clicking each element in Figma and reading values from the right panel
4. Copy the filled checklist into your Claude prompt
5. Share the Figma screenshot or frame link alongside it

### Quick Figma tips for finding values:
- **Spacing/padding** → Select frame → Right panel → "Auto layout" section
- **Gap** → Select frame → Right panel → gap value between layout items
- **Font values** → Select text layer → Right panel → Typography section
- **Colors** → Select element → Right panel → Fill section → click to get hex
- **Border-radius** → Select element → Right panel → corner radius field
- **Shadow** → Select element → Right panel → Effects section
- **Image ratio** → Select image frame → Right panel → W and H values → divide to get ratio
