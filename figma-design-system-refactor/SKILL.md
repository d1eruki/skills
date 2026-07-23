---
name: figma-design-system-refactor
description: Audit, create, refactor, and roll out design systems inside existing Figma files. Use when Codex must identify repeated UI patterns, convert raw layers into reusable components and variants, replace screen elements with instances, normalize variables and styles, consolidate icons, typography, colors, spacing, radii, Auto Layout, system UI, naming, or build and document a Design System page while preserving existing screens, content, overrides, interactions, and visual appearance.
---

# Figma Design System Refactor

Systematize an existing Figma design without treating the component library and the screens as separate deliverables. Build the system from real patterns, then apply it back to the real consumers.

## Required reference

Before auditing or changing Figma, read [references/workflow.md](references/workflow.md) completely. Treat it as the governing workflow and quality standard for this skill.

Do not begin Figma operations after reading only this summary. The reference contains the required rules for source-of-truth resolution, invariants, discovery, pilot changes, batch replacement, overrides, error recovery, and final verification.

## Establish the project profile

Resolve or ask for only the missing information that materially affects the work:

- exact Figma file, branch, or copy authorized for editing;
- pages containing source screens and the Design System;
- target platform or platforms;
- local and subscribed component libraries;
- icon and platform-system libraries;
- current variables, styles, fonts, and naming conventions;
- requested scope and protected areas.

Inspect discoverable context before asking the user. Do not invent project-specific values.

## Select the work mode

Interpret the user's wording literally:

- For “audit,” “check,” “find,” “plan,” or “do not edit,” perform read-only inspection and report findings.
- For “how did you understand it?”, restate the intended scope and wait.
- For “do it,” “go,” “replace,” or another explicit implementation request, make the changes and verify them.
- Never convert a read-only request into a write operation.

## Execute the workflow

Follow this order:

1. Inventory existing components, component sets, instances, variables, styles, libraries, and repeated raw elements.
2. Run both an exact search and a broader semantic or visual search.
3. Classify matches before changing them. Separate true reusable patterns from visually similar but semantically different entities.
4. Define component boundaries, properties, variants, slots, and token roles from actual consumers.
5. Apply one representative pilot change.
6. Verify structure, layout, content, overrides, interactions, and visual parity.
7. Stop and diagnose if the pilot drifts visually.
8. Batch-apply only the verified pattern.
9. Repeat the original searches and visually inspect every affected screen.
10. Report completed work, counts, exceptions, and remaining risks.

## Preserve invariants

Unless the user explicitly authorizes a redesign, preserve:

- visible text and user content;
- hierarchy and intended semantics;
- dimensions, spacing, radii, and alignment;
- visual appearance;
- instance overrides and nested instance choices;
- visibility states;
- prototype interactions;
- touch or click areas;
- library linkage for library-owned elements.

Use instances rather than detached copies. Do not detach subscribed-library instances to make editing easier.

## Make components from evidence

Create variants only for genuine state, hierarchy, size, or configuration differences. Use:

- text properties for editable labels;
- boolean properties for optional elements;
- instance-swap properties for icons or replaceable nested content;
- explicit slots for structurally variable content;
- Auto Layout for normal content flow.

Avoid encoding unrelated concepts into one component set. Do not create a component merely because two layers look similar.

When changing an existing master, audit all consumers first and preserve their overrides. Retain a recoverable path until the new set has been validated.

## Normalize foundations

Reuse existing variables and styles where their semantics fit. Create new tokens only for a real reusable role, not to mirror every raw value.

For each token decision:

- distinguish primitives from semantic roles;
- bind the semantic role at the consumer;
- avoid mapping visibly different colors only because their purpose sounds similar;
- keep exceptional brand, QR, illustration, or system graphics explicit;
- prefer coherent spacing, radius, typography, and icon-size scales;
- document intentional exceptions.

## Keep geometry robust

Prefer Auto Layout and content-driven sizing. Use absolute positioning only for genuine overlays, decoration, or geometry that must be independent of content flow.

Remove wrappers only when they no longer provide layout, clipping, styling, semantics, interaction, or a stable component boundary. Repeat the audit after wrapper removal because hidden raw matches may become visible.

## Verify rather than infer

After every meaningful batch:

- inspect the changed node structure;
- compare before and after visually;
- test long and short content where relevant;
- check instances, properties, and bindings;
- confirm that the search producing the original candidates is now clear within the declared scope;
- classify every remaining match as an exception or unfinished work.

Never claim a count, zero-result audit, or completed rollout without checking the exact scope.

## Communicate

Lead with concrete results. During longer work, provide concise progress updates and surface unexpected visual changes immediately.

In the final report include:

1. components, variants, properties, variables, and styles created or updated;
2. screens or sections affected;
3. number of candidates found, replaced, and intentionally excluded;
4. repeat-audit and visual-QA results;
5. remaining risks or decisions requiring the user.

