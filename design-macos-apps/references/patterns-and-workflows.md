# Patterns and Workflows

## Files and Documents

- Use the system document model, open and save panels, recent items, autosave, versions, and file coordination where they fit the product.
- Make unsaved state and destructive replacement clear without repeatedly interrupting normal work.
- Preserve file identity when moving, renaming, duplicating, exporting, or sharing.
- Support drag and drop for moving or importing content when the operation is natural and provide clear destination feedback.

## Launching, Loading, and Feedback

- Show useful content or structure quickly. Restore the prior workspace when that matches user intent.
- Use determinate progress when duration or completion can be measured; otherwise use an indeterminate indicator without inventing precision.
- Keep the app responsive, permit cancellation when feasible, and explain failures near the affected task.
- Use notifications only for timely information that matters outside the current app context.

## Search, Settings, Help, and Onboarding

- Make search scope and result state clear. Support keyboard initiation and useful empty-result recovery.
- Put infrequent user preferences in a standard Settings experience; keep document-specific properties with the document or inspector.
- Introduce only concepts people need before they can proceed. Prefer contextual guidance and sample content over long mandatory onboarding.
- Offer task-oriented help with searchable language matching the interface.

## Accounts, Privacy, and Permissions

- Delay sign-in until an account-dependent feature requires it unless the app cannot function without an account.
- Explain the user benefit before requesting permission. Ask in context, request only necessary access, and provide recovery when access is denied.
- Separate account removal, sign-out, subscription, and local-data deletion when they have different consequences.

## Undo, Destructive Actions, and Modality

- Support undo and redo for content changes and reversible organizational actions.
- Prefer recovery over confirmation for low-risk mistakes. Confirm only consequential or irreversible actions.
- Use sheets for window-scoped decisions, panels for persistent tools, popovers for transient focused choices, and alerts for important conditions requiring attention.

## Sharing, Collaboration, Printing, and Media

- Use system sharing and collaboration facilities when they provide the expected identities, permissions, and destinations.
- Respect standard print setup, preview, page range, and output behavior when printing is relevant.
- Keep media controls familiar, provide captions and alternatives, respect system audio state, and preserve user control over playback.

## Apple Topics

Consult [Patterns](https://developer.apple.com/design/human-interface-guidelines/patterns), especially file management, drag and drop, loading, feedback, modality, onboarding, searching, settings, undo and redo, collaboration and sharing, printing, notifications, and media playback.
