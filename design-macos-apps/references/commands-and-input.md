# Commands and Input

## Menu Bar

Treat the menu bar as the complete, stable command map for the app. Place commands in conventional menus and ordering when established macOS conventions exist. Keep menu titles and command names concise, specific, and consistent with labels elsewhere.

Reflect context in command availability and state. Disable unavailable commands when their presence remains informative; hide commands only when they are irrelevant or would create confusion. Show standard keyboard shortcuts in menus.

## Keyboard

- Provide shortcuts for frequent and conventional actions.
- Preserve standard shortcuts unless the product has an exceptional, well-tested reason to override them.
- Support keyboard navigation, focus movement, selection, activation, cancellation, and confirmation.
- Make focus visible without relying solely on color.
- Avoid requiring memorized shortcuts for discoverability; expose commands through menus and controls too.
- Ensure text editing respects standard selection, copy, paste, undo, redo, and deletion behavior.

## Pointer and Precision

Assume a high-precision pointer. Provide appropriate hover, selection, resize, drag, drop, contextual menu, and cursor feedback. Make targets comfortable without imitating oversized touch interfaces throughout the app.

For direct manipulation, clarify what is selectable, draggable, editable, and droppable. Preserve precise control and offer keyboard modifiers only when they complement a discoverable base interaction.

## Command Consistency

The same operation may appear in a menu, toolbar, contextual menu, Touch Bar replacement surface, or inline control. Keep its name, symbol, enabled state, destructive character, shortcut, and result consistent across locations.

Support undo and redo for user-authored changes whenever technically and conceptually feasible. Before irreversible destructive actions, prefer recovery mechanisms or clear confirmation proportional to the risk.

## Review Checks

- Can every important command be found in the menu bar?
- Can primary workflows be completed without a pointer?
- Do standard shortcuts behave as Mac users expect?
- Are focus, hover, selection, drag, drop, and disabled states clear?
- Are contextual commands scoped to the current object or selection?
- Are destructive and reversible operations distinguished correctly?

## Related Apple Guidance

Use the current [Designing for macOS](https://developer.apple.com/design/human-interface-guidelines/designing-for-macos) links for menu bar, keyboards, pointing devices, file management, and Dock menus.
