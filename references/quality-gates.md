# Quality Gates

## Required review matrix

Inspect representative screens under all applicable conditions:

| Dimension | Required samples |
|---|---|
| Background | dark detailed, bright detailed, mixed high-contrast, low-detail |
| Width | wide desktop, minimum supported desktop, tablet/narrow, phone if supported |
| State | rest, hover, focus-visible, pressed, selected, disabled, error/success |
| Content | short, long, empty, loading, overflow |
| Motion | normal and reduced motion |
| Browser | every supported engine with and without backdrop-filter fallback |

One attractive screenshot over one dark background is not sufficient validation.

## Material gates

- [ ] Clear glass remains recognizably transparent.
- [ ] Frosted glass still reveals the environment.
- [ ] No surface uses a saturated default tint.
- [ ] Edge highlight stays at the boundary.
- [ ] No large white or black patch dominates a card.
- [ ] Blur follows the 4/6/8/12px scale unless an exception is documented.
- [ ] Large panels do not become more opaque merely because they are large.
- [ ] Fallback is usable and visually related.

## Composition gates

- [ ] No unnecessary same-material card nesting.
- [ ] Persistent optical depth is at most two levels locally.
- [ ] Popovers are not clipped and remain visually connected to triggers.
- [ ] Dividers are inset or edge-faded.
- [ ] Independent regions have independent scrolling when the workflow needs it.
- [ ] Responsive changes follow available content width.
- [ ] Background focal content remains useful at every aspect ratio.

## Component gates

- [ ] Same component and variant render consistently everywhere.
- [ ] Hover is distinguishable from selected.
- [ ] Focus-visible is clearly visible without hover.
- [ ] Disabled state does not react to pointer hover/press.
- [ ] Semantic states use icon/text or shape in addition to color.
- [ ] Menu and trigger share the same component language.
- [ ] Dense lists do not apply expensive glass to every row without need.

## Color and emphasis gates

- [ ] Primary and secondary text remain readable over representative background samples.
- [ ] Muted text is subordinate but not washed out.
- [ ] Accent has a defined role and does not appear on every boundary.
- [ ] Success/danger glows are localized.
- [ ] Neutral, absent, and disabled states do not glow.
- [ ] No region contains competing glow families.
- [ ] Large semantic surfaces use low-alpha veils rather than solid fills.

## Accessibility gates

- [ ] Composited text contrast meets the product's WCAG target.
- [ ] Keyboard order and focus restoration are correct.
- [ ] Pointer targets meet the product's input requirements.
- [ ] Reduced-motion behavior removes decorative motion.
- [ ] Native semantics or equivalent ARIA are present.
- [ ] State and errors are understandable without color.

## Performance gates

- [ ] Rapid list scrolling does not show blank or delayed items.
- [ ] Opening a menu or modal does not cause a visible frame stall.
- [ ] Background motion does not compete with scroll.
- [ ] No continuous animation targets blur, displacement, or large shadows.
- [ ] Filtered surfaces are consolidated where possible.
- [ ] CPU/GPU use is checked on representative hardware when advanced effects are present.

## Severity

| Severity | Meaning | Examples |
|---|---|---|
| Blocker | Material or interaction is functionally wrong | unreadable text, clipped menu, inaccessible focus, severe jank |
| Major | Breaks the visual system | opaque “glass,” nested double frames, selected indistinguishable from hover |
| Minor | Local inconsistency | radius mismatch, overly long transition, divider touches edge |

Fix blocker and major issues before delivery. Do not hide a system defect with a page-specific override.

## Review report

Report each issue as:

```text
[severity] category — component/state
Evidence: observable behavior and context
Rule: violated system rule
Correction: shared token, material, component, or layout change
```

Prefer a small number of root-cause corrections over a long list of isolated pixel adjustments.
