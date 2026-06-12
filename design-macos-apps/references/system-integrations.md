# System Integrations

Load this reference only for integrations the product actually uses.

## General Rules

- Prefer the system framework and standard authorization, identity, picker, payment, sharing, and status surfaces.
- Introduce an integration where it improves a real workflow, not only because the API exists.
- Explain account, network, device, subscription, and permission prerequisites before a user reaches a dead end.
- Define unavailable, offline, signed-out, denied, expired, and partial-sync states.

## Common macOS Integrations

- **iCloud:** Make sync state understandable without turning routine synchronization into persistent noise. Handle conflicts, offline edits, and account changes.
- **Sign in with Apple:** Use the standard control and identity flow. Do not ask for data the feature does not need.
- **Siri, App Shortcuts, and snippets:** Model concise, predictable actions with clear parameters and confirmation proportional to risk.
- **Widgets and notifications:** Surface glanceable, timely information and deep-link to the relevant app context. Avoid duplicating the full app UI.
- **SharePlay and collaboration:** Clarify participant identity, shared state, permissions, and what remains private.
- **Apple Pay and in-app purchase:** Use standard purchase surfaces and clearly distinguish price, billing period, restoration, entitlement, and cancellation implications.
- **Generative AI and machine learning:** Communicate capability and limitations, preserve user review for consequential output, identify data handling, and provide recovery from unavailable or incorrect results.
- **Maps, media, and AirPlay:** Preserve familiar controls, destination state, privacy, and interruption behavior.
- **Mac Catalyst:** Adapt the experience for Mac rather than shipping an enlarged iPad layout. Add menu commands, keyboard support, pointer behavior, window management, toolbar structure, and Mac-appropriate density.

## Verification

Open the exact topic under [Technologies](https://developer.apple.com/design/human-interface-guidelines/technologies) before specifying branding, control appearance, legal text, authorization flow, or recent platform capabilities.
