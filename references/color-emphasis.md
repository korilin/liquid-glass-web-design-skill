# Color and Emphasis

## Color model

The environment supplies most visible color. Interface materials remain neutral so the scene can pass through them. Theme color appears through text, small accents, selection edges, and semantic signals.

Define roles, not page-specific colors:

- `text-primary`, `text-secondary`, `text-muted`, `text-disabled`;
- `edge-soft`, `edge-default`, `edge-strong`;
- `veil-control`, `veil-card`, `veil-floating`;
- `accent`, `accent-soft`, `accent-edge`;
- `success`, `warning`, `danger`, `info`;
- `shadow`, `focus-ring`.

Prefer OKLCH for authored solid colors because lightness changes remain predictable. Use alpha-composited white or black for neutral optical edges and veils.

## Backdrop-aware text

| Role | Dark or mixed backdrop | Bright backdrop |
|---|---|---|
| Primary | white 92–98% | near-black 88–94% |
| Secondary | white 70–80% | near-black 68–78% |
| Muted | white 55–66% | near-black 52–64% |
| Disabled | white 34–44% | near-black 32–42% |

Muted text must remain readable; “muted” is hierarchy, not near-invisibility. Validate final composited contrast against the actual background, not the declared RGBA value.

## Neutral material color

Clear glass has no interior hue. Its edge may borrow a small amount of light from the environment, but should still read as neutral.

Frosted glass uses a neutral veil:

- dark/mixed scenes: low-alpha near-black or cool-neutral, never saturated navy;
- bright scenes: low-alpha white or neutral gray;
- mixed scenes: combine backdrop blur with a very low-alpha neutral veil and text shadow rather than a colored fill.

Do not use blue or purple as the default glass color merely because they are associated with futuristic UI.

## Accent selection

Choose one theme accent whose lightness works on the dominant environment. Derive variants by changing lightness/chroma, not by introducing unrelated hues.

Recommended starting pattern:

```css
--accent: oklch(76% 0.14 235);
--accent-soft: color-mix(in oklch, var(--accent) 12%, transparent);
--accent-edge: color-mix(in oklch, var(--accent) 62%, white 18%);
```

Use accent for:

- selected controls;
- current navigation location;
- primary action;
- focus ring when it is not semantic;
- small chart or progress highlights.

Do not use accent for every border, label, and icon.

## Semantic colors

Suggested starting solids:

| Role | OKLCH | Use |
|---|---|---|
| Success | `oklch(78% 0.18 145)` | accepted, healthy, complete |
| Warning | `oklch(80% 0.16 78)` | caution, attention, pending risk |
| Danger | `oklch(69% 0.22 25)` | rejected, failed, destructive |
| Info | `oklch(78% 0.13 235)` | neutral information, active process |

Semantic fills should usually remain below 12% opacity. Use the solid color for a dot, icon, short edge, or text. Never turn a large card fully green or red unless it is a dedicated alert surface.

## State treatment

| State | Luminance/edge | Color | Glow | Motion |
|---|---|---|---|---|
| Rest | Soft edge | Neutral | None | None |
| Hover | Edge +10–20%; veil +2–4% | Neutral or slight accent | None | 120–180ms |
| Focus-visible | Strong 2px outer ring | Accent | Optional tight halo | 120ms |
| Pressed | Slightly darker veil; 1px depth shift | Same as rest | None | 80–120ms |
| Selected | Strong edge plus small veil | Accent | Restrained, localized | 160–220ms |
| Disabled | Lower contrast, stable shape | Neutral | None | None |
| Success | Normal material | Success on indicator/text | Tight indicator glow | 180–240ms |
| Danger | Normal material | Danger on indicator/text | Tight indicator glow | 180–240ms |

Hover must not look selected. Focus must remain visible even when hover is absent. Selected state must not depend on color alone; change edge, icon, checkmark, or typography too.

## Glow policy

Glow is permitted when one of these is true:

- a small status indicator needs to remain legible over a complex scene;
- the currently selected control needs a secondary focal cue;
- a primary action is intentionally emphasized;
- focus-visible needs separation from a similarly colored background.

Constraints:

- radius: normally 6–16px for controls, 4–12px for status dots;
- opacity: normally 10–28%;
- area: localized around edge, icon, or dot;
- count: one dominant glow family per local region;
- animation: no continuous pulsing unless it represents a live process and reduced motion is respected.

Do not glow muted labels, disabled controls, negative absence states, every card edge, or entire large panels.

## Emphasis decision

1. Increase font weight or size if the information hierarchy is weak.
2. Increase text luminance if readability is weak.
3. Strengthen the local edge if the boundary is weak.
4. Add a small neutral veil if the background interferes.
5. Add accent if the element is selected or primary.
6. Add glow only if accent alone cannot communicate the focal or semantic state.

This order prevents a colorful interface from compensating for poor hierarchy.
