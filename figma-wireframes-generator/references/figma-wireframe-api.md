# Figma Wireframe API Notes

Load this reference only when writing JavaScript for `use_figma`.

## Setup

- Use `await figma.loadFontAsync({ family: "Inter", style: "Regular" })` before creating text.
- Use `await figma.loadFontAsync({ family: "Inter", style: "Medium" })` or `"Semi Bold"` only if needed.
- Do not set `figma.currentPage` directly. Use `await figma.setCurrentPageAsync(page)` when changing pages.
- Prefer deterministic names: `Wireframes`, `Components`, `Landing`, `Pricing`, `Thank You`.

## Reference Style Matching

When the user asks to make a page consistent with another page, use that page as a strict visual reference, not loose inspiration.

Trigger phrases include:

- "in the style of"
- "like this page"
- "like the main page"
- "as the main page"
- "consistent with"
- "based on this page"
- "по примеру"
- "в стиле"
- "как главная"
- "консистентно с"

Before generating the new wireframe, inspect the reference frame and extract a style inventory:

- page width, content width, grid, margins, gutters
- section paddings, section gaps, section background fills
- typography roles: hero heading, section heading, section description, card title, card body, labels, CTA text, footer text, form label, input placeholder
- fills, strokes, stroke weights, corner radii, padding, gaps, and heights for cards
- button fills, strokes, radii, padding, text styles
- form field fills, strokes, radii, padding, text styles
- divider and placeholder styles
- header/footer component usage

Use literal values from the reference wherever a matching pattern exists. Do not approximate colors, strokes, radii, or spacing.

If the reference card has no stroke, the generated card must have no stroke. If the reference card has radius `8`, use radius `8`. If the reference section description uses a muted gray, use the same muted gray. If the reference card body uses a different gray, preserve that distinction.

Create a role map before building:

```text
source content role -> reference visual role
```

Examples:

- new section description -> reference section description style
- new card title -> reference card title style
- new card body -> reference card body style
- new process step -> reference process step card style
- new final CTA -> reference final CTA pattern

Do not invent new visual patterns when the reference page already contains a similar pattern. Reuse or clone existing components and instances when possible. If cloning is not practical, recreate the pattern with the same measured values.

Choose matching patterns:

- audience cards on a new page should use audience-card parameters from the reference when available
- process steps should use process-step parameters from the reference when available
- final CTA should use the final CTA pattern from the reference when available
- form fields should use the closest input/form pattern from the reference when available
- if no exact pattern exists, use the nearest low-fidelity surface style while preserving measured card/text parameters

When preserving source content, do not add semantic blocks, stats, benefits, CTA labels, labels, captions, decorative text, or placeholder copy that were not supplied by the user or present in the source page.

Structural validation is not enough. Run a visual parity check against the reference page before the final answer:

- card fills match
- strokes match
- corner radii match
- text colors match by role
- typography scale matches by role
- section spacing rhythm matches
- buttons match
- header/footer are reused or visually identical
- the new page does not look like a separate design system

Use screenshots for the reference page and the generated page when possible. Inspect the first screen, card sections, form section, FAQ, final CTA, and footer. If the new page differs in visual language, fix it before answering.

## Variables

Create or reuse a collection named `Wireframe`. Add a mode named exactly `desktop`. Define number variables:

- `columns = 12`
- `breakpoint = 1280`
- `margin = 60`
- `gutter = 20`

If existing variables with these names exist in the collection, update their desktop values instead of duplicating them.

When adding the `desktop` mode, do not assume `collection.addMode("desktop").modeId` is immediately usable. Prefer this safer pattern:

```js
let collection = (await figma.variables.getLocalVariableCollectionsAsync())
  .find(c => c.name === "Wireframe");

if (!collection) {
  collection = figma.variables.createVariableCollection("Wireframe");
}

if (!collection.modes.some(m => m.name === "desktop")) {
  collection.addMode("desktop");
  collection = (await figma.variables.getLocalVariableCollectionsAsync())
    .find(c => c.name === "Wireframe");
}

const modeId = collection.modes.find(m => m.name === "desktop")?.modeId;
if (!modeId) throw new Error("Wireframe desktop variable mode was not created");
```

## Layout Grid

Apply this grid to each 1280 px page frame:

```js
frame.layoutGrids = [{
  pattern: "COLUMNS",
  visible: true,
  color: { r: 0.2, g: 0.2, b: 0.2, a: 0.12 },
  alignment: "STRETCH",
  gutterSize: 20,
  offset: 60,
  count: 12
}];
```

Create a grid style named `Wireframe / Desktop 12 Columns` and assign it to frames when possible. If style creation is unsupported in the current context, apply the grid object directly to each frame.

## Auto Layout Grid Generation Rules

