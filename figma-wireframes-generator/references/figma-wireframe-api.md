# Figma Wireframe API Notes

Load this reference only when writing JavaScript for `use_figma`.

## Setup

- Use `await figma.loadFontAsync({ family: "Inter", style: "Regular" })` before creating text.
- Use `await figma.loadFontAsync({ family: "Inter", style: "Medium" })` or `"Semi Bold"` only if needed.
- Do not set `figma.currentPage` directly. Use `await figma.setCurrentPageAsync(page)` when changing pages.
- Prefer deterministic names: `Wireframes`, `Components`, `Landing`, `Pricing`, `Thank You`.

## Variables

Create or reuse a collection named `Wireframe`. Add a mode named exactly `desktop`. Define number variables:

- `columns = 12`
- `breakpoint = 1280`
- `margin = 60`
- `gutter = 20`

If existing variables with these names exist in the collection, update their desktop values instead of duplicating them.

## Layout Grid

Apply this grid to each 1280 px page frame:

```js
frame.layoutGrids = [{
  pattern: "COLUMNS",
  sectionSize: 1,
  visible: true,
  color: { r: 0.2, g: 0.2, b: 0.2, a: 0.12 },
  alignment: "STRETCH",
  gutterSize: 20,
  offset: 60,
  count: 12
}];
```

Create a grid style named `Wireframe / Desktop 12 Columns` and assign it to frames when possible. If style creation is unsupported in the current context, apply the grid object directly to each frame.

## Auto Layout

Use vertical auto layout for page frames:

```js
frame.layoutMode = "VERTICAL";
frame.primaryAxisSizingMode = "AUTO";
frame.counterAxisSizingMode = "FIXED";
frame.itemSpacing = 0;
frame.resize(1280, frame.height);
```

Use centered section containers:

```js
section.layoutMode = "VERTICAL";
section.counterAxisAlignItems = "CENTER";
section.primaryAxisSizingMode = "AUTO";
section.counterAxisSizingMode = "FIXED";
section.resize(1280, section.height);
```

Inside each section, create an inner content frame with fixed width `1280 - 60 * 2 = 1160` unless the user asks for a different container. Center it in the section.

## Text

Create text using supplied copy only. Keep text hug-like:

```js
text.textAutoResize = "WIDTH_AND_HEIGHT";
text.characters = suppliedText;
```

If long body copy needs readable wrapping, use `text.textAutoResize = "HEIGHT"` and set a fixed width on the text node within an auto-layout content area.

## Components

Create components before pages:

- `Header / Wireframe`
- `Footer / Wireframe`
- `Button / Wireframe`

Use `component.createInstance()` for every page occurrence. Do not detach instances.

Use simple gray fills:

- page background `#FFFFFF`
- section placeholder `#F2F2F2`
- component fill `#E6E6E6`
- strokes `#BDBDBD`
- text `#1F1F1F`

## Final Check

Before ending the `use_figma` script, inspect generated page frames:

- each page has layout grids
- each page uses vertical auto layout
- header/footer/button occurrences are instances
- page width is 1280
- no obvious text node has empty generated filler such as lorem ipsum
