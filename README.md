# Alive Checker (HA)

Dead-man switch automation blueprint for Home Assistant that tracks activity and escalates when no check-in is received.

## What this does
- Monitors selected entities for activity
- Updates a timestamp helper on every activity event
- Sends a check-in notification after inactivity
- Escalates to an emergency contact if no response arrives in time

## Requirements
- Home Assistant 2026.1.2 or newer
- Helper: input_datetime named for last activity
- Notification service(s): Mobile App, Telegram, or Email

## Install
1. Copy the blueprint to your Home Assistant blueprints folder.
2. Import the blueprint in Home Assistant.
3. Create a new automation from the blueprint and configure inputs.

Blueprint file: [alive_check.yaml](alive_check.yaml)

## Usage
- Create a helper (Settings > Devices & Services > Helpers) for last activity time.
- Choose entities to monitor (motion sensors, doors, locks, etc.).
- Pick a notification method and configure the notifier service.
- Set an inactivity timeout and a response grace period.

## Configuration inputs
- Monitored entities
- Inactivity timeout (hours)
- Response grace period (minutes)
- Notification method (mobile app, Telegram, email)
- Notifier services for the chosen method and emergency contact
- Timestamp helper
- Check-in and emergency message text
- Action and callback identifiers for mobile app and Telegram

## License
Unlicense. See [LICENSE](LICENSE).
