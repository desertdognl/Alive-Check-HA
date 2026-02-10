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
1. Import the blueprint in Home Assistant using the raw URL.
2. Create a new automation from the blueprint and configure inputs.

Raw import URL (always use raw, not GitHub blob):
https://raw.githubusercontent.com/desertdognl/Alive-Check-HA/main/alive_check.yaml?v=3

If Home Assistant shows a YAML error like `--tab-size-preference`, it means a GitHub HTML page was imported. Use the raw URL above.

Blueprint file: [alive_check.yaml](alive_check.yaml)

## Usage
- Create a helper (Settings > Devices & Services > Helpers) for last activity time.
- Choose entities to monitor (motion sensors, doors, locks, etc.).
- Choose which services should receive the check-in (mobile app, Telegram, email).
- Fill in the notifier service names for each enabled method.
- Set an inactivity timeout and a response grace period.

## Finding notify services (Home Assistant 2026.2)
The Developer Tools "Services" tab is now called "Actions".

To find your mobile app notify service:
1. Settings > Devices & Services > Integrations > Mobile App.
2. Open your phone device and note the notification service name.
3. In Developer Tools > Actions, choose "Call service" and search for `notify.mobile_app_`.

If you only see a Telegram service, the phone app is not registered. Open the Home Assistant mobile app, log in, and allow notifications.

## Configuration inputs
- Monitored entities
- Inactivity timeout (hours)
- Response grace period (minutes)
- Enabled notification services (mobile app, Telegram, email)
- Notifier service names for each enabled method and emergency contact
- Optional emergency target (phone number or email address)
- Timestamp helper
- Check-in and emergency message text
- Action and callback identifiers for mobile app and Telegram

## Example automation inputs
When using this blueprint, enter notifier services as plain service names (no action payload needed). Example:

```yaml
use_blueprint:
	path: desertdognl/alive_check.yaml
	input:
		monitored_entities:
			- binary_sensor.hallway_sensor_motion
			- binary_sensor.corridor_sensor_motion
		inactivity_timeout_hours: 10
		send_telegram: true
		send_mobile_app: true
		send_email: false
		timestamp_helper: input_datetime.last_alive_check
		telegram_notifier: notify.me
		mobile_app_notifier: notify.mobile_app_iphone_02
		emergency_notifier: notify.me
		emergency_target: "+123456789"
```

	## Troubleshooting
	- Import error mentioning `--tab-size-preference`: you imported the GitHub HTML page. Use the raw URL with `?v=3`.
	- Import error about `monitored_entities` selector: ensure you are using the raw URL, not a cached or blob URL.
	- No `notify.mobile_app_*` service: open the Home Assistant mobile app, log in, register the device, and enable notifications.
	- Telegram button does not acknowledge: confirm the Telegram integration is working and the callback event fires.

## License
Unlicense. See [LICENSE](LICENSE).
