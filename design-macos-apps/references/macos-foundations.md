# macOS Foundations

## Platform Context

Design for a spacious, high-resolution workspace that may span multiple displays. Assume people can spend hours in the app, keep several apps visible, and switch frequently between active and inactive contexts.

Mac input is combinational: keyboard, trackpad, mouse, game controls, accessibility technologies, and voice can coexist. Do not make a core workflow depend exclusively on touch-like gestures or pointer interaction.

## Core Heuristics

- Show enough context to support deep work without overwhelming the screen.
- Favor stable spatial organization so users can build muscle memory.
- Keep persistent app structure distinct from transient task state.
- Use familiar macOS terminology, symbols, control behavior, and command ordering.
- Preserve user control over windows, views, data, and repeated workflows.
- Allow quick tasks and sustained sessions to use the same coherent model.
- Handle activation changes gracefully; do not discard selection, edits, or context merely because another app becomes active.

## Native Feel

A native-feeling app is defined more by behavior than decoration. Prioritize system-consistent focus, selection, menus, keyboard navigation, window management, drag and drop, undo, copy and paste, state restoration, and accessibility before visual novelty.

Use system materials, typography, colors, controls, and symbols when appropriate. Custom presentation is acceptable when it clarifies the product's identity or domain, but custom controls must preserve expected semantics and states.

## Questions to Resolve

- What are the primary objects users create, open, select, edit, or organize?
- Is the app document-based, library-based, utility-like, or a collection of independent workspaces?
- Which information must remain visible while users act?
- Which operations deserve direct manipulation, a toolbar item, a menu command, or an inspector?
- What must survive relaunch, window closure, display changes, and activation changes?
- Which workflows need keyboard-only completion?

## Authority

Start with [Designing for macOS](https://developer.apple.com/design/human-interface-guidelines/designing-for-macos). Recheck the official page for current platform changes before making time-sensitive claims.
