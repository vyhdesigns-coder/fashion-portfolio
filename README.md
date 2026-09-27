# Portfolio Template — Fashion Business Internship

A starter portfolio for an MIS student who designs and sews his own clothing and is applying for business-side internships at fashion houses (merchandising, product development, sourcing, marketing, brand, operations).

This is a **template**. Nearly all content is placeholder.

**Visual direction:** a screenprint look on charcoal. Cream "ink" sits on a near-black charcoal background, with thin framed panels like a record sleeve, a grain texture over the whole page, and halftone-dot image placeholders. A **barcode** is the signature mark, and it doubles as a garment SKU / hang tag. It appears in the header logo, the hero, every case study card, every case study title block, and the footer.

No frameworks, no build step, and no JavaScript. Open `index.html` in a browser to view it.

---

## File structure

```
/
├── index.html      Home: hero, work (3 case study cards), about, contact
├── denim.html      Case study 1 — Make It: Built to Fit
├── brand.html      Case study 2 — Brand It: Building [Brand Name]
├── business.html   Case study 3 — Run It: Behind the Seams
├── styles.css      One shared stylesheet (design tokens at the top)
└── README.md       This file
```

Suggested folders to add as content comes in:

```
images/             Photos and screenshots (see "Swapping image placeholders")
resume.pdf          Linked from the nav, hero, and contact section
```

Each page has the same header, nav, and footer. Each case study page follows the same pattern: back link → title block → numbered sections → previous/next pager.

---

## Placeholder conventions

| Type | Looks like | What to do |
|---|---|---|
| **Text** | `[Brand Name]`, `[Number of pairs made]`, `[Short explanation of why this fit change mattered]` | Replace the whole thing, brackets included. Search the project for `[` to find what's left. |
| **Images** | Gray dashed box with a label such as `IMAGE: Side-by-side of first and latest pair of jeans (16:9)` | Take the photo described at the listed aspect ratio, then swap it in (see below). |
| **Alt text** | `aria-label="[Alt text: ...]"` on every image placeholder | Write a real description when you swap in the image. |
| **Links** | `href="[resume.pdf]"`, `href="mailto:[you@email.com]"` | Replace with the real URL or file path. |
| **Tables** | Correct column headers with 2–4 rows of bracketed example values | Replace the values and add or remove `<tr>` rows as needed. |
| **Section comments** | `<!-- ... -->` above every section | Explains what belongs there and why recruiters care. You can keep or delete them. They don't show on the page. |

**Quick check for leftovers:** search every `.html` file for `[` and `IMAGE:`. When nothing comes back, the content is done.

---

## Editing design tokens

Every color, font, font size, spacing value, max width, and border radius is a CSS variable at the top of `styles.css`, in the `:root { ... }` block (section 1).

| Token group | Variables | Notes |
|---|---|---|
| Color | `--color-bg` (charcoal), `--color-surface`, `--color-surface-strong`, `--color-line` (cream frame rules), `--color-border` (quiet dividers), `--color-text` (cream), `--color-text-muted`, `--color-accent`, `--color-accent-contrast`, `--color-placeholder-text` | Dark by default. Keep text contrast at 4.5:1 or higher against the background. |
| Texture | `--grain-opacity`, `--halftone-dot`, `--halftone-size` | Set `--grain-opacity: 0` to turn off the page grain (useful before importing to Figma). |
| Font families | `--font-sans`, `--font-serif`, `--font-mono`, `--font-body`, `--font-heading`, `--font-label` (mono, for labels, tags, and codes) | System fonts as placeholders. To use a web font, add a `<link>` in each page's `<head>` and update `--font-body` and/or `--font-heading`. |
| Type scale | `--text-xs` … `--text-5xl` | 1.25 ratio. `--text-5xl` is the hero name. Large sizes shrink at the breakpoints (section 9). `--tracking-caps` sets the letter-spacing of uppercase labels. |
| Spacing | `--space-1` (4px) … `--space-9` (96px) | Every gap, padding, and margin uses these. Mirror them as spacing variables in Figma. |
| Layout | `--max-width`, `--max-width-text`, `--gutter`, `--frame-gap`, `--frame-pad` | Page width, reading width, side padding, gap between framed panels, and padding inside them. |
| Radius / lines | `--radius-*`, `--border-width`, `--line-width` | Radii are 0 (screenprint is sharp-edged). `--line-width` is the frame rule weight. |

