---
name: figma-wireframes-generator
description: Generate desktop low-fidelity landing page wireframes and supporting pages in the currently open Figma file. Use when the user asks the agent to create, draw, build, or generate Figma wireframes for landing pages from supplied text structure, headings, sections, page copy, or related page outlines, including requests to match an existing landing page style or make a page consistent with a reference page. Trigger for landing wireframes only, including main landing pages, policy pages, pricing/detail pages, thank-you pages, and other landing-adjacent pages; do not use for mobile screens, dashboards, web apps, diagrams, or pixel-perfect visual design.
---

# Figma Wireframes Generator

Create strict desktop landing-page wireframes in Figma from user-supplied text. Keep the output low-fidelity: gray blocks, real copy, clear hierarchy, reusable components, auto layout, and a 1280 px desktop frame.

## Required Skills And Tools

- Use the available Figma MCP write tool for generation:
  - Codex/OpenAI: load `figma:figma-use` before every `use_figma` write call.
  - Claude Code: use the configured Figma MCP write tool equivalent to `use_figma`.
- If no Figma MCP write tool is available, ask the user to connect/configure Figma MCP instead of generating non-Figma artifacts.
- Do not call `generate_diagram`, `generate_deck`, or `generate_figma_design` for this skill.
- Work in the open or user-provided Figma file. Do not create a new Figma file unless the user explicitly asks for one.
- For Figma API implementation patterns, read `references/figma-wireframe-api.md` only when preparing JavaScript for the Figma MCP write tool.
- If the user asks to make a page "in the style of", "like", "consistent with", "as the main page", or "based on" an existing page, treat that page as a strict visual reference. Measure its visual values before generating; do not use it as loose inspiration.

## Runtime Support

This skill supports both Codex/OpenAI and Claude Code. Keep the workflow, constraints, component rules, and `references/figma-wireframe-api.md` shared across both runtimes.

`agents/openai.yaml` is OpenAI/Codex UI metadata only. Claude Code does not require a separate `agents/claude.yaml`; its skill metadata is the YAML frontmatter in `SKILL.md`.

## Intake

Before generating anything, run a 5-question intake as a step-by-step questionnaire.

Ask one question at a time, wait for the user's answer, then ask the next question. Do not ask all 5 questions in one message.

Use the native interactive questionnaire tool when it is available, such as `request_user_input` or `ask_user_question`. Do not simulate the questionnaire as a plain text list when a native UI question tool is available.

For each native UI question:

- ask exactly one question per tool call
- provide 2-3 concise mutually exclusive options
- put the recommended/default option first when there is a sensible default
- rely on the tool's built-in custom/Other answer field when available

If no native UI question tool is available in the current environment, explain briefly that the interactive questionnaire UI is unavailable and ask whether to continue with plain text questions.

Use the user's previous answers to choose the next most useful question. Cover the missing decisions that most affect layout and UX, such as:

- page list and hierarchy
- target audience
- primary conversion goal
- desired header navigation items
- CTA labels and destinations
- required sections and ordering
- footer links
- whether supplied text may be edited or extended

If the user provides limited information, complete the 5-question questionnaire and wait after each question. Act as a competent UX designer, but do not silently invent core product content.

Example native questionnaire content:

```text
Header: Goal
Question: What is the primary conversion goal for this landing page?
Options:
- Lead form submission
- Book a call
- Learn more
Custom answer: handled by the UI's Other field
```

## Copy Rules

- Use only the headings, body copy, CTA labels, and page text supplied by the user.
- Do not add generic marketing copy, placeholder benefits, invented slogans, or filler text.
- Preserve the user's text intent and meaning.
- It is acceptable to improve structure, hierarchy, grouping, and section order when doing so follows UX best practices.
- For Russian copy, avoid dangling short prepositions, conjunctions, and particles at line ends by keeping them with the following word when possible.
- Do not insert manual line breaks into supplied text for visual composition. Let text wrap naturally from container width; preserve user-provided line breaks and use non-breaking spaces only to prevent dangling short words.
- If the user explicitly asks to add, expand, rewrite, complete, or improve the copy, ignore the no-added-copy rule for that request and provide the requested copy support.
- If a UI element needs text but the user did not supply it, ask for it unless it is a purely structural label such as "Header", "Footer", or an internal layer name.

## Wireframe Specification

Always create desktop wireframes only.

