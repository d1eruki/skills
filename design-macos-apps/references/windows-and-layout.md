# Windows and Layout

## Window Model

Choose the window model from the product's objects and workflows, not from visual preference.

- Use independent windows when users benefit from arranging or comparing separate documents, workspaces, or content views.
- Use auxiliary panels or inspectors for controls that need to remain available while the main content stays interactive.
- Use sheets for focused tasks tied to a specific window.
- Use app-modal presentation only when proceeding elsewhere would be unsafe or meaningless.

Support resizing across a useful range. Define intentional behavior for minimum size, expanded layouts, split views, sidebars, inspectors, toolbars, and content overflow. Avoid layouts that merely stretch empty space or clip essential controls.

Restore meaningful window size, placement, visibility, and view state when appropriate. Account for removed displays and changed resolutions rather than restoring windows offscreen.

## Information Architecture

- Use the available display area to reduce unnecessary hierarchy and modality.
- Keep primary content dominant and supporting navigation or inspectors visually subordinate.
- Prefer sidebars for persistent top-level destinations or collections when that structure matches the app.
- Prefer inspectors for properties of the current selection or document.
- Keep controls near the content they affect, while placing global commands in predictable app-level locations.
- Make empty, loading, unavailable, and no-selection states informative and actionable.

## Toolbars

Use a toolbar for frequent, window-relevant actions and modes. Keep all commands discoverable through menus even when duplicated in the toolbar. Support customization when users have varied recurring workflows and the underlying framework permits it.

Avoid filling the toolbar with every available action. Group related items, maintain stable placement, use clear labels or recognizable symbols, and show state for toggles or modes.

## Full Screen and Multiple Displays

Support full screen when it creates a useful focused workspace. Do not rely on full screen to compensate for a layout that fails at ordinary window sizes. Preserve access to essential commands and make transitions reversible and state-preserving.

Test windows across multiple displays, display scaling settings, and changes in the available screen configuration.

## Review Checks

- Can users resize and arrange the workspace to match their task?
- Does content reflow rather than simply scale or clip?
- Is modality limited and scoped to the correct window?
- Are toolbar actions frequent and window-relevant?
- Are navigation, content, and inspection roles visually clear?
- Does the app recover safely from display changes?

## Related Apple Guidance

Consult the current HIG pages linked from [Designing for macOS](https://developer.apple.com/design/human-interface-guidelines/designing-for-macos), especially full-screen behavior and relevant component guidance.