Use real Figma Auto Layout grids for repeated card groups, not visual layout grids.

Do not confuse:

- `layoutGrids` = visual design grid overlay.
- `layoutMode = "GRID"` = real auto-layout grid container.

Do not reuse a previously mutated grid container when changing column or row structure. Recreate the grid container from scratch.

Reason: Figma may keep stale row or track state, causing UI to show doubled rows such as `4 x 2` instead of `4 x 1`.

### Correct Workflow

1. Collect existing card nodes.
2. Create a new frame.
3. Set `layoutMode = "GRID"` before appending cards.
4. Set `gridColumnCount`, `gridRowCount`, `gridColumnGap`, and `gridRowGap` on the fresh grid.
5. Set every card width from the target column width before placing it.
6. Insert cards with `appendChildAt`.
7. Set card width again after placing it.
8. Remove the old grid container.
9. Resize the grid from actual child bounds.

Do not mutate an existing broken grid from `4 x 4` to `4 x 2`.

### Grid Patterns

Use these defaults:

- 4 cards: `4 columns x 1 row`
- 8 cards: `4 columns x 2 rows`
- 3 cards: `3 columns x 1 row`
- 5 compact cards: `5 columns x 1 row`
- 6 cards with mixed width: `4 columns x 2 rows`; first 4 cards span `1` column, last 2 cards span `2` columns

### Container Setup

```js
grid.layoutMode = "GRID";
grid.gridColumnCount = columns;
grid.gridRowCount = rows;
grid.gridColumnGap = 20;
grid.gridRowGap = 20;
grid.primaryAxisSizingMode = "FIXED";
grid.counterAxisSizingMode = "FIXED";
grid.resize(1160, computedHeight);
```

If setting `gridRowCount` throws because the current Figma context uses auto-tracked rows, do not repair a broken existing grid by mutation. Keep the fresh grid, place children explicitly, size from child bounds, and validate the expected row count from child positions.

### Card Width Formula

```js
const cardWidth = (containerWidth - gap * (columns - 1)) / columns;
const spannedWidth = cardWidth * span + gap * (span - 1);
```

Set card width before placing it into the grid, and again after placing it.

For grid children:

- Set every direct card child to fixed width before and after placing it in the grid.
- Constrain text inside cards to `card.width - card.paddingLeft - card.paddingRight`.
- Do not run a generic fit pass that expands grid children based on internal content width.

### Grid Span Rules

For mixed grids:

```js
const spans = [1, 1, 1, 1, 2, 2];
```

Placement:

```js
grid.appendChildAt(card, rowIndex, columnIndex);
card.gridColumnSpan = span;
card.gridRowSpan = 1;
```

For a `4 x 2` transfer layout:

```js
[
  { row: 0, col: 0, span: 1 },
  { row: 0, col: 1, span: 1 },
  { row: 0, col: 2, span: 1 },
  { row: 0, col: 3, span: 1 },
  { row: 1, col: 0, span: 2 },
  { row: 1, col: 2, span: 2 }
]
```

### Height Rule

Never trust nominal row count for height. After children are placed:

```js
const maxBottom = Math.max(
  ...grid.children.map(child => child.y + child.height)
);

grid.resize(1160, Math.ceil(maxBottom) + 24);
```

The `+24` prevents clipping caused by Figma fractional grid placement.

### Validation

- no visual `layoutGrids` on card groups unless explicitly requested
- every intended grid container has `layoutMode === "GRID"`
- grid container width is `1160`
- no grid child exceeds its column width
- validation arrays must be empty: `badRows.length === 0`, `tooWideFrames.length === 0`, `textTooWide.length === 0`, `overflow.length === 0`
- no child overflows its parent:
  - `child.x + child.width <= parent inner width`
  - `child.y + child.height <= parent inner height`

Expected rows map for common landing sections:

```js
const expectedRowsBySection = {
  "Benefits grid": 1,
  "Steps": 1,
  "Use cases grid": 2,
  "Selection parameters": 1,
  "Transfers grid": 2,
  "Premium benefits": 1,
  "Security grid": 2,
  "Audience grid": 2,
  "Blog cards": 1
};
```

## Section Width Rules

Every page section must be:

- width: `1280`
- horizontal padding: `60`
- content width inside: `1160`
- height: hug or auto based on content

Do not allow inner content frames or grids to grow beyond `1160`.

Validation:

- no direct content frame inside a section may exceed `1160`
- no section may exceed `1280`
- section children should sit inside the 60 px side padding

## Integer Values Only

Never generate fractional numeric values in Figma wireframes.

Apply only whole-number values for:

- `x`, `y`
- `width`, `height`
- padding
- item spacing
- grid gaps
- card widths
- text widths
- font sizes
- line heights
- corner radius
- stroke weight

