# GrOverview

**Plants, spaces and live readings — inside Home Assistant.**

Journal a plant once. Connect it to its room and planter. Keep photos, care events and sensor history together.

**Built by mikeybatoz with extensive assistance from OpenAI Codex.** The foundation was mikeybatoz's existing Home Assistant growing system, AC Infinity reverse-engineering work, Bluelab data collection and BLE6 Node-RED dosing workflows. Codex helped turn that established work and the owner's requirements into this application through code implementation, refactoring, documentation and testing. Third-party projects retain their own credit and licenses.

[![Install GrOverview in Home Assistant](https://my.home-assistant.io/badges/supervisor_app.svg)](https://my.home-assistant.io/redirect/supervisor_app/?app=572737a2_growerview&repository_url=https%3A%2F%2Fgithub.com%2Fmikeybatoz%2FGrOverview)

[Install GrOverview](https://my.home-assistant.io/redirect/supervisor_app/?app=572737a2_growerview&repository_url=https%3A%2F%2Fgithub.com%2Fmikeybatoz%2FGrOverview) · [Add the repository only](https://my.home-assistant.io/redirect/supervisor_add_addon_repository/?repository_url=https%3A%2F%2Fgithub.com%2Fmikeybatoz%2FGrOverview)

**Experimental beta · 0.21.2-beta.3 · ARM64 and AMD64 · Home Assistant OS**

This is the official installer and support repository. Application development is private. Prebuilt images are downloaded from GitHub Container Registry; Home Assistant does not compile the application on your Pi.

## Install

1. Make a full Home Assistant backup.
2. Click **Install GrOverview** above. If My Home Assistant asks, enter your own Home Assistant address. Confirm adding the GrOverview repository if prompted.
3. On the **GrOverview** app page, select **Install**, then **Start** and **Open Web UI**. The link opens its page; it does not install or restart anything without your action.
4. Select **Install connector & check configuration**, then **Restart Home Assistant** when the check passes. The included connector supplies HA entities, Bluetooth/USB access and recording. No HACS installation is needed.
5. Leave **dosing_locked** enabled. Add your rooms, link sensors and assign plants to their planters.

Installation needs Home Assistant OS with Supervisor, Core 2026.11 or newer, and an administrator account. Home Assistant Container alone has no add-on store. Read [setup, backup and migration details](growerview/DOCS.md) before upgrading an existing installation.

**Manual fallback:** use [Add the repository only](https://my.home-assistant.io/redirect/supervisor_add_addon_repository/?repository_url=https%3A%2F%2Fgithub.com%2Fmikeybatoz%2FGrOverview), or open **Settings → Apps → Install app → ⋮ → Repositories** and add `https://github.com/mikeybatoz/GrOverview`. Then find **GrOverview** and select **Install**. Older HA versions call this **Add-ons → Add-on Store**. If My Home Assistant opens the wrong server, change the instance address at [my.home-assistant.io](https://my.home-assistant.io/).

## Update an existing installation

1. Keep dosing locked off and make a full backup including **Home Assistant and GrOverview**.
2. Open **Settings → Apps → GrOverview → Update** (or **Add-ons** on older versions). If needed, select **Check for updates** on the Apps page.
3. Select **Open Web UI → Update connector & check configuration**.
4. After the check passes, select **Restart Home Assistant** and wait for the journal to reopen.

Your existing journal, photos, sensor history, room/bed links, device settings, pump calibrations and saved recipes stay in place. Do not uninstall or create a new journal. App auto-updates still require the connector/restart step. OneDrive journals retain their account/library; a fully offline backup requires downloading the cloud journal first. See [update and backup details](growerview/DOCS.md#updating-without-starting-over).

## What is included

| Area | What it does |
| --- | --- |
| Plant journal | Individual plant records, shared care events, photos, dates and planter history |
| Room designer | Room and bed placement, equipment, positioned sensors and links back to the journal |
| Measurements | Automatic recording of linked HA readings, charts, DLI calculations and saved stage comparisons |
| Optional OneDrive storage | Your personal OneDrive stores journal records, photos and full sensor history; Home Assistant keeps a working cache and unsent changes |
| AC Infinity | Native Bluetooth discovery and supported controller profiles; requires an HA radio or active proxy |
| ESPHome sensors | Link compatible Home Assistant entities to rooms, planters and sensor history |
| Govee sensors and leak alerts | Compatible sensor links; H5054 reports through supported MQTT/RF receivers, with battery reports when supplied and selectable phone notifications |
| Wyze and other cameras | Camera assignment, snapshots and dated reviews using configured camera transport; see dependencies below |
| Sonoff and Broadlink | Existing device connections, RF detector mapping, model-based mini-split profiles and guided IR learning |
| Bluelab | USB receiver selection and automatic reconnection after setup; optional Edenic account connection |
| Reservoirs | Custom nutrients and pumps in Settings; nutrient sliders, Veg/Flower presets, calibration and dosing controls behind a default-on dosing lock |
| Diagnostics | Connection status and missing/stale data in a dedicated page |

## Beta boundaries

- Physical hardware support depends on model, firmware, radio/USB availability and configuration. A detected device is not proof that every control is supported.
- Existing Home Assistant cameras can be linked. Wyze uses an additional transport service; the portable video setup is still being completed.
- Plant Sense journal/sensor checks are included. Local image analysis needs a separately configured worker; its model/runtime is not bundled in this beta. Photo results are observations to review, not a confirmed diagnosis.
- DLI from lux requires a configured conversion factor and is an estimate. Missing readings are not silently treated as zero.
- OneDrive storage uses a personal Microsoft account and stores the shared installation journal. Device configuration and credentials stay local. For a complete offline journal backup, download the cloud journal first through **Options → Journal storage**.
- The dosing lock blocks commands through this add-on, including activation of configured pump switches. It does not disable separate Node-RED flows, HA automations, vendor apps or an older panel. Leave dosing off until pump calibration and commissioning are complete.

## Tested

The current release passes 409 journal tests and 48 add-on tests (cloud cases overlap), including scheduled cloud-sync dispatch and settings preservation through updates/rollback. Published beta.1 → beta.2 → beta.3 updates were exercised through Home Assistant on an isolated PC: 35 journal events, 1,008 readings, 16 photo hashes, room/bed links, pump settings, Veg/Flower recipes and OneDrive preferences matched afterward. Earlier releases passed full-backup restore and OneDrive recovery into an empty journal. These tests do not establish compatibility with every physical device. AMD64 and ARM64 images are provided.

## Get help

[Installation guide](growerview/DOCS.md) · [Changes](growerview/CHANGELOG.md) · [Report a problem](https://github.com/mikeybatoz/GrOverview/issues/new/choose)

Please include your add-on version, HA version, device model and steps to reproduce. Remove passwords, API keys, tokens, photographs and other private records from logs before sharing them.

## Use and ownership

Official releases are free to install for personal and internal organizational use under the [GrOverview license](LICENSE). Redistribution, resale, rebranding and hosted services using the original code need written permission. Share the official installation link instead. This is not an open-source release; third-party components keep their [own licenses](THIRD-PARTY.md).

GrOverview is an independent project and is not affiliated with or endorsed by Home Assistant or the equipment manufacturers.
