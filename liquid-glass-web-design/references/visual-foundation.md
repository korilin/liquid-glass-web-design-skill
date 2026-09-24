# Visual Foundation

## Contents

- Design model
- Environment requirements
- Optical anatomy
- Material scale
- Shape and spacing
- Failure patterns

## Design model

Liquid glass is an optical relationship between a surface and the environment behind it. The surface should appear to have a boundary, a small amount of depth, and a controlled effect on background detail. It must not appear as a separately painted rectangle.

Judge every surface with three questions:

1. Can the environment still be recognized through it?
2. Does the edge describe a thin optical boundary rather than a thick frame?
3. Does the component remain readable when the environment changes beneath it?

If the first answer is no, the material is frosted or opaque, not clear glass. If the second is no, it is a bordered panel. If the third is no, the theme lacks contrast control.

## Environment requirements

The environment is a first-class theme asset.

| Property | Target | Reject |
|---|---|---|
| Detail | Recognizable medium- and high-frequency detail | Featureless solid field |
| Focus | Sharp source image or crisp generated scene | Global blur applied to the wallpaper |
| Range | Dark, midtone, and bright regions | Uniform near-black or saturated blue/purple wash |
| Scale | Subject scale appropriate to viewport | Extreme zoom that removes context |
| Motion | Static by default; slow transform only when useful | Fast looping video or constant turbulent motion |
| Overlay | Neutral scrim only when required for contrast | Colored overlay that repaints the entire scene |

Use `background-size: cover` as a starting point, but inspect cropping at all target aspect ratios. Set focal position intentionally. Do not compensate for a poor crop by blurring the image.

If the background moves, animate only a compositor-friendly transform or opacity on a dedicated layer. Typical cycle: 40–120 seconds, displacement no more than 2–4% of the viewport, and no motion under `prefers-reduced-motion: reduce`.

## Optical anatomy

A material can combine these signals:

1. **Backdrop blur** — reduces detail behind the surface.
2. **Saturation adjustment** — keeps colors alive after blur; normally `110–145%`.
3. **Neutral veil** — optional for frosted material, never a saturated tint.
4. **Thin edge** — a 1px boundary with uneven luminance.
5. **Inner highlight** — a restrained top or light-facing reflection.
6. **Outer shadow** — soft separation from the environment, not a black halo.
7. **Localized bloom** — only for focus, selection, or semantic emphasis.

Do not make every signal strong at once. Clear glass usually needs blur, a thin edge, and one restrained highlight. Frosted glass adds a neutral veil. Stronger shadow is reserved for floating layers.

## Material scale

Blur is based on surface size and information density, not aesthetic preference per element.

| Scale | Blur | Typical use | Notes |
|---|---:|---|---|
| `control` | 4px | buttons, tags, compact inputs | Keeps background recognizable |
| `floating` | 6px | dropdowns, popovers, compact toolbars | Add shadow before increasing blur |
| `card` | 8px | list shells, metric cards, forms | Default frosted information surface |
| `panel` | 12px | large inspector rails, modal bodies | Maximum routine blur |

Values above 12px need a concrete readability reason. Large surfaces often need less opacity and careful internal layout, not unlimited blur.

Recommended neutral veils:

| Material | Dark environment | Bright environment |
|---|---:|---:|
| Clear | transparent | transparent |
| Frosted control | white 3–6% | white 10–16% or black 3–6% |
| Frosted card | black 10–18% | white 14–24% |
| Floating frosted | black 14–24% | white 18–30% |

Treat these as starting ranges. Contrast tests and real screenshots decide the final value.

## Shape and spacing

- Use a shared radius scale. Recommended: 10px compact, 14px control, 18px card, 22px large panel.
- A child surface radius should normally be 4–8px smaller than its parent.
- Keep edge thickness at 1px. A 2px edge is an explicit emphasis state, not a default.
- Maintain at least 8px optical breathing room between separate glass surfaces; use 12–16px for cards.
- Do not run dividers into rounded edges. Inset by at least the local radius or fade both ends to transparent.
- Prefer whitespace over extra borders for internal grouping.

## Failure patterns

| Symptom | Cause | Correction |
|---|---|---|
| Surface looks black | Veil opacity too high or no visible environment | Reduce fill; confirm background exists behind it |
| Surface looks milky white | Interior highlight or gradient covers too much area | Restrict light to the edge and reduce opacity |
| Surface looks like neon | Edge, accent, and glow are all strong | Keep one focal signal; neutralize the others |
| Glass effect disappears | Background is flat or already blurred | Use a sharper, more detailed environment |
| UI looks noisy | Every child has its own border and material | Flatten grouping; reserve surfaces for structural regions |
| UI looks thick | Multiple inset shadows and duplicated outlines | Keep one edge, one inner highlight, one shadow plane |
| Narrow screen becomes one color | Oversized colored gradient or background focal crop | Reposition/crop environment; avoid viewport-filling tint layers |
| Scrolling stutters | Too many overlapping backdrop filters or animated shadows | Share surfaces, reduce layers, animate transform/opacity only |
