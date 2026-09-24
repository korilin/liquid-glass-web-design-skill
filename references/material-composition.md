# Material Composition

## Surface hierarchy

Use at most two persistent optical surface levels in one local region:

- **Level 0:** environment.
- **Level 1:** structural surface such as a list shell, inspector rail, toolbar, or comparison card.
- **Level 2:** a necessary autonomous control or information block.

Floating overlays are a separate temporary plane and do not count as persistent nesting when rendered through the top layer or a portal.

## Nesting decision

Before adding a child surface, ask in order:

1. Is the child independently interactive, movable, selectable, or reusable?
2. Does it require a different readability level from the parent?
3. Can spacing, typography, or a faded divider express the grouping instead?
4. Will the child remain visually distinct without repeating the parent's material and border?

Add a child surface only when the first or second answer is yes and the third answer is no.

## Compatibility matrix

| Parent | Child | Decision | Conditions |
|---|---|---|---|
| No surface | Clear glass | Preferred | Controls, chips, floating actions |
| No surface | Frosted glass | Preferred | Dense cards, lists, forms |
| Clear glass | Plain content | Preferred | Use spacing and typography |
| Clear glass | Frosted block | Allowed | Child needs stable readability; inset and smaller radius |
| Clear glass | Clear glass | Usually reject | Allowed only for a floating overlay on a separate plane |
| Frosted glass | Plain content | Preferred | Default internal composition |
| Frosted glass | Clear control | Allowed | Buttons, chips, inputs with visible boundary |
| Frosted glass | Frosted card | Usually reject | Allow only for an autonomous module with obvious spacing and weaker parent boundary |
| Any glass | Same glass with same radius/edge | Reject | Produces double frames and visual thickness |
| Any surface | Opaque child | Exception | Media canvas, code editor, checkerboard, or accessibility fallback |

## Card-in-card rules

Card nesting is valid only when the inner card is an autonomous unit with its own action or lifecycle, such as a removable upload, a separate billing method, or a draggable dashboard module.

When nesting is valid:

- use a different material role from the parent;
- reduce inner radius by 4–8px;
- keep at least 12px between parent edge and child;
- reduce the child's shadow relative to floating surfaces;
- avoid a second title bar if hierarchy is already clear;
- never exceed two persistent surface levels.

Metric values inside a summary card are normally not nested cards. Use a quiet frosted tile only when values require strong scanning separation; otherwise use a grid with spacing.

## Glass-over-glass

Glass over glass is appropriate for temporary depth:

- popover above a toolbar;
- context menu above a card;
- tooltip above a control;
- modal above the page.

Render the overlay outside clipped and scrolling ancestors. The environment and underlying UI must remain perceptible through it. Use a stronger shadow and, if needed, a slightly stronger frosted veil; do not solve separation with an opaque black fill.

Persistent clear-glass children inside a clear-glass parent are normally forbidden because both layers sample the same background and create doubled blur, borders, and highlights.

## Structural layout

- Use material surfaces to define major functional zones, not every content group.
- Keep independent scroll regions independent. Do not let a visual card merge scroll behavior unintentionally.
- Set responsive behavior from the component's available width with container queries when possible.
- Switch comparison content from side-by-side to stacked when each side cannot preserve its minimum useful width.
- Allow toolbars and filter rows to wrap by semantic group; do not shrink controls until text truncates unnecessarily.
- Keep popovers aligned to their trigger, but allow viewport collision handling to change placement.

## Separation without boxes

Use these methods before adding another card:

1. 8–16px spacing;
2. text hierarchy;
3. alignment and grid structure;
4. a localized faded divider;
5. a neutral change in backdrop blur or veil;
6. a new surface only if the content is functionally independent.

Faded divider reference:

```css
.section-divider {
  height: 1px;
  margin-inline: var(--local-radius);
  background: linear-gradient(90deg, transparent, rgb(255 255 255 / 18%) 20%, rgb(255 255 255 / 18%) 80%, transparent);
}
```

The divider is decorative. Do not use it as the only indicator of an interactive boundary.
