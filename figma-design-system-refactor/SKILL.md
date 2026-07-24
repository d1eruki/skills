---
name: figma-design-system-refactor
description: Audit, create, refactor, and roll out design systems inside existing Figma files. Use when Codex must identify repeated UI patterns, trace component usage across pages, safely retire unused masters or documentation, convert raw layers into reusable components and variants, replace screen elements with instances, normalize variables and styles, consolidate icons, typography, colors, spacing, radii, Auto Layout, system UI, naming, or build and document a Design System page while preserving existing screens, content, overrides, interactions, and visual appearance.
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

1. Resolve the linked node's actual type and role. If it is an instance, follow `mainComponent` to the variant and Component Set instead of treating the linked placement as the master. Re-resolve current page names and node IDs, then inventory existing components, instances, variables, styles, libraries, and repeated raw elements.
2. Convert the user's wording into an explicit eligibility filter. Run both an exact relationship search and a broader semantic or visual search, but report and change only candidates that pass that filter.
3. Classify matches before changing them. Separate true reusable patterns from visually similar but semantically different entities.
4. Define component boundaries, properties, variants, slots, token roles, and coupled content rules from actual consumers.
5. Snapshot the pilot's content, overrides, parent index, sizing, and geometry before inserting anything into its Auto Layout parent. Immediately before the write, re-read the live node and assert that the assumptions still hold; stop if the file drifted.
6. Verify structure, layout, content, overrides, interactions, and visual parity.
7. Stop and diagnose if the pilot drifts visually.
8. Batch-apply only the verified pattern. Re-read each candidate before mutation rather than relying on an old discovery snapshot.
9. Repeat the original searches, reconcile the final per-variant distribution with real current content, include hidden states when the result may authorize deletion, and visually inspect every affected screen, master, and documentation container.
10. Report completed work, counts, exceptions, and remaining risks.

## Preserve invariants

Unless the user explicitly authorizes a redesign, preserve:

- visible text and user content exactly; never paraphrase a label while performing a structural refactor;
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

When two editable values must remain synchronized, do not expose only one of them. For example, an address and its QR code, a label and its status asset, or a payment method and its logo may require paired properties, a nested instance swap, a slot, or a variant that prevents invalid combinations.

When two components share the same structural and sizing contract and differ only by a stable hierarchy or appearance axis, prefer extending the existing component set over creating a parallel public component. Migrate all confirmed consumers before retiring the old master.

Treat a repeated composite as a data matrix, not a single visual sample. Before replacing a list, timeline, status stack, or multi-row control, record its item count, order, text, per-item state, and visibility for every consumer. The migration must preserve that matrix; never collapse several old items into one new instance merely because the new visual is compact.

When changing an existing master, audit all consumers first and preserve their overrides. Retain a recoverable path until the new set has been validated.

Represent progress, stepper, and multi-stage states from the full consumer matrix. Do not collapse distinct active steps into one generic visual. Keep only combinations that exist or are explicitly required; if a universal set creates many irrelevant properties or invalid combinations, split the API or use a nested component.

## Audit usage before retirement

Do not infer a linked node's role from its name or appearance. A link may target a documentation wrapper, preview frame, master component, component set, variant, instance, or raw copy. Resolve its type, ancestors, material descendants, and source relationship first.

Count actual consumers by master ID or component key, not by layer name. Audit every page in scope and distinguish:

- source master placement;
- documentation preview;
- direct product instances;
- nested instances inside other masters;
- hidden instances or states;
- detached or raw lookalikes.

A fast scan that skips invisible instance children is not sufficient evidence for deletion. Repeat the exact audit without that optimization before declaring a master unused.

No instances in the current file does not prove that a published library component has no consumers in other files. Check publish status and state this limitation before deletion.

Before deleting a wrapper that contains a master, name every material object that will be removed. After deletion, verify the old IDs no longer resolve, repeat the broad search, and inspect the parent layout for gaps or unintended reflow.

## Normalize foundations

Reuse existing variables and styles where their semantics fit. Create new tokens only for a real reusable role, not to mirror every raw value.

For each token decision:

- distinguish primitives from semantic roles;
- bind the semantic role at the consumer;
- include interaction or state in the role when it changes meaning, such as static, interactive, selected, disabled, or overlay;
- avoid mapping visibly different colors only because their purpose sounds similar;
- keep exceptional brand, QR, illustration, or system graphics explicit;
- prefer coherent spacing, radius, typography, and icon-size scales;
- document intentional exceptions.

## Keep geometry robust

Prefer Auto Layout and content-driven sizing. Use absolute positioning only for genuine overlays, decoration, or geometry that must be independent of content flow.

Record the source state before inserting a replacement into an Auto Layout parent. Insertion can immediately reflow the source, making post-insertion coordinates invalid as “before” evidence.

Moving or cloning a source into Auto Layout documentation can also change the future master before it is combined as a variant. Normalize every variant's `FILL`/`HUG`/`FIXED` behavior and exact dimensions after reparenting, then validate the entire set rather than only the first child.

Normalize fractional values only on editable UI layout geometry. Do not round library internals, vector path data, QR or barcode geometry, masks, or negligible floating-point artifacts inside imported graphics.

Remove wrappers only when they no longer provide layout, clipping, styling, semantics, interaction, or a stable component boundary. Repeat the audit after wrapper removal because hidden raw matches may become visible.

Classify small graphics before an icon-library rollout. Interchangeable glyphs, state indicators, progress rings, status dots, logos, system graphics, and decoration are different families. Replace only the families explicitly in scope; preserving a local state indicator can be correct when it is not an interchangeable icon.

## Verify rather than infer

After every meaningful batch:

- inspect the changed node structure;
- compare before and after visually;
- test long and short content where relevant;
- check instances, properties, and bindings;
- confirm that the search producing the original candidates is now clear within the declared scope;
- classify every remaining match as an exception or unfinished work.

Treat the Figma file as live state. If a late read disagrees with an earlier count, size, variant, title, or visibility, inspect the outlier and current content before correcting it. The expected count is not a source of truth.

For visual QA, prefer an opaque outer screen or consumer. An isolated transparent component can render on a dark checkerboard or black background and hide dark text, producing a false failure or false pass.

If pages, sections, or layers were renamed during the task, refresh the page inventory and resolve the current structure again before claiming completion. Treat IDs as stable references only while they still resolve; replacement or deletion can invalidate the original link.

When claiming that a rollout is complete, rerun both the exact relationship search and the broad structural or visual search over the entire agreed page or page set. A clean instance count does not prove that raw lookalikes are gone.

Never claim a count, zero-result audit, or completed rollout without checking the exact scope.

Organize Design System documentation by semantic domain and component role, not by shared words alone. Move documentation wrappers rather than recreating masters, preserve component IDs, use Auto Layout for the category, and verify parent reflow plus broken instances.

## Communicate

Lead with concrete results. During longer work, provide concise progress updates and surface unexpected visual changes immediately.

In the final report include:

1. components, variants, properties, variables, and styles created or updated;
2. screens or sections affected;
3. number of candidates found, replaced, and intentionally excluded;
4. repeat-audit and visual-QA results;
5. remaining risks or decisions requiring the user.