Round every computed value before using `resize`, assigning positions, setting spacing, or applying typography:

```js
const px = value => Math.round(value);

node.x = px(node.x);
node.y = px(node.y);
node.resize(px(width), px(height));
frame.itemSpacing = px(frame.itemSpacing);
frame.paddingLeft = px(frame.paddingLeft);
frame.paddingRight = px(frame.paddingRight);
```

For grid calculations, distribute any remainder intentionally so total width remains exact and no card receives a fractional width:

```js
function integerColumns(containerWidth, gap, columns) {
  const totalGap = gap * (columns - 1);
  const base = Math.floor((containerWidth - totalGap) / columns);
  const remainder = (containerWidth - totalGap) - base * columns;
  return Array.from({ length: columns }, (_, index) =>
    base + (index < remainder ? 1 : 0)
  );
}
```

Validation:

- no generated node has fractional `x`, `y`, `width`, or `height`
- no spacing, padding, grid gap, text width, font size, or line height is fractional
- no computed layout uses `.5` values as a visual workaround

## Language Consistency

Do not mix Russian and English randomly.

If the landing page is generated in Russian:

- section headings should be Russian
- card titles should be Russian unless they are product terms
- CTA labels should follow the selected language
- product terms such as `crypto top-up`, `Apple Pay`, `Google Pay`, `Premium`, `KYC`, and `OTP` may remain English

Run a final text audit for mixed-language UI labels.

## Russian Typography

Avoid dangling short words at the end of lines in Russian UI copy. Keep short prepositions, conjunctions, and particles with the following word when possible.

Examples of words to keep with the next word:

- `в`, `во`, `на`, `с`, `со`, `к`, `ко`, `у`, `о`, `об`, `от`, `до`, `за`, `из`, `по`, `для`, `при`, `и`, `а`, `но`, `не`

Use non-breaking spaces when preserving the user's exact text does not forbid typographic cleanup:

```js
function preventRussianDanglingWords(text) {
  return text.replace(/\b(в|во|на|с|со|к|ко|у|о|об|от|до|за|из|по|для|при|и|а|но|не)\s+/gi, "$1\u00A0");
}
```

Do not rewrite wording just to fix typography. Only join short words to the following word.

Do not force typographic fixes with manual line breaks. Use non-breaking spaces for dangling short words and let container width determine wrapping.

## Auto Layout

Use Figma Plugin API axis alignment values, not CSS names:

- start -> `MIN`
- end -> `MAX`
- center -> `CENTER`
- baseline -> `BASELINE`
- do not use `STRETCH` or `FLEX_START` as `counterAxisAlignItems`

Use vertical auto layout for page frames:

