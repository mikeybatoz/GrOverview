# 0.21.2-beta.5

- Add optional Google Drive journal storage alongside OneDrive, with account verification, upload progress and bounded local caches. Home Assistant still runs the app and retains device settings and credentials.
- Schedule camera captures independently of AI processing, defaulting to eight-hour snapshots. Prioritize newly uploaded photos and retry deferred assessments when the configured vision worker is available.
- Allow a longer bounded processing window for optional local image analysis while keeping journal and sensor monitoring responsive. Image analysis still requires a separately configured worker.
- Tap reservoir water temperature to switch °C/°F, or nutrient concentration to cycle EC, ppm500 and ppm700. Save display choices per reservoir across reloads and restarts, independently of dosing limits, recipes and pump operation.
- Request active Bluetooth scan responses for saved AC Infinity controllers, and retain verified identities across name-only advertisements without refreshing old measurements. Release scan requests when profiles are disabled or unloaded.
- Load the AC Infinity inventory immediately when reopening its page instead of showing an empty grid until the periodic refresh.
- Refresh saved outlet-controller settings when live port data arrives even if no climate probe is attached.
- Show Enable dosing when off and Stop dosing when enabled or running, including mixing waits. Show rejected activation errors and refresh status without erasing edits.
- Autosave live nutrient amounts, pH/PPM limits and separate Veg/Flower profiles. Acknowledge a save only after durable storage; retain failed drafts for retry after reload. Changing recipes leaves automatic dosing off.
- Match BLE6's 600-second periodic check and five-minute Bluelab freshness window. Extra sustained-demand and mixing waits default to zero; preserve custom timing during migration.
- Remove mandatory reservoir volume, water-level input, device-side cutoff confirmation and manual exclusivity checkbox from fixed-dose setup. Optional linked level sensors remain enforced. Dose/runtime/daily limits are optional; only known uncommissioned import defaults are cleared.
- Keep PPM preset automations out of competing-pump detection, exclude unmapped imported Silica/Boost channels until configured, and allow pH correction independently of high PPM. Preserve mappings, quantities, presets and history. Native delivery remains sequential and dosing stays off after migration.
- Keep scheduled sensor checks and camera capture running while a local AI assessment is pending.

# 0.21.2-beta.4

- Add API-key-only Govee setup under the Govee page's settings gear. The form skips optional account sign-in and reports setup errors without erasing the entered key. It uses the separately installed Govee Cloud Integration; existing BLE readings remain independent.
- Move page-specific connection and discovery controls into the settings gear. Hide Govee devices without available readings or controls while retaining their saved links and history.
- Require confirmation before clearing a recorded leak incident, and reject stale confirmations or clearing an entity that still reports wet. Connecting Govee does not run alarm or notification tests.
- Add per-plant camera journal support with tag/trunk association, individual crops, duplicate prevention and diagnostics for unreadable or ambiguous tags. A configured camera transport and compatible local vision worker are still required.
- Add selectable camera-meter regions and dated visual readings linked to rooms and planters. Preserve their source photos in journal storage, including OneDrive.
- Retain all reservoir controls, calibration, recipes and the default dosing lock. Connector updates preserve existing journal records and settings.

# 0.21.2-beta.3

- Fix scheduled OneDrive journal sync running outside Home Assistant's event loop. Background uploads use the existing five-minute schedule and retain unsent records on failure.
- Document the Home Assistant app update, connector update and restart sequence, including full-backup requirements and OneDrive cache behavior.
- Keep the journal footer and Home Assistant integration version aligned with the installed app release.
- Add regression coverage for operational settings and new journal records surviving connector updates and rollback. Keep dosing locked off and retain every beta.2 feature.

# 0.21.2-beta.2

- Put nutrient and pump setup, calibration, reservoir links and connection options in Reservoirs & dosing → Settings. Keep readings, nutrient sliders, Veg/Flower presets and dosing controls on the dashboard.
- Support custom nutrient products, any number of pumps, recipe inclusion, ordering and removal/restoration without erasing delivery history. Product or connection changes require their relevant amounts and calibration to be reviewed.
- Add Sonoff and Broadlink connection pages, a model-based mini-split catalogue and guided IR learning with controller-style remotes. IR requests do not confirm the appliance's actual state.
- Add Govee H5054/compatible leak reporting through supported MQTT/RF receivers, room/planter links and selectable notification recipients. Compatible receiver hardware is required.
- Improve camera assignment and dated checks, with shared photo/camera review context. Camera transport and local image-analysis workers remain separate dependencies.
- Preserve the default dosing lock and existing records. Editing setup leaves automatic dosing off.

# 0.21.2-beta.1

- Add optional personal OneDrive storage for journal records, photos and complete sensor history, with a bounded local photo/readings cache and retained unsent changes.
- Add Storage under Options, the settings gear and Diagnostics; include account connection, sync status, recovery and download-to-local controls.
- Verify uploaded content before evicting local copies, detect conflicting writers and protect rollback to older connectors.
- Verify Microsoft reports a personal drive before accessing journal folders; reject work/school and unrecognized drive types without writing to them.
- Load cloud photos and history through the existing charts, exports and Plant Sense review paths.
- Validate personal Microsoft sign-in, real upload/readback, cache eviction, clean recovery and return to local storage in the isolated PC Supervisor lab. Keep dosing locked off.
- Handle OneDrive’s escaped folder descriptions and keep recovery choices open during refresh.
- Keep the full menu accessible when a new installation has an empty journal.

# 0.21.1-beta.4

- Prepare a public installer repository, with the development source kept private.
- Include the personal/internal-use license and retained third-party notices in distributed images.
- Add versioned multi-architecture image publishing and an installation guide.
- Keep all existing controls and the default dosing lock unchanged.

# 0.21.1-beta.3

- Use GrOverview as the app and add-on display name.
- Retain the grow_journal domain, growerview install slug, entity IDs and storage paths for compatibility.

# 0.21.1-beta.2

- Validate AMD64 and ARM64 Docker builds, with ARM64 startup under emulation.
- Validate fresh installation, update, rollback and full backup restoration under a real Supervisor on the development PC.
- Make undo available after a fresh connector installation.
- Explain a connector version mismatch and recover the restart screen after a disconnected request.
- Verify the native AC Infinity bridge initializes automatically on a fresh installation, with dosing requests locked off.

# 0.21.1-beta.1

- Package the current GrOverview frontend and HA connector for the Add-on Store.
- Add an administrator-only ingress host and connector setup/rollback workflow.
- Preserve journal storage, photos, sensor links and existing control pages.
- Default to locked dosing requests.
- Include the separate Diagnostics page.

Beta releases. See the repository release page for published images and limitations.
