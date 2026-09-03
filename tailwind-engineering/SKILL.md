---
name: tailwind-engineering
description: Implement, review, or diagnose Tailwind CSS styling, including utilities, variants, theme tokens, responsive behavior, dynamic classes, and justified custom CSS. Use only when the target project actually uses Tailwind CSS.
---

# Tailwind Engineering

## Establish the Active Tailwind Setup

Inspect the installed Tailwind version, CSS entrypoints, configuration, plugins, theme definitions, and nearby templates before editing. Follow the project's active configuration style and do not assume that syntax or defaults from another Tailwind release apply.

## Prefer Utilities and Existing Tokens

Prefer built-in utilities, project theme tokens, CSS variables, and variants over custom CSS or hardcoded values. Use canonical utilities when Tailwind directly covers the requirement, and do not duplicate framework defaults for breakpoints, spacing, colors, typography, shadows, radii, transitions, or stacking values.

Implement layout, spacing, sizing, colors, typography, responsive behavior, borders, and shadows with utilities in templates when that is the established project approach. Use normal sizing, padding, flex, and grid before introducing complex arbitrary calculations.

Prefer whole numeric values in authored utilities and theme tokens. Avoid fractional values when whole values can express the intended design without meaningful loss. When a fractional value is genuinely necessary, use no more than one digit after the decimal point.

When the project has a semantic color-token layer, consume its established utilities instead of raw palette classes or lower-level values. Keep state styling in the component through supported variants when possible.

## Keep Classes Discoverable

Use complete class names in source or explicit mappings recognized by the project's Tailwind build. Do not construct class fragments dynamically when that prevents the compiler from discovering the resulting utilities; use an established safelist only when explicit mappings are insufficient.

## Justify Custom Extensions

Add an arbitrary value, custom utility, theme token, plugin, or component-specific selector only when built-in utilities and existing project tokens cannot express the requirement. Identify the missing Tailwind capability, keep the exception local, and avoid extending custom CSS when variants or utilities already cover the affected state.
