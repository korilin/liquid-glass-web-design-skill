---
name: liquid-glass-web-design
description: Design, implement, or refactor web interfaces into a coherent liquid-glass system with backdrop-aware materials, reusable component contracts, restrained emphasis, responsive composition, and visual quality gates. Use for product UI, dashboards, tools, and component libraries; do not use for an isolated glass illustration with no interface system.
---

# Liquid Glass Web Design

Build an interface in which the background remains a visible part of the composition and every optical surface belongs to one deliberate material system. Treat liquid glass as a theme architecture, not a collection of translucent gradients.

## Definition

A successful liquid-glass interface has three distinct layers:

1. **Environment** — a clear, detailed background that supplies color and depth.
2. **Material** — transparent or frosted optical surfaces that blur, soften, and edge-highlight the environment without replacing it.
3. **Component** — cards, controls, menus, tags, and status indicators whose shape, spacing, typography, and states remain consistent wherever they appear.

The environment must still be recognizable through clear glass. Frosted glass may veil detail for readability, but must remain visibly related to the environment. A dark translucent rectangle with a border is not sufficient.

## Required workflow

### 1. Inspect before styling

For an existing project, identify:

- framework, styling system, component boundaries, and browser targets;
- existing theme tokens and reusable primitives;
- scroll containers, overlays, popovers, and responsive layout behavior;
- the real background at dark, bright, detailed, and low-detail regions;
- interaction and performance constraints.

Preserve product behavior and data flow unless the user also requests structural changes. Remove local one-off styling only after replacing it with a shared material or component contract.

### 2. Establish the theme

Read [references/visual-foundation.md](references/visual-foundation.md) before choosing materials or background treatment. Define global tokens for tone, text, edge light, shadow, blur, radius, motion, accent, and semantic states.

Use the bundled [assets/liquid-glass.css](assets/liquid-glass.css) as a reference implementation or copy its token and material layers into the project's native styling system. Adapt names to the host project; do not maintain two competing token systems.

### 3. Choose materials before components

Read [references/material-composition.md](references/material-composition.md) when laying out surfaces or nesting containers.

Use only these primary material roles:

- **clear glass** for controls, tags, floating actions, compact toolbars, and surfaces where the environment should remain legible;
- **frosted glass** for information-dense cards, long lists, forms, and areas needing stronger text stability;
- **opaque fallback** only when backdrop filtering is unavailable or contrast cannot be made accessible.

Components consume a material role. They do not invent a new material per instance.

### 4. Build shared component contracts

Read [references/component-contracts.md](references/component-contracts.md) for controls, cards, list items, inputs, menus, status indicators, and interaction states.

Prefer one of these implementations:

- shared semantic classes and data attributes for vanilla HTML/CSS;
- shared primitives and variants for React, Vue, Svelte, or another component framework;
- host design-system tokens and recipes when the project already has them.

Do not duplicate the same glass declaration in individual pages. A `frosted card` must render from the same tokens and recipe everywhere, while allowing layout-specific size and content.

### 5. Apply color and emphasis deliberately

Read [references/color-emphasis.md](references/color-emphasis.md) before selecting text colors, accents, semantic colors, selection treatments, or glows.

Use this emphasis order:

1. spacing and grouping;
2. typography and luminance;
3. edge strength or a small neutral veil;
4. accent color;
5. glow.

Do not jump directly to saturated fills or broad glows. Glow is a semantic or focal signal, not a default glass property.

### 6. Implement optical behavior within browser limits

Read [references/implementation.md](references/implementation.md) for architecture, fallbacks, responsive behavior, and performance. Read [references/optical-effects.md](references/optical-effects.md) only when actual distortion or refraction is requested.

Keep global backgrounds sharp. Blur belongs to the surface through `backdrop-filter`, not to the page background image. Do not animate blur, displacement, or large shadows continuously in scrolling regions.

### 7. Validate before delivery

Read and execute [references/quality-gates.md](references/quality-gates.md). Verify the interface against more than one background region and at every interaction state. Fix system-level causes before patching individual components.

## Non-negotiable constraints

- No opaque or near-opaque fill masquerading as glass.
- No colored glass by default; hue is reserved for selection, semantics, or an explicitly colored theme variant.
- No large white bloom or high-contrast gradient covering the component interior.
- No repeated same-material card-inside-card framing.
- No full-width divider that touches container edges; inset it or fade its ends.
- No permanent motion used merely to prove that a surface is “liquid.”
- No per-instance material tuning when a token or component variant can express the difference.
- No native select/menu left visually unrelated when custom controls are already required by the theme.
- No popover clipped by a scroll container; use the top layer, a portal, or equivalent overlay root.
- No reliance on blur alone for text contrast or state distinction.

## Delivery expectations

When implementing, report:

- the chosen environment and tone strategy;
- the material roles and shared tokens introduced or reused;
- the component primitives or variants affected;
- responsive and fallback behavior;
- visual, interaction, accessibility, and performance checks performed.

When reviewing without editing, identify violations by system cause: environment, material, composition, component contract, state, color, or performance. Avoid subjective labels without a concrete rule and correction.
