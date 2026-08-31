---
name: repository-workflow
description: Plan and carry out repository file changes with identity checks, explicit scope approval, concise user communication, documentation alignment, and instruction hygiene. Use when project instructions or the user opt into this workflow.
---

# Repository Workflow

Apply this workflow only within the repository and task scope established by the user or project instructions. It does not grant permission for unrelated changes or external actions.

## Confirm Repository Identity

Before modifying files, verify that the resolved Git root matches the repository established for the task. Do not edit another checkout, clone, or worktree merely because it became the current working directory. If the paths differ, stop and resolve the intended repository before making changes.

Preserve unrelated worktree changes and treat existing edits as user-owned unless the task establishes otherwise.

## Agree on the Change Scope

Before making any file changes, inspect the relevant context, explain the intended plan, and wait for explicit user approval. The plan must state:

- Every file that will be changed.
- Every file that will be deleted, or that no files will be deleted.
- What will be changed or removed in each file.
- Why each change is needed.

After the plan, briefly explain its material pros and cons in plain language. Include only concrete tradeoffs supported by inspected context; do not invent a disadvantage merely to balance the presentation, and state plainly when there are no material cons.

Do not edit, delete, rename, format, generate, or otherwise modify files before approval. Read-only inspection is allowed when it is needed to produce an evidence-based plan.

If the approved file list changes, a deletion becomes necessary, or the task materially expands, stop and request approval for an updated plan. Implementation details that remain within the approved files and intent do not require another approval, but tell the user that the work continues under the approved plan before editing.

## Communicate Concisely

- Keep implementation plans to at most five short bullets while covering the required approval details.
- After inspection, present one coherent approach. Change it only when new evidence or a changed requirement invalidates it, and explain the concrete reason.
- Keep routine progress updates to two sentences and send another only when the state materially changes or work exceeds 60 seconds.
- Keep final handoffs to five short lines unless risk, failure, or a blocker requires more detail.
- Do not narrate individual tool calls, repeat reported results, or list every passing command when a shorter outcome summary is sufficient.
- Clearly label unverified hypotheses. Do not claim visual appearance has been verified when visual review belongs to the user.

## Keep Documentation Aligned

When adding a dependency, update the repository's relevant setup, usage, or dependency documentation. Follow a repository-specific documentation target when one is named locally.

## Maintain Repository Instructions

Add a repository instruction only when it captures a recurring, repository-specific requirement that is not already covered by higher-level instructions, reusable skills, project tooling, or an existing rule.

Before adding or changing repository instructions:

- Search the complete applicable instruction set for overlaps or contradictions.
- List material conflicts in the approved implementation plan and resolve them as part of the change.
- Check whether an existing instruction can be clarified or extended instead.
- Keep repository-specific rules local and place reusable workflows in shared skills only when that shared-skill change is part of the user's approved task.
- Avoid duplicating behavior already enforced by formatters, linters, tests, or other tooling.

If an instruction change expands the approved scope or intent, stop and request approval for an updated plan before editing.
