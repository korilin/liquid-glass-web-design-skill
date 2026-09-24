# Component Contracts

## Component identity

Every reusable component is defined by:

`semantic role + material variant + size + interaction state + optional semantic tone`

Examples:

- `Button / clear / compact / selected / accent`
- `Card / frosted / regular / rest / neutral`
- `StatusDot / no-surface / small / rest / success`

Do not encode layout location into component appearance. A frosted card in a sidebar and a frosted card in a modal use the same material, edge, radius family, and typography rules.

## Shared variant API

Expose equivalent variants in the host stack:

```text
material: clear | frosted | opaque-fallback
size: compact | regular | spacious
state: rest | selected | disabled | loading
tone: neutral | accent | success | warning | danger | info
elevation: embedded | raised | floating
```

Only expose variants that the product actually uses. Prevent arbitrary per-instance alpha, blur, and shadow values.

## Card

- Default to frosted material for dense information and clear material for lightweight grouping.
- Header is optional; do not add a label merely to decorate the card.
- Use padding of 12–20px according to density.
- Do not create a separate title strip or footer strip unless it contains independent controls.
- Selected cards change edge and a small veil; they do not become saturated blocks.
- Hover is only present when the entire card is interactive.

## Button

- Clear glass is the default material.
- Height: 32–44px; compact icon buttons may be 30px.
- Maintain the same edge, radius, and hover recipe across text and icon buttons.
- Primary action uses accent edge/veil; destructive action uses danger only when the action is actually destructive.
- Pressed state may move by 1px or reduce highlight. Do not scale dramatically.
- Toggle buttons expose `aria-pressed`; selection is visible without relying on color alone.

## Chip and tag

- Chips are interactive filters or selections; tags are informational.
- Interactive chips receive hover, focus, pressed, and selected states.
- Informational tags do not glow on hover.
- Status tags may use semantic text/edge and a low-alpha veil; negative absence states remain neutral unless they are errors.
- Keep labels short and prevent the material from becoming a large pill-shaped banner.

## Input and search

- Use clear or lightly frosted glass according to background complexity.
- Focus-visible strengthens edge and adds a ring outside layout bounds.
- Placeholder text remains readable but subordinate.
- Validation state uses semantic icon/text plus edge; do not fill the entire field red or green.
- Expandable search controls must expand in place without detaching into an unrelated popover unless search suggestions require an overlay.

## Select, menu, and popover

- Trigger and menu belong to the same component family.
- Use a custom menu only when the project can preserve keyboard navigation, focus management, roles, and selection semantics.
- Render floating content in the top layer or an overlay root so it is not clipped.
- Use floating frosted material, 6px blur, stronger shadow, and a neutral veil that still reveals underlying content.
- Menu options are normally plain rows inside one surface, not individual nested glass cards.
- Selected options use a checkmark and accent text/edge or low-alpha row veil.

## List shell and list item

- The list shell may be one frosted structural surface.
- Items inside it should normally be plain rows with spacing and faded separators.
- Use item cards only when items are autonomous objects with their own action set or drag behavior.
- Hover belongs to the item under the pointer and must not trigger expensive backdrop changes.
- Selected item uses a stable accent edge/veil distinct from hover.
- Scroll-edge disappearance should be implemented with content opacity or a true mask attached to the viewport, never with an opaque overlay that covers rows.

## Metric tile

- Prefer a grid of quiet frosted tiles only when scanning benefits from distinct cells.
- Use one shared tile recipe; do not color each metric independently.
- Label is secondary, value is primary.
- Semantic color belongs to the value or indicator, not the entire tile.

## Status indicator

- Use a 6–10px solid dot or a compact icon.
- Success, warning, danger, and live states may use a tight semantic glow.
- Neutral, absent, inactive, and disabled states use a dim neutral indicator without glow.
- Pair color with text when the meaning is not already explicit nearby.

## Modal and drawer

- Use one large frosted surface with a clear hierarchy.
- Avoid a glass card for every modal section.
- Backdrop dimming is neutral and minimal; preserve enough environment to support the glass illusion.
- Focus is trapped and restored correctly.

## Interaction state contract

Every interactive component must define:

| State | Required cue |
|---|---|
| Rest | Stable boundary and readable label |
| Hover | Small edge or veil increase |
| Focus-visible | 2px visible ring independent of hover |
| Pressed | Depth reduction or 1px shift |
| Selected | Persistent non-color cue plus accent |
| Disabled | Lower contrast and no hover/press response |
| Loading | Stable dimensions and progress semantics |
| Error | Semantic icon/text and accessible announcement when appropriate |

Transitions should normally be 120–220ms with an ease-out curve. Animate opacity, color, border color, and small transforms. Avoid animating `backdrop-filter`, large blur radii, layout dimensions, or multi-layer shadows during scroll.

## Accessibility

- Text contrast: target WCAG AA after compositing over representative background samples.
- Focus: never remove outline without an equal or stronger replacement.
- Motion: honor reduced motion and avoid essential information conveyed only by animation.
- Pointer target: at least 36px for dense desktop tools and 44px for touch-first interfaces.
- Semantics: preserve button, link, checkbox, menu, listbox, dialog, and status roles.
- State: use `aria-pressed`, `aria-selected`, `aria-expanded`, `aria-current`, or native controls as appropriate.