```js
frame.layoutMode = "VERTICAL";
frame.primaryAxisSizingMode = "AUTO";
frame.counterAxisSizingMode = "FIXED";
frame.counterAxisAlignItems = "CENTER";
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

## Size Normalization

Auto-layout roots can collapse after generation, especially with large page frames. Always run a final sizing pass after all children are added:

1. Fit standalone components.
2. Fit component instances if their parent layout needs explicit dimensions.
3. Fit page sections from deepest children upward.
4. Fit the root page frame last.

Use a helper like this and adapt dimensions to the actual layout:

```js
function fitGeneratedWireframe(node) {
  if (!("children" in node)) return;
  for (const child of node.children) fitGeneratedWireframe(child);

  if (node.layoutMode === "VERTICAL") {
    const children = node.children || [];
    const spacing = node.itemSpacing || 0;
    const paddingY = (node.paddingTop || 0) + (node.paddingBottom || 0);
    const height = children.reduce((sum, child) => sum + child.height, 0)
      + Math.max(0, children.length - 1) * spacing
      + paddingY;
    if (height > 1 && "resize" in node) node.resize(node.width, height);
  }

  if (node.layoutMode === "HORIZONTAL") {
    const children = node.children || [];
    const spacing = node.itemSpacing || 0;
    const paddingX = (node.paddingLeft || 0) + (node.paddingRight || 0);
    const width = children.reduce((sum, child) => sum + child.width, 0)
      + Math.max(0, children.length - 1) * spacing
      + paddingX;
    const height = Math.max(
      node.height,
      ...children.map(child => child.height + (node.paddingTop || 0) + (node.paddingBottom || 0))
    );
    if (width > 1 && height > 1 && "resize" in node) node.resize(width, height);
  }
}
```

Run this before final QA:

```js
for (const component of [headerComponent, footerComponent, buttonComponent]) {
  fitGeneratedWireframe(component);
}
for (const pageFrame of generatedPageFrames) {
  fitGeneratedWireframe(pageFrame);
  pageFrame.resize(1280, pageFrame.height);
}
```

## Text

Create text using supplied copy only. Text must hug height but be constrained to the parent content width.

## Typographic Hierarchy

Assign text sizes by semantic role, not by arbitrary section-by-section styling.

Default hierarchy:

- Hero `H1` is usually the largest text on the page.
- `H2` must be smaller than `H1`.
- `H3` must be smaller than `H2`.
- `H4` must be smaller than `H3`.
- `H5` must be smaller than `H4`.
- Body paragraph text must not be smaller than `16px`.
- Caption text must be `12-14px`.

Do not let a lower-level heading visually outrank a higher-level heading. For example:

- card title must not be larger than a section heading
- body copy must not be `12px` unless it is explicitly a caption or legal microcopy
- captions must not be styled like body text

When matching a reference page, copy typography values by role from the reference, but preserve the hierarchy: `H1 > H2 > H3 > H4 > H5 > p > caption`. If the reference contains a local exception, keep it only when the same semantic role exists in the new page.

Validation:

- collect generated text nodes by role
- verify heading sizes decrease by semantic level
- verify body paragraph text is at least `16px`
- verify captions are between `12px` and `14px`
- verify CTA, button, and nav labels are treated as UI labels, not headings

All text must fit inside its parent container:

- Do not leave text nodes with `height = 1`.
- Do not use fixed text height unless there is a specific reason.
- Do not insert manual `\n` line breaks into supplied text for visual composition. Preserve line breaks already present in the user's source text.
- Use `textAutoResize = "HEIGHT"` for text that must wrap inside a card, section, row, table cell, FAQ row, or content column.
- Use `textAutoResize = "WIDTH_AND_HEIGHT"` only for short labels that may define their own width, such as nav items, language switchers, compact button labels, and small pills.
- For card titles, descriptions, FAQ questions, table rows, section body copy, and any long text, set the text width to the available inner width of the parent, then use `textAutoResize = "HEIGHT"`.
- Available width is `parent.width - parent.paddingLeft - parent.paddingRight`.
- Text should never be wider than the parent's inner content area.

Use this helper for long or wrapping text:

```js
function fitTextToParent(textNode) {
  const parent = textNode.parent;
  const innerWidth =
    parent && "width" in parent
      ? parent.width - (parent.paddingLeft || 0) - (parent.paddingRight || 0)
      : textNode.width;

  textNode.textAutoResize = "HEIGHT";
  textNode.resize(Math.max(40, innerWidth), Math.max(1, textNode.height));

  if ("layoutSizingHorizontal" in textNode) {
    textNode.layoutSizingHorizontal = "FIXED";
  }

  if ("layoutSizingVertical" in textNode) {
    textNode.layoutSizingVertical = "HUG";
  }
}
```

For short labels only:

```js
textNode.textAutoResize = "WIDTH_AND_HEIGHT";
if ("layoutSizingVertical" in textNode) textNode.layoutSizingVertical = "HUG";
```

## Text Node Structure Rules

Do not wrap every individual text node in its own frame. Text should not get a separate frame just to sit inside a frame; layout should usually be handled by the parent auto-layout container.

Text should usually be a direct child of the semantic container it belongs to:

- card title and card body are direct children of `Card`
- section heading and body are direct children of `Section heading`
- FAQ question text is a direct child of `Accordion row`
- table text is a direct child of `Table row`
- button label is a direct child of `Button`

Only create an extra text wrapper frame when it has a real layout purpose:

- grouping multiple text nodes into a reusable content block
- separating a left/right column
- aligning text with an icon or control
- applying shared padding, background, or stroke
- creating a component or component slot
- making a repeated pattern easier to maintain

Avoid meaningless wrappers like:

- `Text wrapper`
- `Title container`
- `Label frame`
- one-frame-per-text structures

Bad:

```text
Card
  Title frame
    Text
  Body frame
    Text
```

Good:

```text
Card
  Icon placeholder
  Card title
  Card body
```

For layout, rely on the parent auto-layout container instead of wrapping each text:

```js
card.layoutMode = "VERTICAL";
card.itemSpacing = 12;
card.appendChild(titleText);
card.appendChild(bodyText);
```

Validation:

- flag frames that contain exactly one text node and have no fill, stroke, padding, component role, or semantic layout purpose
- avoid generating one-text wrapper frames by default

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
- no text node has `textAutoResize = "NONE"`
- no non-instance text node has `height <= 2`
- no text node is wider than `parent.width - parent horizontal padding`
- no text inside a card overflows below the card

For visual QA, use Figma MCP `get_screenshot`. Do not require shell `curl` download of the screenshot URL; sandboxed DNS can fail even when Figma generation succeeded. If visual inspection is required and shell download fails, request an inline/base64 screenshot from the MCP tool when available, or combine the screenshot metadata with the structural checks above.
