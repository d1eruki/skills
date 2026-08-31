---
name: frontend-verification
description: Plan or validate frontend changes and tests using durable behavioral checks, existing test infrastructure, visual review, formatting, and proportional automated verification.
---

# Frontend Verification

## Reuse Test Infrastructure

Before creating a test helper, fixture, source traversal, setup hook, parser, loader, matcher, or assertion utility, search the applicable test tree for an equivalent or extendable implementation. Reuse or extract a shared mechanism when it has the same contract and lifecycle.

When a repository requires change approval, include every affected test and shared helper in the plan. If duplication is necessary, explain the concrete incompatibility that prevents reuse.

## Design Durable Tests

Prefer tests for durable product guarantees and broad failure classes, including viewport containment, usable core controls, correct navigation, persisted critical preferences, and accessible state.

Do not add a test merely because code changed or a one-off bug was fixed. Add one when a critical guarantee is likely to regress and is not already covered. Prefer extending an existing broad test over creating a narrow test.

Avoid assertions for a single CSS class, utility, `z-index`, font family, or exact pixel value unless that value is an explicit product contract. Generalize the assertion or leave visual judgment to visual review.

Exercise behavior through real interactions and observable outcomes. Trigger hover in hover tests, resize the viewport in responsive tests, and verify usability or hit testing rather than implementation details.

## Verify Proportionally

Batch related edits and run the relevant verification set after the implementation batch instead of repeatedly rerunning the same checks after individual edits.

For visual UI work:

1. Complete the scoped implementation.
2. Perform or request visual review in the environments and states affected by the change.
3. Apply visual feedback within scope and repeat review until accepted.
4. Run the repository's formatter, relevant integrity or unit tests, and relevant browser tests.
5. If a relevant failure requires a code change, treat verification as incomplete and repeat affected review and checks.

For non-visual changes, skip visual review and run only relevant checks. Run a production build when build configuration, dependencies, asset processing, or production-only behavior is affected, or at the end of a larger integration batch.

Report unrelated or pre-existing failures separately and do not describe a suite as passing when relevant checks failed or were skipped.
