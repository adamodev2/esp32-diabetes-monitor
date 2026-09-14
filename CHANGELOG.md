# Changelog

All notable changes to the ESP32 CGM Display project.

## [1.0.45]

### Changed
- **Reading age in status bar**: The top line now shows the current local time and relative reading age, for example `13:45, Updated 3m ago`.
- **Clear stale status**: When data is stale, the same line shows how long fresh data has been unavailable. The glucose unit was removed from this status line.

## [1.0.44]

### Fixed
- **Truthful time-based graph**: History points are positioned by their Libre timestamps, so network and uploader outages remain visible as empty gaps.
- **History recovery**: Available LibreLinkUp `graphData` is merged into the chart after reconnection without duplicating readings.
- **Stale data handling**: Repeated old Libre measurements no longer refresh the reading age or add fake graph continuity.
- **No zero on fetch failure**: The last valid measurement is retained internally; after 15 minutes the dashboard shows no current value and reports when data stopped.

## [1.0.43]

### Added
- **Web-configurable display brightness**: Added a 1-100% brightness slider with 1% increments to Hardware Control. The setting is stored in NVS and restored after reboot.
- **Brightness backup and restore**: Display brightness is included in configuration exports and imports.

### Changed
- Saving brightness applies it immediately. The device only reboots when display rotation changes.

## [1.0.42] - 2026-07-03

### Added
- **Libre delta readings**: Easily see the difference between current reading and last reading and/or last x readings
- **Configurable Graph Y-Axis Indicator Lines**: Decoupled dotted indicators from alert warning thresholds
- **Libre Config Trend Arrow Toggle**: Added checkbox to enable/disable the Libre Link Up trend arrow.
- **Unified Alert Triggers & Colors System**: Merged the old warning limits and message rules into a single 10-rule alert engine. Supports Above, Below, Between, Drops Below (passing 2 thresholds over duration), and Rises Above (passing 2 thresholds over duration) rules with configurable Red, Amber, Green colors and optional custom dashboard messages.
- **LLU Poll rate default**: Set default Libre Link Up poll rate to 1 minute.
- **Backup & Restore**: Added support for all new functions
- **Display rotation**: Can now rotate the display
- **BETA BETA BETA MQTT / Home Assistant Integration**: Enabled TCP (1883) and TLS (8883) secure MQTT client connections.
- **Bi-directional MQTT commands**: Listens for incoming commands on `<prefix>/cmd/refresh` (forces LibreLinkUp fetch), `<prefix>/cmd/reboot` (reboots device), and `<prefix>/cmd/message` (displays custom status message at the bottom of the dashboard).

---

## [1.0.34] - 2026-06-27

### Added
- **Internet Loss Fallback to Zero Glucose Reading**: Resets `last_glucose` to `0.0` when LLU fetches fail.
- **Clean Disconnected Display State**: If `last_glucose <= 0.0`, the screen displays `"0.0"` (or `"0"` in mg/dL), draws a neutral **Grey** background banner
- **Diabetes:M Custom Category Upload Mapping**: Custom category selections
- **LCD Touch Screen Long Press Diagnostics**: Press and hold display for quick diagnostics
- **Network / WiFi Configuration Webpage**: Added a dedicated `/wifi` settings webpage allowing you to reconfigure Wi-Fi SSID, Password, and Device Name (hostname) on the fly.
- **DHCP Client Hostname**: Set customized hostname dynamically on boot using `WiFi.setHostname(device_name)`.
