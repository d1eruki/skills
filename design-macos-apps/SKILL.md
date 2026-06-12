---
name: design-macos-apps
description: Design, implement, and review native-feeling macOS app interfaces using Apple's Human Interface Guidelines. Use for macOS UX architecture, visual foundations, SwiftUI, AppKit, or Mac Catalyst decisions, windows, navigation, components, menus, keyboard and pointer interaction, files, settings, onboarding, accessibility, localization, privacy, system integrations, and HIG audits of designs, screenshots, specifications, prototypes, or code.
---

# Design macOS Apps

Apply macOS conventions without turning the interface into a generic desktop template. Preserve the product's purpose while making behavior predictable to Mac users.

## Workflow

1. Identify the task: create, implement, critique, or migrate a macOS experience.
2. Establish the app's primary tasks, document model, expected session length, window model, and required input methods.
3. Read only the references relevant to the task:
   - Read [macos-foundations.md](references/macos-foundations.md) for every task.
   - Read [visual-foundations.md](references/visual-foundations.md) for color, materials, Liquid Glass, typography, icons, imagery, motion, or writing.
   - Read [windows-and-layout.md](references/windows-and-layout.md) for navigation, layout, windows, panels, toolbars, or full-screen behavior.
   - Read [commands-and-input.md](references/commands-and-input.md) for menus, commands, keyboard, pointer, selection, or editing workflows.
   - Read [patterns-and-workflows.md](references/patterns-and-workflows.md) for files, loading, search, settings, onboarding, accounts, help, notifications, sharing, printing, media, or undo.
   - Read [components.md](references/components.md) when choosing or reviewing specific controls and presentation containers.
   - Read [accessibility-localization-privacy.md](references/accessibility-localization-privacy.md) for accessibility, inclusion, localization, right-to-left layout, permissions, or sensitive data.
   - Read [system-integrations.md](references/system-integrations.md) for iCloud, Sign in with Apple, Siri, App Shortcuts, widgets, notifications, payments, sharing, AI, or Mac Catalyst.
   - Read [implementation.md](references/implementation.md) when translating design decisions into SwiftUI, AppKit, or Mac Catalyst.
   - Read [review-checklist.md](references/review-checklist.md) when auditing an existing interface or before finalizing a design.
4. Inspect existing product and code conventions before proposing changes. Prefer system components and established project patterns when they satisfy the requirement.
5. Produce concrete decisions. Specify hierarchy, window behavior, command placement, shortcuts, states, accessibility behavior, and implementation implications where relevant.
6. Verify current guidance on official Apple documentation when the answer depends on recently changed platform behavior or when delivering a formal compliance review.

## Scope Rules

- Treat the references as a macOS-focused decision guide, not a substitute for the complete HIG.
- Apply only guidance relevant to macOS and the technologies the product actually uses.
- Follow links to the exact Apple topic before making a component-specific, version-specific, or compliance claim.
- Distinguish a platform convention, an accessibility requirement, a product recommendation, and an optional refinement.
- State which HIG areas were reviewed and which were not observable.

## Design Priorities

- Use the large display to expose useful context and reduce unnecessary navigation depth.
- Keep information density comfortable; more visible content must not mean smaller, harder-to-scan content.
- Treat windows as user-managed workspace objects. Support resizing and state restoration when appropriate.
- Put the complete command set in the menu bar, even when common commands also appear in toolbars or contextual controls.
- Make keyboard and precise pointer workflows first-class, not secondary adaptations.
- Reduce modal interruptions. Prefer direct manipulation, inspectors, popovers, sheets, and modeless workflows when they preserve clarity.
- Support personalization where it improves repeated work, including toolbar configuration, window arrangement, and view preferences.
- Design active, inactive, focused, selected, disabled, loading, empty, and error states explicitly.
- Preserve platform accessibility, localization, appearance, motion, and input settings.

## Review Output

Lead with actionable findings, ordered by severity. For each finding include:

- **Issue:** Describe the observable behavior or design decision.
- **Impact:** Explain the user cost and affected workflow.
- **Recommendation:** Give a specific macOS-native correction.
- **Priority:** Use `critical`, `high`, `medium`, or `low`.
- **Evidence:** Point to the relevant artifact and official Apple guidance when available.

Separate confirmed HIG conflicts from product tradeoffs and optional refinements. Do not claim formal Apple compliance when only a partial artifact was reviewed.

## Implementation Guidance

- Translate recommendations into the framework already used by the project, typically SwiftUI or AppKit.
- Prefer semantic system APIs and controls over custom replicas.
- Do not invent exact dimensions when Apple provides no fixed requirement. Explain the layout relationship and adaptive behavior instead.
- Avoid applying iPhone navigation patterns to macOS without a task-specific reason.
- Keep destructive actions explicit, reversible where possible, and consistent across menus, toolbars, contextual menus, and shortcuts.
- Test resizing, multiple windows, multiple displays, keyboard-only operation, pointer precision, VoiceOver, increased contrast, reduced motion, and light/dark appearances as relevant.

## Sources

Use Apple's current documentation as the authority:

- [Designing for macOS](https://developer.apple.com/design/human-interface-guidelines/designing-for-macos)
- [Foundations](https://developer.apple.com/design/human-interface-guidelines/foundations)
- [Patterns](https://developer.apple.com/design/human-interface-guidelines/patterns)
- [Components](https://developer.apple.com/design/human-interface-guidelines/components)
- [Inputs](https://developer.apple.com/design/human-interface-guidelines/inputs)
- [Technologies](https://developer.apple.com/design/human-interface-guidelines/technologies)
- [Apple Design Resources](https://developer.apple.com/design/resources/#macos-apps)

Summarize and apply the guidance. Do not reproduce long passages from Apple documentation.
