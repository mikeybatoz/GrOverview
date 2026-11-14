# GrOverview

**Plants, spaces and live readings — inside Home Assistant.**

Journal a plant once. Connect it to its room and planter. Keep photos, care events and sensor history together.

**Built by mikeybatoz with extensive assistance from OpenAI Codex.** The foundation was mikeybatoz's existing Home Assistant growing system, AC Infinity reverse-engineering work, Bluelab data collection and BLE6 Node-RED dosing workflows. Codex helped turn that established work and the owner's requirements into this application through code implementation, refactoring, documentation and testing. Third-party projects retain their own credit and licenses.

[![Add GrOverview to Home Assistant](https://my.home-assistant.io/badges/supervisor_add_addon_repository.svg)](https://my.home-assistant.io/redirect/supervisor_add_addon_repository/?repository_url=https%3A%2F%2Fgithub.com%2Fmikeybatoz%2FGrOverview)

**Experimental beta · 0.21.1-beta.4 · ARM64 and AMD64 · Home Assistant OS**

This is the official installer and support repository. Application development is private. Prebuilt images are downloaded from GitHub Container Registry; Home Assistant does not compile the application on your Pi.

## Install

1. Make a full Home Assistant backup.
2. Click **Add GrOverview to Home Assistant** above. Alternatively open **Settings → Apps → Install app → ⋮ → Repositories** and add `https://github.com/mikeybatoz/GrOverview`. Older HA versions call this **Add-ons → Add-on Store**.
3. Find **GrOverview**, select **Install**, then **Start** and **Open Web UI**.
4. Select **Install connector & check configuration**, then **Restart Home Assistant** when the check passes. The included connector supplies HA entities, Bluetooth/USB access and recording. No HACS installation is needed.
5. Leave **dosing_locked** enabled. Add your rooms, link sensors and assign plants to their planters.

Installation needs Home Assistant OS with Supervisor, Core 2026.11 or newer, and an administrator account. Home Assistant Container alone has no add-on store. Read [setup, backup and migration details](growerview/DOCS.md) before upgrading an existing installation.

## What is included

| Area | What it does |
| --- | --- |
| Plant journal | Individual plant records, shared care events, photos, dates and planter history |
| Room designer | Room and bed placement, equipment, positioned sensors and links back to the journal |
| Measurements | Automatic recording of linked HA readings, charts, DLI calculations and saved stage comparisons |
| AC Infinity | Native Bluetooth discovery and supported controller profiles; requires an HA radio or active proxy |
| ESPHome and Govee | Use compatible entities already available in Home Assistant |
| Bluelab | USB receiver selection and automatic reconnection after setup; optional Edenic account connection |
| Reservoirs | Pump settings, calibration, nutrient recipes, sliders and dosing controls behind a default-on dosing lock |
| Diagnostics | Connection status and missing/stale data in a dedicated page |

## Beta boundaries

- Physical hardware support depends on model, firmware, radio/USB availability and configuration. A detected device is not proof that every control is supported.
- Existing Home Assistant cameras can be linked. Wyze uses an additional transport service; the portable video setup is still being completed.
- Plant Sense journal/sensor checks are included. Local image analysis needs a separately configured worker; its model/runtime is not bundled in this beta. Photo results are observations to review, not a confirmed diagnosis.
- DLI from lux requires a configured conversion factor and is an estimate. Missing readings are not silently treated as zero.
- The dosing lock blocks commands through this add-on, including activation of configured pump switches. It does not disable separate Node-RED flows, HA automations, vendor apps or an older panel. Leave dosing off until pump calibration and commissioning are complete.

## Tested

The previous beta passed AMD64/ARM64 builds, ARM64 startup under emulation, and real Supervisor installation, upgrade, rollback and full-backup restore on an isolated development PC. Journal records and photo bytes survived those tests. The application code in this release is unchanged apart from release identification and distribution notices. Each published image runs the 19 add-on checks; physical-device and microphone tests are separate.

## Get help

[Installation guide](growerview/DOCS.md) · [Changes](growerview/CHANGELOG.md) · [Report a problem](https://github.com/mikeybatoz/GrOverview/issues/new/choose)

Please include your add-on version, HA version, device model and steps to reproduce. Remove passwords, API keys, tokens, photographs and other private records from logs before sharing them.

## Use and ownership

Official releases are free to install for personal and internal organizational use under the [GrOverview license](LICENSE). Redistribution, resale, rebranding and hosted services using the original code need written permission. Share the official installation link instead. This is not an open-source release; third-party components keep their [own licenses](THIRD-PARTY.md).

GrOverview is an independent project and is not affiliated with or endorsed by Home Assistant or the equipment manufacturers.
