# Components

Choose a component from its behavior and information role, not its visual resemblance.

## Layout and Navigation

- Use a sidebar for persistent top-level collections or destinations.
- Use split views for adjacent regions that users may resize or hide.
- Use lists and tables for scannable structured data; support selection, sorting, disclosure, and keyboard navigation as appropriate.
- Use outline or column views for hierarchy when parent-child context matters.
- Use tabs for a small set of peer views, not as a substitute for deep navigation.
- Use path controls when location within a file or hierarchy is actionable.

## Actions and Menus

- Use buttons for immediate actions and clearly distinguish default, cancel, destructive, toggle, and disclosure behavior.
- Use a pop-up button to choose one value from a menu; use a pull-down button to expose actions.
- Keep contextual menus supplementary. Never hide an essential command exclusively in a contextual menu.
- Use toolbar items for frequent window actions and preserve menu-bar access to commands.

## Presentation

- Use windows for independent workspaces, sheets for window-scoped decisions, panels for persistent utilities, popovers for transient contextual content, and alerts for significant conditions.
- Avoid action sheets and mobile presentation patterns when a standard macOS menu, popover, sheet, or alert is more appropriate.
- Use scroll views without hiding essential controls or creating nested scrolling conflicts.

## Selection and Input

- Use text fields for editable text, combo boxes when entry and suggested values both matter, and token fields for discrete editable items.
- Use checkboxes for independent options, radio-style choices for one item in a visible small set, and pop-up buttons for compact single selection.
- Use segmented controls for a small number of closely related modes or views.
- Use sliders for continuous or approximate values and steppers for small incremental changes. Provide direct entry when precision matters.
- Use color and image wells for standard selection and drag-and-drop behavior rather than custom swatches without system semantics.

## Content and Status

- Use native text views for editing semantics, selection, spelling, substitutions, accessibility, and services.
- Use progress indicators for ongoing work and reserve gauges or ratings for values their visual models accurately represent.
- Design charts with labels, accessible descriptions, non-color differentiation, and interaction appropriate to precise pointer input.

## Selection Procedure

1. Define the information or action model.
2. Identify the closest standard macOS component.
3. Check its current platform availability and behavior in the exact Apple HIG topic.
4. Prefer the native component unless it cannot support a core requirement.
5. If custom behavior is necessary, preserve semantics, focus, keyboard interaction, accessibility, and state communication.

## Apple Topics

Start with [Components](https://developer.apple.com/design/human-interface-guidelines/components), then open the exact topic under content, layout and organization, menus and actions, navigation and search, presentation, selection and input, or status.
