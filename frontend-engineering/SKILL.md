---
name: frontend-engineering
description: Implement, review, or diagnose frontend application work involving components, CSS, Tailwind, themes, color tokens, responsive layouts, accessibility, effects, or localization. Use existing project conventions when they are available.
---

# Frontend Engineering

## Diagnose Active Runtime Behavior

When observed behavior contradicts the expected code path, confirm the active runtime source instead of relying on static inspection alone. Treat visually similar CSS, browser, and JavaScript effects as separate hypotheses.

Where practical, verify:

- Active state classes, attributes, media-query results, and feature-detection results.
- Activated conditional branches and dynamic imports.
- The code or stylesheet controlling the relevant DOM property, CSS variable, inline style, or computed style.
- Whether the behavior is owned by a library, the browser, or project code.

For capability-gated behavior, trace the path from detection through resolved application state and initialization to the final observable result. Keep independent causes separate during diagnosis, while making consumers depend on one resolved state when they require identical behavior. Clearly distinguish confirmed causes from unverified hypotheses.

## Follow Existing Component Patterns

Before styling or structuring a component, inspect nearby components that solve a similar task. Reuse their complete applicable pattern: utilities, typography, spacing, controls, interaction states, theme tokens, and breakpoints.

Prefer extending or composing an established pattern over introducing component-specific CSS, arbitrary values, or a parallel mechanism. Keep a one-off element in its nearest semantic parent unless extraction creates a meaningful reusable or independently owned component.

Before creating state flow, persistence, routing, data loading, or another shared mechanic, search for an equivalent helper, composable, store, or established lifecycle and reuse or extend it when its contract fits.

## Derive Responsive Layouts

Derive responsive behavior from layout topology rather than treating each breakpoint as an isolated design.

When cards share a horizontal row:

- Keep outer heights equal when the design calls for a uniform row.
- Align corresponding headings, prices, dividers, lists, and actions.
- Let flexible content regions absorb differences in content length.

When cards stack vertically:

- Size each card by its own content.
- Remove equal-height constraints and unnecessary empty space.
- Preserve consistent external spacing.

Equal outer heights are insufficient when corresponding internal sections remain misaligned.

## Calculate Nested Corners

Calculate an inner radius as `max(0, outer radius - distance between contours)`. When horizontal and vertical insets differ, calculate each radius axis separately. Include padding, gap, and border thickness in the contour distance. Use an existing radius token when it exactly matches the result.

## Prefer Framework and Library Primitives

Use a framework's documented APIs and established project patterns before custom workarounds. For Tailwind projects, prefer built-in utilities, theme tokens, CSS variables, and variants over custom CSS or hardcoded values.

Use canonical utilities when the framework covers the requirement. Avoid complex arbitrary calculations when normal sizing, padding, flex, or grid can resolve the layout. Add custom utilities or theme tokens only when built-in behavior is insufficient or the value is a deliberate project token.

Implement layout, spacing, sizing, colors, typography, responsive behavior, borders, and shadows in component templates with utilities by default when that is the project's established approach.

## Maintain Layered Color Systems

Treat a color change as a change to one connected system. When the project uses layered color tokens, audit the affected path with these columns before proposing a cross-cutting change:

```text
role | light | dark | semantic token | component token | utility | consumers | states | background
```

Trace affected values from palette primitives through semantic and component tokens to their consumers. Check supported themes and existing default, hover, active, focus, and disabled states. Mark unverified assumptions and identify direct primitives, layer bypasses, mixed terminology, stale aliases, unused tokens, and colors evaluated against the wrong background.

Keep dependencies layered:

- Define semantic tokens from palette primitives.
- Name semantic tokens for reusable visual roles rather than concrete colors or page locations.
- Define component tokens from semantic tokens when a component-specific role is needed.
- Consume established component tokens instead of bypassing them with lower-level values.
- Keep reusable component states inside the component; expose a prop or variant when a parent must select them.

Use one vocabulary across the chain. Paired colors should describe a surface and its content. Reserve `muted` for enabled low-priority content and `disabled` for unavailable controls or content. Do not use raw palette utilities in application code when the project has an established semantic token layer.

Prefer utilities and existing tokens over component-specific selectors. When custom CSS is necessary, identify the missing framework capability and keep the exception local.

## Preserve Accessibility and Localization

Add appropriate accessibility attributes to icons and SVGs, including `aria-hidden` and `focusable` for decorative graphics. Give icon-only or ambiguous controls an accessible name, and keep image alternatives accurate.

Write toggle labels as the action or alternative state applied after activation rather than merely repeating the current state.

Keep equivalent interface copy consistent across locales unless a language-specific convention requires a difference. When adding or changing a localization key or variable, update every supported locale in the same change.
