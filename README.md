# Liquid Glass Web Design Skill

A Codex skill for designing, implementing, and reviewing coherent liquid-glass web interfaces.

This skill treats liquid glass as a complete design system rather than a translucent CSS effect. It connects the background environment, optical materials, reusable components, interaction states, color roles, responsive composition, accessibility, and performance into one implementation model.

## What it provides

- A precise definition of clear glass, frosted glass, and opaque fallback materials.
- Shared blur, edge, veil, radius, shadow, color, and motion tokens.
- Rules for cards, buttons, chips, inputs, menus, lists, metrics, status indicators, modals, and drawers.
- A decision matrix for card nesting, glass-over-glass, and glass-over-frosted composition.
- Explicit hover, focus-visible, pressed, selected, disabled, loading, success, and error states.
- Backdrop-aware text, accent, semantic color, and glow guidance.
- CSS, React, Vue, Svelte, and utility-CSS implementation patterns.
- Separate guidance for CSS optics, SVG displacement, WebGL refraction, and 3D glass.
- Visual, accessibility, responsive, and performance quality gates.
- A reusable CSS foundation with theme tokens and component recipes.

## Design principles

The system is built around a few durable rules:

1. The environment remains sharp, visible, and compositionally useful.
2. Glass changes how the environment is perceived; it does not replace it with a painted rectangle.
3. Clear and frosted glass are reusable material variants shared by every component family.
4. Persistent optical depth stays shallow; unnecessary same-material card nesting is rejected.
5. Color and glow communicate selection, focus, or semantic state instead of decorating every edge.
6. Liquid appearance comes from restrained optics and state response, not permanent animation.
7. Responsive layout follows available component space, while advanced effects stay within a measured performance budget.

## Repository structure

| Path | Purpose |
|---|---|
| [`SKILL.md`](SKILL.md) | Skill entry point, workflow, routing, and non-negotiable constraints |
| [`references/visual-foundation.md`](references/visual-foundation.md) | Environment, optical anatomy, material scale, and failure diagnosis |
| [`references/material-composition.md`](references/material-composition.md) | Surface hierarchy, nesting matrix, and layout composition |
| [`references/color-emphasis.md`](references/color-emphasis.md) | Text, accent, semantic color, state, and glow rules |
| [`references/component-contracts.md`](references/component-contracts.md) | Reusable component variants and interaction contracts |
| [`references/implementation.md`](references/implementation.md) | Cross-stack architecture, responsive behavior, fallbacks, and performance |
| [`references/optical-effects.md`](references/optical-effects.md) | CSS, SVG, WebGL, and 3D optical capability boundaries |
| [`references/quality-gates.md`](references/quality-gates.md) | Delivery checklist and review severity model |
| [`assets/liquid-glass.css`](assets/liquid-glass.css) | Reusable CSS tokens, materials, components, and states |
| [`agents/openai.yaml`](agents/openai.yaml) | Codex UI metadata and default invocation prompt |

## Installation

Clone the repository into the Codex skills directory using the skill name as the destination folder:

```bash
git clone git@github.com:korilin/liquid-glass-web-design-skill.git \
  "${CODEX_HOME:-$HOME/.codex}/skills/liquid-glass-web-design"
```

Restart or refresh Codex skill discovery after installation if the skill is not immediately visible.

To update an existing installation:

```bash
git -C "${CODEX_HOME:-$HOME/.codex}/skills/liquid-glass-web-design" pull --ff-only
```

## Usage

Invoke the skill explicitly with `$liquid-glass-web-design`, or let Codex select it automatically for a matching web UI task.

Example prompts:

```text
Use $liquid-glass-web-design to build a responsive analytics dashboard with a photographic environment, a frosted data rail, and clear-glass controls.
```

```text
Use $liquid-glass-web-design to refactor this React interface into shared clear and frosted material primitives without changing its business behavior.
```

```text
Use $liquid-glass-web-design to review this page for material, nesting, state, color, accessibility, and performance violations. Report root causes and shared fixes.
```

## CSS foundation

[`assets/liquid-glass.css`](assets/liquid-glass.css) can be copied into a project or translated into its existing design system. It includes:

- dark and light backdrop-tone tokens;
- 4px, 6px, 8px, and 12px blur scales;
- clear, frosted, raised, and floating materials;
- cards, buttons, chips, inputs, popovers, menu items, dividers, and status indicators;
- hover, focus-visible, pressed, selected, disabled, and semantic states;
- backdrop-filter fallback and reduced-motion handling.

Minimal markup:

```html
<html data-lg-tone="dark">
  <link rel="stylesheet" href="/styles/liquid-glass.css">

  <section
    class="lg-card lg-material lg-stack"
    data-lg-material="frosted"
    data-lg-scale="card"
  >
    <h2 class="lg-text-primary">Workspace</h2>
    <p class="lg-text-secondary">A shared frosted card recipe.</p>

    <div class="lg-cluster">
      <button class="lg-button lg-material" data-lg-material="clear">
        Action
      </button>
      <button
        class="lg-chip lg-material"
        data-lg-material="clear"
        data-lg-selected="true"
        aria-pressed="true"
      >
        Selected
      </button>
      <span class="lg-status" data-lg-tone="success">Ready</span>
    </div>
  </section>
</html>
```

Treat this stylesheet as a reference foundation. When the target project already has tokens or components, merge the material roles into that system instead of maintaining two competing theme layers.

## Validation

Validate the skill structure after changes:

```bash
python3 "${CODEX_HOME:-$HOME/.codex}/skills/.system/skill-creator/scripts/quick_validate.py" .
```

Also verify that all Markdown references resolve and render the CSS foundation over dark, bright, mixed, and low-detail backgrounds before changing shared optical tokens.
