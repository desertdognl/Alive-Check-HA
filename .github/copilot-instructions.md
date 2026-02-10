# Copilot Instructions

You are working on a Home Assistant blueprint repository.

## Project goals
- Provide a reliable dead-man switch blueprint for Home Assistant.
- Keep configuration in one file and expose all options as blueprint inputs.
- Maintain clear defaults and safe behavior.

## Files
- Blueprint: [alive_check.yaml](../alive_check.yaml)
- Documentation: [README.md](../README.md)
- Changelog: [CHANGELOG.md](../CHANGELOG.md)

## Editing rules
- Keep YAML valid and compatible with Home Assistant 2026.1.x.
- Prefer explicit inputs over hard-coded entity ids.
- Preserve existing input names unless there is a breaking change.
- Use ASCII unless the file already contains non-ASCII text.
- When sharing raw GitHub URLs, always append a cache-busting query string like `?v=2`.

## Behavior expectations
- Activity should reset the timer by updating the timestamp helper.
- Check-in notification must occur after the inactivity timeout.
- Escalation occurs only if no acknowledgment is received.
- Ensure mobile app and Telegram acknowledgment paths are maintained.
