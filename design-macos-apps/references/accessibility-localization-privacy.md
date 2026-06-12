# Accessibility, Localization, and Privacy

## Accessibility

- Expose a semantic role, accessible name, value, state, and action for every interactive element.
- Maintain logical keyboard and VoiceOver order. Keep focus visible and restore it predictably after presentations close.
- Support keyboard-only completion of primary workflows, including menus, toolbars, tables, dialogs, and drag alternatives.
- Do not encode meaning with color, position, sound, or motion alone.
- Test increased contrast, reduced transparency, reduced motion, VoiceOver, zoom, full keyboard access, and alternate pointer settings.
- Provide labels or descriptions for meaningful images, charts, progress, and custom controls.

## Inclusion and Language

- Avoid assumptions about identity, ability, culture, family structure, and expertise.
- Use plain, respectful, task-oriented language. Make error messages explain what happened and how to recover.
- Localize all user-facing strings, formats, shortcuts shown in text, and accessibility labels.
- Allow text expansion and avoid layouts dependent on a fixed character count.
- Mirror directional layout and symbols for right-to-left languages when meaning is directional; do not mirror universally recognized or inherently oriented content.

## Privacy and Permissions

- Minimize data collection and retain only what the feature needs.
- Explain the value before a system permission prompt and request access at the moment of need.
- Avoid coercive permission screens and provide useful fallback behavior when access is denied.
- Clearly separate local processing, cloud processing, sharing, analytics, and generative-AI data use.
- Avoid exposing sensitive content in notifications, recent items, previews, logs, or shared screens without user intent.

## Review Evidence

Record which assistive settings, languages, window sizes, and permission states were actually tested. Treat code inspection without assistive-technology testing as incomplete evidence.

## Apple Topics

[Accessibility](https://developer.apple.com/design/human-interface-guidelines/accessibility), [Inclusion](https://developer.apple.com/design/human-interface-guidelines/inclusion), [Right to left](https://developer.apple.com/design/human-interface-guidelines/right-to-left), [Privacy](https://developer.apple.com/design/human-interface-guidelines/privacy), and [VoiceOver](https://developer.apple.com/design/human-interface-guidelines/voiceover).
