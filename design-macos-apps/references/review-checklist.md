# macOS HIG Review Checklist

Use this checklist as a reasoning aid, not as a claim of formal certification. Mark items as `pass`, `issue`, `not applicable`, or `not observable`.

## Product Model

- Primary objects and tasks are identifiable.
- Window and document behavior matches the product model.
- Quick tasks and sustained workflows are both supported.
- App state survives activation changes and expected relaunch scenarios.

## Layout and Windows

- The hierarchy uses large displays effectively without excessive density.
- Windows have useful minimum, default, and expanded layouts.
- Resizing, multiple windows, full screen, and multiple displays behave intentionally.
- Navigation, primary content, and inspectors have distinct roles.
- Modality is limited and scoped correctly.
- Empty, loading, error, and no-selection states are designed.

## Visual Foundations

- Semantic colors, system materials, typography, and SF Symbols are used appropriately.
- Light, dark, increased-contrast, and reduced-transparency appearances remain legible.
- Liquid Glass or vibrancy is framework-provided and does not reduce content clarity.
- Motion explains state and respects Reduce Motion.
- Labels and writing are concise, consistent, and localizable.

## Commands and Input

- The menu bar exposes the complete command set.
- Frequent window commands are appropriately available in the toolbar.
- Standard shortcuts and editing behaviors are preserved.
- Core workflows support keyboard-only operation.
- Pointer interactions provide hover, focus, selection, drag, drop, and cursor feedback.
- Commands remain consistent across menus, toolbars, contextual menus, and inline controls.

## Personalization and State

- Repeated-work preferences are preserved when appropriate.
- Toolbar or workspace customization is supported when it has clear user value.
- Active, inactive, focused, selected, disabled, and destructive states are distinguishable.
- User-controlled window arrangement is respected.

## Patterns and Components

- Files, autosave, export, drag and drop, and undo follow expected system behavior where relevant.
- Search, Settings, onboarding, help, accounts, and permission requests appear in the correct context.
- Loading, progress, cancellation, errors, and recovery are communicated accurately.
- Standard components are chosen by behavior rather than visual resemblance.
- Alerts, sheets, panels, popovers, menus, and windows use appropriate scope and modality.
- Sharing, collaboration, printing, notifications, and media use system facilities when relevant.

## Accessibility and Adaptation

- Controls expose semantic roles, names, values, and actions.
- Focus order is logical and focus is visible.
- Meaning is not conveyed by color alone.
- Light and dark appearances remain legible.
- Increased contrast, reduced motion, text expansion, and localization are considered.
- VoiceOver and keyboard navigation are tested for primary workflows.
- Localization, text expansion, and right-to-left behavior are tested where supported.
- Sensitive data is minimized and protected in permissions, previews, notifications, and integrations.

## System Integrations

- Each integration solves a real workflow and uses standard system surfaces.
- Signed-out, offline, denied, unavailable, expired, and conflict states are designed.
- Payments, identity, synchronization, AI, sharing, widgets, and notifications communicate consequences clearly.
- Mac Catalyst experiences add Mac-specific menus, windows, keyboard, pointer, and density behavior.

## Reporting Template

```text
[priority] Short finding title
Issue: Observable problem.
Impact: User and workflow consequence.
Recommendation: Specific macOS-native correction.
Evidence: Artifact location and relevant Apple guidance.
```

End the review with assumptions, unobservable areas, and the highest-risk test gaps.
