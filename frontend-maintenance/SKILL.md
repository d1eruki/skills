---
name: frontend-maintenance
description: Audit and modernize a frontend project's runtime, dependencies, tooling, or custom mechanisms while preserving a coherent compatible stack. Use for explicit currency audits, dependency updates, compatibility reviews, or replacement research.
---

# Frontend Maintenance

Treat maintenance as a compatibility problem across one connected system rather than a sequence of isolated package upgrades. Prefer the newest stable level the complete project can safely support within its selected runtime line.

## Select a Supported Runtime

1. For runtimes with an LTS lifecycle, default to the newest active LTS major and latest stable patch supported by the complete stack.
2. Do not select Current, nightly, prerelease, or experimental lines merely because they are newer. Use them only for an explicit product requirement.
3. During a currency or support audit, check the selected runtime's lifecycle phase, maintenance date, end-of-life date, and the newest active LTS.
4. For dependencies without LTS policy, prefer the latest mutually compatible stable release and exclude prerelease tags unless explicitly required.

## Establish the Baseline

1. Confirm the repository root and preserve unrelated worktree changes.
2. Read the manifest, lockfile, runtime declarations, build and test configuration, CI or hosting configuration, and relevant dependency documentation.
3. Record runtime and package-manager requirements, lockfile format, framework and bundler versions, deployment constraints, pins, and documented workarounds.
4. Distinguish runtime, development, optional, and important transitive dependencies by actual responsibility. Libraries imported by browser application code and responsible for shipped behavior belong in runtime dependencies; build, lint, formatting, and test tools normally belong in development dependencies.
5. Keep the audit read-only until the repository's approval policy permits changes.

## Audit Currency and Maintenance

Use current primary sources because versions and compatibility policies change.

1. Compare installed, declared, latest stable, and latest compatible versions. Inspect distribution tags instead of assuming `latest` is the intended line.
2. Read official release notes, migration guides, engine requirements, peer ranges, deprecations, and breaking changes for proposed major updates.
3. Inspect the connected chain around each update: runtime, package manager, framework, bundler, dev server, plugins, loaders, compilers, linters, and test runners.
4. Check maintenance status, release recency, advisories, repository health, license, and replacement notices. Treat security findings separately from compatibility findings.
5. Use package-manager commands as evidence, but do not treat one command as sufficient compatibility proof.

For project-wide audits, account for every direct dependency. Map each package to confirmed imports, configuration, scripts, tests, documentation, or generated assets. Classify each as `keep`, `update`, `replace`, `remove`, or `defer`, and separate confirmed evidence from hypotheses.

## Evaluate Custom Mechanisms

1. Map the mechanism's contract, lifecycle, consumers, edge cases, fallbacks, tests, and production constraints.
2. Look first for a platform built-in, an API in an installed library, or an established project pattern. Consider a new dependency only when those are insufficient.
3. Compare candidates by maintenance, compatibility, API fit, bundle and install cost, tree-shaking, accessibility, licensing, security history, migration effort, and future ownership.
4. Recommend replacement only when it removes meaningful maintenance burden without losing required behavior or creating a larger integration surface.
5. Record rejected candidates and their concrete mismatch.

## Derive a Compatible Target

1. Build a compatibility graph for coupled upgrades and identify constraints from engines, peer dependencies, compiler APIs, plugin APIs, and lockfile behavior.
2. Select the highest mutually supported stable target versions. State which newer versions remain blocked, why, and what would unblock them.
3. Group coupled packages into one atomic batch. Do not independently upgrade parts of a framework, bundler, compiler, loader, or test-adapter chain when their compatibility is connected.
4. Separate low-risk independent updates from major migrations.
5. Define observable acceptance checks before editing: clean installation, dependency-tree validity, formatting, tests, browser checks, production build, and migration-specific behavior.

## Update Without Hiding Conflicts

1. Modify manifests through the package manager where practical and let it regenerate the lockfile. Do not edit resolved lockfile entries manually.
2. Require a clean frozen-lockfile installation using the declared runtime and normal settings as the installation acceptance check.
3. Do not accept forced installs, ignored peer dependencies, broad overrides, or ignored engine checks as permanent fixes.
4. When installation fails, identify exact conflicting ranges using package-manager explanation commands, tree inspection, lockfile evidence, and upstream documentation.
5. Do not run forced automatic security upgrades. Determine whether an advisory affects production, development only, or an unreachable path, then resolve it compatibly.
6. Request revised approval when conflict resolution changes approved files, dependency strategy, runtime target, or product behavior.

## Verify and Report

Use `$frontend-verification` for test design, visual review, and validation ordering when it is available in the target environment.

Verify each approved compatibility batch once after implementation and include a production build whenever dependencies, build configuration, asset processing, or production-only behavior changes. Confirm both declared dependency validity and a clean installation.

Report selected versions, skipped versions and blockers, removed and remaining workarounds, custom mechanisms retained or replaced, and intentionally deferred work with concrete revisit conditions.
