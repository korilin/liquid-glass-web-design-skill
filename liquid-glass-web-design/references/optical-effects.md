# Optical Effects

Read this reference only when the requested result requires visible refraction, distortion, caustics, or a three-dimensional droplet effect.

## Browser reality

`backdrop-filter: blur()` softens and color-adjusts content behind a surface. It does not physically refract, magnify, or displace the backdrop. Borders and highlights can imply a thin glass boundary, but they cannot create true optical displacement.

Do not claim that ordinary CSS blur is refraction. Choose an effect level based on the requested fidelity and performance budget.

## Effect levels

| Level | Technique | Use | Avoid |
|---|---|---|---|
| 1 | CSS backdrop blur + edge optics | Most product cards and controls | Calling it physical refraction |
| 2 | Static SVG displacement/filter | One hero control, logo, or isolated focal surface | Lists, scrolling grids, many repeated items |
| 3 | Canvas/WebGL background sampling | Demonstrations, hero scenes, specialized visual products | Routine management UI and low-power devices |

## CSS edge optics

Create depth through an edge-only gradient, one inner highlight, and a soft shadow. Keep the interior clear. The bundled CSS uses a masked pseudo-element so highlights remain at the boundary rather than becoming a white block.

Use pointer-relative highlights only when they are inexpensive and input-relevant. Update CSS variables through a throttled pointer handler; disable on touch and reduced motion. Static directional highlights are preferred for dense applications.

## SVG displacement

Use SVG displacement only for isolated surfaces where the backdrop can be captured or represented correctly. A filter attached to the foreground element usually distorts that element, not arbitrary content behind it.

Constraints:

- displacement scale normally 2–8px for interface glass;
- use a low-frequency map without obvious stripes;
- keep the map static unless motion is essential;
- clip precisely to the surface radius;
- provide a CSS fallback;
- test text legibility and pointer hit regions independently from the visual filter.

Reject displacement maps that create repeated bands, hard contour lines, or chromatic noise unrelated to the environment.

## Canvas or WebGL

True dynamic refraction requires sampling the environment into a renderable texture and displacing samples through a normal or height field.

Use it only when:

- the environment is controlled by the same renderer or can be captured legally and efficiently;
- the surface count is small;
- the visual effect is central to the product;
- a static or CSS fallback is acceptable;
- frame time is measured on target hardware.

Do not render a separate WebGL scene for every button or card. Use a shared scene or texture and composite only a few focal surfaces.

## Three-dimensional glass

A 3D droplet requires geometry, thickness, environment lighting, normals, roughness, and refraction/IOR—not stacked CSS rectangles. Typical physical starting points:

- IOR: 1.33–1.5;
- transmission: near 1;
- roughness: 0.05–0.25;
- thickness: proportional to visible curvature;
- environment map with bright and dark features.

This is a different visual mode from the restrained product material system. Do not mix full 3D droplets into every management control. Reserve them for branding, hero visuals, or a single focal interaction.

## Motion

Liquid appearance does not require constant flow. Prefer static curvature and optical response. When motion is necessary, make it event-driven:

- hover: local highlight shift;
- press: small compression;
- selection: one short settling transition;
- live process: restrained pulse with reduced-motion fallback.

Never animate the entire material continuously merely to make it look liquid.
