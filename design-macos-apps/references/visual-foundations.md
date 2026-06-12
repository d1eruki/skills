# Visual Foundations

Use current system styling as a behavioral and semantic system, not as decoration to imitate manually.

## Color and Appearance

- Use semantic system colors so appearance, contrast, vibrancy, and accessibility settings can adapt automatically.
- Verify light and dark appearances independently; do not derive one by mechanically inverting the other.
- Reserve accent color for emphasis, selection, and interactive meaning. Do not use it as the only status signal.
- Test increased contrast, reduced transparency, inactive windows, disabled controls, and different wallpapers behind translucent materials.

## Materials and Liquid Glass

- Prefer framework-provided materials and controls. Do not recreate Liquid Glass or vibrancy with static blur, gradients, borders, and shadows.
- Use translucent or glass-like surfaces to establish hierarchy and preserve context, not behind dense reading or editing content when it harms legibility.
- Keep content visually primary. Avoid stacking multiple decorative materials that compete for attention.
- Recheck current Apple guidance and deployment-target behavior before specifying new design-system APIs.

## Typography and Writing

- Prefer system text styles and native font behavior. Support localization, text expansion, accessibility settings, and font substitution where users can choose fonts.
- Build hierarchy through role, weight, spacing, and placement rather than many arbitrary sizes.
- Use sentence-style capitalization unless a standard macOS label requires otherwise.
- Write concise action labels that describe the result. Avoid vague labels such as `OK` when a specific verb is clearer.
- Keep terminology consistent across controls, menus, help, and documentation.

## Icons, SF Symbols, and Imagery

- Prefer SF Symbols for familiar system actions and statuses. Match symbol variant, weight, scale, and rendering mode to its context.
- Pair unfamiliar symbols with labels. Do not repurpose a conventional symbol for an unrelated action.
- Keep app icons distinctive, simple at small sizes, and consistent with current macOS icon templates and export requirements.
- Provide image alternatives and avoid embedding important text in images.

## Motion

- Use motion to explain causality, continuity, hierarchy, or state change.
- Keep frequent transitions restrained and interruptible.
- Respect Reduce Motion. Replace large spatial movement with fades or simpler state changes when needed.
- Do not delay access to content merely to complete an animation.

## Review Questions

- Are semantic colors and materials used instead of fixed appearance values?
- Is text legible over every material and window state?
- Do symbols communicate standard meanings and remain understandable without color?
- Does motion clarify an interaction and adapt to reduced-motion preferences?

## Apple Topics

[Color](https://developer.apple.com/design/human-interface-guidelines/color), [Dark Mode](https://developer.apple.com/design/human-interface-guidelines/dark-mode), [Materials](https://developer.apple.com/design/human-interface-guidelines/materials), [Typography](https://developer.apple.com/design/human-interface-guidelines/typography), [SF Symbols](https://developer.apple.com/design/human-interface-guidelines/sf-symbols), [Icons](https://developer.apple.com/design/human-interface-guidelines/icons), [Images](https://developer.apple.com/design/human-interface-guidelines/images), [Motion](https://developer.apple.com/design/human-interface-guidelines/motion), and [Writing](https://developer.apple.com/design/human-interface-guidelines/writing).
