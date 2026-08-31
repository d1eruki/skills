---
name: vue-engineering
description: Implement, review, or diagnose Vue application code, including Single-File Components, component boundaries, reactivity, composables, state ownership, and lifecycle behavior. Use only when the target project actually uses Vue.
---

# Vue Engineering

## Establish the Active Vue Conventions

Inspect the installed Vue version, build integration, source files, and nearby components before editing. Identify whether the project uses Composition API or Options API, `<script setup>` or traditional component definitions, JavaScript or TypeScript, and which router, store, and localization patterns are already established.

Follow the active local pattern unless the user explicitly requests a migration. Do not introduce a second component or state style merely because another Vue API is available.

## Keep Component Ownership Clear

Keep a one-off element in its nearest semantic parent unless extraction creates a meaningfully reusable or independently owned component. Reuse or extend an existing component before creating a parallel implementation.

Keep state with the narrowest component or shared owner that controls its lifecycle. Use the project's established props, emits, model bindings, injection, router, or store boundaries; do not make parents depend on a child's private markup or mutate state across an unclear ownership boundary.

## Reuse Reactive and Shared Logic

Before adding a composable, store, watcher, or lifecycle hook, search for an equivalent mechanism with the same contract and lifecycle. Reuse or extend it when it fits, and extract shared logic only when its consumers genuinely share ownership and cleanup requirements.

Use computed state for derived values and watchers for effects that must react to change. Keep browser subscriptions, observers, timers, and other effects in an explicit lifecycle, and clean them up when their owner is disposed.

## Preserve Observable Behavior

Diagnose rendered behavior through the active component tree, reactive state, emitted events, conditional rendering, and computed DOM state. Distinguish a Vue lifecycle or reactivity problem from CSS, browser, and third-party-library behavior before changing component structure.
