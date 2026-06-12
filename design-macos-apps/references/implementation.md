# Implementation Guidance

## Framework Choice

- Follow the framework already established by the project unless migration is part of the task.
- Use SwiftUI for declarative composition and system adaptation where its APIs satisfy the required behavior.
- Use AppKit when the app needs mature document architecture, advanced text, precise window control, complex tables or outlines, or behavior unavailable in SwiftUI.
- Bridge frameworks deliberately and keep ownership of state, focus, commands, and lifecycle clear.

## Map Design to System APIs

- Represent app commands with the framework command and menu APIs rather than custom in-window replicas.
- Use scene and window APIs for multiwindow behavior, restoration, Settings, and document workflows.
- Use system panels for open, save, print, color, font, and sharing tasks.
- Use semantic controls and accessibility modifiers before custom drawing.
- Use system materials, text styles, symbols, focus, keyboard shortcuts, drag and drop, undo management, and pasteboard APIs.

## Implementation Review

- Check minimum deployment targets and API availability before recommending a current design-system feature.
- Verify that menu enabled state, toolbar state, selection, focus, and model state share one source of truth.
- Avoid fixed frame assumptions that fail under window resizing, localization, accessibility, or differing content.
- Persist user-facing workspace preferences separately from transient UI state.
- Test inactive windows, reopened documents, multiple scenes, multiple displays, denied permissions, offline behavior, and interrupted tasks.

## Mac Catalyst

Audit Catalyst apps for mobile assumptions: oversized controls, missing menu commands, single-window constraints, hidden hover state, absent contextual menus, touch-only gestures, and navigation bars used where Mac sidebars or toolbars fit better.

## Source Checks

Use current SwiftUI, AppKit, and Mac Catalyst developer documentation alongside HIG. Do not infer API availability from HIG illustrations alone.
