# Implementation Guide

## Architecture

Implement from general to specific:

1. theme tokens;
2. material primitives;
3. component recipes;
4. state variants;
5. layout utilities;
6. page composition.

Recommended CSS layer order:

```css
@layer lg.tokens, lg.materials, lg.components, lg.states, lg.utilities;
```

Do not place page-specific selectors in the material layer. Do not put blur, edge, and shadow declarations into every component recipe.

## Token contract

At minimum define:

- backdrop tone: dark, light, or mixed;
- text roles;
- accent and semantic colors;
- four blur scales: 4, 6, 8, 12px;
- neutral veils for clear, frosted, and floating surfaces;
- edge strengths;
- embedded, raised, and floating shadows;
- radius scale;
- state transition durations and easing.

Use `data-lg-tone="dark|light"` or the host theme mechanism to switch composited neutrals. Do not infer tone continuously from pixels unless the product truly needs adaptive sampling; it adds complexity and unstable state changes.

## Framework mapping

### Vanilla HTML/CSS

Use semantic classes plus material attributes:

```html
<section class="lg-card lg-material" data-lg-material="frosted">
  ...
</section>
```

### React, Vue, Svelte

Create a small primitive layer rather than one component per visual permutation:

```text
GlassSurface(material, elevation, radius, as)
GlassButton(tone, size, selected, disabled)
GlassCard(material, interactive, selected)
GlassPopover(open, anchor, placement)
StatusIndicator(tone, label)
```

Map props to stable classes or recipes. Reject arbitrary `blur`, `alpha`, and `glow` props in ordinary product code.

### Utility CSS

Create named recipes or component classes. Do not paste a 20-utility glass stack into every call site. Tokens remain CSS custom properties so runtime themes can switch without regenerating every class.

## Background implementation

Use a dedicated fixed or absolute environment layer below the application:

```css
.app-environment {
  position: fixed;
  inset: 0;
  z-index: -2;
  background: var(--app-background) center / cover no-repeat;
}
```

Do not apply `filter: blur()` to this layer. If contrast requires a scrim, add a separate neutral layer so opacity can be tuned independently.

Prevent narrow-screen color collapse by testing `background-position` and crop at each layout family. Use `<picture>` or alternate focal positions when one crop cannot serve all aspect ratios.

## Backdrop filtering

- Apply `backdrop-filter` to stable material surfaces.
- Avoid dozens of overlapping filtered descendants.
- Prefer one list shell surface with plain rows over filtered material on every row.
- Use `isolation: isolate` only when the stacking behavior is understood; it does not solve overlay clipping.
- Ensure content behind the surface actually exists in the same compositing context.
- Never add an opaque fill because backdrop blur appears weak; first confirm stacking, background placement, and browser support.

## Overlay implementation

Popover, select menu, tooltip, and context menu should use one of:

- the HTML Popover API;
- `<dialog>` for modal interaction;
- a framework portal to a dedicated overlay root.

Position against the trigger, handle viewport collision, and keep focus/keyboard semantics. A large `z-index` cannot escape an ancestor's clipping or transformed stacking context.

## Responsive behavior

Use container queries for component composition and media queries for global layout/environment changes.

Examples:

- comparison grid stacks when its own content area is too narrow;
- toolbar wraps when its own width cannot fit semantic groups;
- inspector becomes a separate row when the workspace cannot preserve minimum column widths;
- card padding steps down one token at compact widths.

Do not reduce type and controls indefinitely to preserve a desktop column count.

## Fallback

Provide a deterministic non-glass fallback:

```css
@supports not ((backdrop-filter: blur(1px)) or (-webkit-backdrop-filter: blur(1px))) {
  .lg-material {
    background: var(--lg-fallback-surface);
    border-color: var(--lg-edge-default);
  }
}
```

Fallback surfaces may be more opaque, but remain neutral and use the same component, spacing, color, and state system.

## Performance budget

- Keep routine blur at or below 12px.
- Avoid backdrop filters on every virtualized or rapidly scrolling item.
- Do not animate `backdrop-filter`, SVG displacement, large gradients, or large multi-stop shadows continuously.
- Animate compositor-friendly `transform` and `opacity` when motion is necessary.
- Pause decorative background motion when the document is hidden.
- Test rapid scrolling, open menus, resize, and simultaneous hover/focus states.
- Profile before replacing a simple CSS surface with Canvas or WebGL.

## Migration strategy

For an existing UI:

1. inventory repeated material declarations;
2. create tokens without changing appearance;
3. replace duplicated declarations with shared primitives;
4. correct environment and material hierarchy;
5. normalize component states;
6. remove obsolete wrappers, borders, and overrides;
7. validate representative screens before broad rollout.

Avoid piling final overrides at the end of a stylesheet indefinitely. Once the direction is accepted, consolidate the source rules.