- Frame width: `1280`
- Variable mode name: `desktop`
- Variables:
  - `columns = 12`
  - `breakpoint = 1280`
  - `margin = 60`
  - `gutter = 20`
- Apply a layout grid to every wireframe page using these values.
- Center page content inside each frame.
- Constrain main section content to the `breakpoint` variable.
- Every page section must be width `1280`, with horizontal padding `60`, inner content width `1160`, and auto height based on content.
- Use auto layout for frames, sections, component internals, and repeated structures.
- Use real Figma Auto Layout grids for repeated card groups with predictable columns. Recreate grid containers from scratch when changing row or column structure.
- Set text to hug height while constraining width to the parent content area. Do not make long text hug width, because it can expand cards and break the grid.
- Preserve typographic hierarchy by role: hero `H1` is usually largest, then `H2`, `H3`, `H4`, `H5` decrease by level; body text must not be smaller than `16px`, and captions must be `12-14px`.
- Do not wrap individual text nodes in meaningless one-text frames. Let the parent auto-layout container handle spacing and alignment.
- Normalize generated sizes after building components and pages so auto-layout frames do not collapse to height `1`.
- Never generate fractional numeric layout values. Round all computed positions, sizes, gaps, padding, and typography values to whole pixels before applying them in Figma.
- Keep UI language consistent. Do not randomly mix Russian and English labels; preserve product terms when appropriate.
- When matching an existing reference page, copy visual values literally by role and pattern: colors, strokes, radii, spacing, typography, buttons, cards, forms, placeholders, header, and footer.
- Use restrained layer names: clear enough for a designer, not obsessively detailed.
- Use gray-scale fills and strokes only unless the user explicitly asks for visual styling.
- Do not create final UI polish, brand styling, illustrations, photos, or decorative visual design.

## Component Rules

Create reusable components beside the page frames before composing pages:

- Header component
- Footer component
- Button component, with variants only if the supplied structure requires distinct button types

Use instances of those components in every landing page and supporting page. Do not leave non-component headers, footers, or buttons inside the wireframe pages.

Header, footer, and button components may use simple gray containers, text, and spacing. They should be structurally useful for later design work rather than visually final.

## Generation Workflow

1. Parse the user's supplied structure into pages, sections, headings, body text, CTAs, and repeated elements.
2. Ask exactly 5 clarifying questions as a sequential questionnaire, one question per user turn.
3. Summarize the planned pages and section order briefly.
4. Use the available Figma MCP write tool: `use_figma` in Codex/OpenAI after loading `figma:figma-use`, or the configured equivalent in Claude Code.
5. If a reference page is requested, inspect it first, extract a style inventory, and create a content-role to reference-style role map.
6. Create or update the wireframes in the current Figma file.
7. Create desktop variables, grid style, and the component set.
8. Build each page as a 1280 px wide auto-layout frame with the grid applied.
9. Build repeated card groups as fresh `layoutMode = "GRID"` containers when the column structure is predictable.
10. Insert header, footer, and button instances instead of detached copies.
11. Use the supplied text exactly unless the user asked for copy expansion.
12. Run a final sizing pass: fit standalone components first, then page sections, then root page frames.
13. Run a Figma-side validation for section widths, grid row counts, overflow, text sizing, and detached header/footer/button structures.
14. Run a final text audit for mixed-language UI labels.
15. If matching a reference page, run a visual parity check against the reference before answering.
16. For visual QA, use Figma MCP `get_screenshot`. If shell networking is restricted, do not require `curl`; request an inline/base64 screenshot when visual inspection is needed, or combine the MCP screenshot metadata with Figma-side structural checks.

## UX Guidance

Use landing-page UX best practices to shape layout without inventing content:

- Put the primary offer, value proposition, or product subject first if the supplied content identifies it.
- Keep section order legible: hero, supporting proof or explanation, benefits/features, process/details, conversion block, footer.
- Create supporting pages with simpler hierarchy and the same reusable header/footer.
- Prefer clear scanning, sufficient whitespace, and predictable CTA placement.
- If the supplied structure conflicts with usability, preserve the text but improve grouping and order, then mention the adjustment.

## Deliverable

Return only a short completion note and the Figma file/page context when available. Do not produce extra artifacts such as user flows, diagrams, journey maps, notes boards, or documentation unless the user explicitly asks.