Changing a token updates it everywhere.

### Figma notes
- Layouts use flexbox (`.stack`, `.cluster`) and grid (`.grid--2/3/4`, `.split`) with token-based `gap`s, so they map to Figma auto layout.
- Class names follow a block__element--modifier pattern (e.g., `.case-card__title`, `.cs-section--costing`). Every section has an ID (`section-overview`, `section-costing`, and so on), so imported layers stay easy to identify.
- Signature pieces:
  - `.frame` / `.frame__row`: a ruled box. Rows are separated by rules.
  - `.barcode`: patterns `--v1`–`--v4`, sizes `--mini`, `--sm`, default, `--lg`. Drawn in CSS, no image file.
  - `.mark-rings` and `.mark-burst`: decorative graphics taken from the references.
- Grain is a fixed `body::after` overlay, so it won't import as a layer. Recreate it in Figma with a noise fill or texture image.
- Shared case study components: `.cs-title`, `.quick-facts`, `.cs-section__header`, `.split`, `.full-image`, `.data-table`, `.quote-callout`, `.metric-callout`, `.insight-callout`, `.theme-block`, `.cs-pager`.

---

## Swapping image placeholders for real images

1. Put the image in an `images/` folder, e.g. `images/denim-hero.jpg`.
2. Find the placeholder:
   ```html
   <div class="img-placeholder ratio-16x9" role="img" aria-label="[Alt text: your latest pair of jeans]">
     IMAGE: Hero shot of latest pair of jeans, full-length on body or flat lay (16:9)
   </div>
   ```
3. Replace it with an `<img>`. Keep the same `ratio-*` class and switch `img-placeholder` to `img-cover`. Add `img-cover--duotone` to render the photo in grayscale with extra contrast so it matches the screenprint look:
   ```html
   <img src="images/denim-hero.jpg"
        alt="Latest pair of raw indigo jeans, full-length, worn with a white tee"
        class="img-cover img-cover--duotone ratio-16x9"
        loading="lazy">
   ```
4. Write alt text that describes what's in the image. Use `alt=""` only for purely decorative images.

Available ratio classes: `ratio-21x9`, `ratio-16x9`, `ratio-3x2`, `ratio-4x3`, `ratio-1x1`, `ratio-4x5`, `ratio-3x4`, `ratio-9x16`. `img-cover` crops to fill the ratio, so the image won't stretch.

**Brand color swatches** (`brand.html`) aren't images. To show a color, give each `.swatch__chip` a background, e.g. `<div class="swatch__chip" style="background:#1f2a44">`, or add a class in `styles.css`.

**Getting the screenprint look in photos:** shoot or edit with high contrast and hard light. For a true stipple or halftone like the references, run images through a halftone or stochastic-dither filter (Photoshop *Bitmap → Diffusion Dither*, or a free halftone generator) and export in cream on charcoal.

**Tip:** export photos at about 2× their display width (hero images around 2400px wide, cards around 1000px) and compress them (JPG/WebP, under 400KB each) so the site loads fast.

---

## Accessibility built in

- Skip-to-content link, one `<h1>` per page, and headings in order (h1 → h2 → h3).
- Landmarks: `<header>`, `<nav aria-label>`, `<main>`, `<footer>`. Sections are labelled with `aria-labelledby`.
- Every image placeholder has `role="img"` and a placeholder `aria-label` for alt text.
- Tables use `<caption>`, `<th scope="col">`, and `<th scope="row">`, and scroll sideways on small screens instead of breaking the layout.
- Visible focus outlines, and text contrast that passes WCAG AA with the default tokens.
