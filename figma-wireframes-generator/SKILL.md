---
name: figma-wireframes-generator
description: Generate desktop low-fidelity landing page wireframes and supporting pages in the currently open Figma file. Use when the user asks Codex to create, draw, build, or generate Figma wireframes for landing pages from supplied text structure, headings, sections, page copy, or related page outlines. Trigger for landing wireframes only, including main landing pages, policy pages, pricing/detail pages, thank-you pages, and other landing-adjacent pages; do not use for mobile screens, dashboards, web apps, diagrams, or pixel-perfect visual design.
---

# Figma Wireframes Generator

Create strict desktop landing-page wireframes in Figma from user-supplied text. Keep the output low-fidelity: gray blocks, real copy, clear hierarchy, reusable components, auto layout, and a 1280 px desktop frame.

## Required Skills And Tools

- Load `figma:figma-use` before every `use_figma` write call.
- Use only `use_figma` for generation. Do not call `generate_diagram`, `generate_deck`, or `generate_figma_design` for this skill.
- Work in the open or user-provided Figma file. Do not create a new Figma file unless the user explicitly asks for one.
- For Figma API implementation patterns, read `references/figma-wireframe-api.md` only when preparing code for `use_figma`.

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
- Use auto layout for frames, sections, component internals, and repeated structures.
- Set text nodes to hug width and hug height whenever possible.
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
4. Load `figma:figma-use`.
5. Use `use_figma` to create or update the wireframes in the current Figma file.
6. Create desktop variables, grid style, and the component set.
7. Build each page as a 1280 px wide auto-layout frame with the grid applied.
8. Insert header, footer, and button instances instead of detached copies.
9. Use the supplied text exactly unless the user asked for copy expansion.
10. Run a quick Figma-side check that no generated page contains detached header/footer/button structures.

## UX Guidance

Use landing-page UX best practices to shape layout without inventing content:

- Put the primary offer, value proposition, or product subject first if the supplied content identifies it.
- Keep section order legible: hero, supporting proof or explanation, benefits/features, process/details, conversion block, footer.
- Create supporting pages with simpler hierarchy and the same reusable header/footer.
- Prefer clear scanning, sufficient whitespace, and predictable CTA placement.
- If the supplied structure conflicts with usability, preserve the text but improve grouping and order, then mention the adjustment.

## Deliverable

Return only a short completion note and the Figma file/page context when available. Do not produce extra artifacts such as user flows, diagrams, journey maps, notes boards, or documentation unless the user explicitly asks.
