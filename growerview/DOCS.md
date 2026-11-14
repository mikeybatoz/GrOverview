# Setup

1. Install the GrOverview add-on in Home Assistant OS. ARM64 and AMD64 are the declared target architectures.
2. Start it and select **Open Web UI** while signed in as a Home Assistant administrator.
3. Select **Install connector & check configuration**. For an existing installation this reads **Update connector & check configuration**.
4. Setup preserves the prior connector and `configuration.yaml` in the add-on's private `/data/releases` folder. It adds `grow_journal:` only if the top-level configuration does not already contain it. Comments, `!secret` and `!include` entries are preserved.
5. If Home Assistant's configuration check passes, select **Restart Home Assistant** once. Existing installations with large journals can take several minutes to start.
6. The page verifies the running connector's release and opens the app. Enable **Show in sidebar** on the add-on page if desired.

Setup is never run automatically when the add-on starts. An update does not overwrite a customized connector without using the setup button. An incomplete install is reported rather than silently retried.

## Dosing

`dosing_locked` defaults to `true`. Leave it enabled during installation, migration and pump calibration. It blocks arming and running doses through this add-on, including direct switch-on commands to configured pumps. Dose previews, sensor links, sliders, recipe presets, pump configuration and Stop remain accessible.

The lock does not control independent HA automations or Node-RED. A connector upgrade refuses to proceed if its dosing engine reports an active job or enabled reservoir. No setup operation runs pumps.

## Existing installations

The connector retains the `grow_journal` domain and storage paths. Records stay in `/homeassistant/.storage`, photos in `/homeassistant/grow_journal_media`, and existing entity identifiers remain unchanged. The UI is served by the add-on. The old `/grow-journal` panel and its files are not removed automatically, allowing rollback; hide/remove that duplicate panel only after validating the add-on.

**Restore previous connector** restores the saved code. If you edited `configuration.yaml` after setup, rollback keeps your newer edits. Restart HA after rollback. Use the original HA panel if the previous connector predates the add-on release endpoint.

On a fresh installation the same action removes the newly installed connector and restores the previous configuration, while retaining journal records. GrOverview keeps the existing `grow_journal` integration domain and `growerview` install slug so the name change does not create duplicate devices or storage.

## Device discovery

Native AC Infinity discovery starts with the connector and repeats every minute. Recognized, fresh and connectable Bluetooth devices are added once; disabled profiles stay disabled. A Home Assistant Bluetooth adapter or active proxy is required. No separate AC Infinity cloud integration is needed for these supported native devices.

Bluelab USB setup lists detected `/dev/serial/by-id` receivers. Select the correct receiver, release it from any other serial-reading software, then enable it once. The saved connection retries automatically and reconnects after restarts. It does not open every unknown serial port automatically. Edenic requires its own credentials. These measurement connections do not enable dosing.

## Permissions

The add-on exposes no host port. It accepts application requests only through Supervisor ingress, and checks the forwarded user against HA's active administrators. Missing user identity is rejected. The server keeps `SUPERVISOR_TOKEN` out of browser responses and serves only the UI directory, never the connector/configuration directories.

It maps HA's configuration folder read/write solely to manage the connector. `homeassistant_api` supports entities and existing journal commands. `hassio_role: homeassistant` supports configuration checking and a requested Core restart. It does not request host networking, privileged hardware access, Docker access or protection-mode changes. The HA connector uses HA's existing Bluetooth and USB access.

## Backups and uninstalling

### Optional OneDrive journal storage

Open **GrOverview menu → Options → Journal storage**, or **⚙ Settings → Storage**.

1. Choose **Connect OneDrive in Home Assistant** and finish Microsoft's sign-in. This uses Home Assistant's native OneDrive integration and currently supports **personal Microsoft accounts**, not work/school accounts. GrOverview checks the drive type before creating or accessing journal folders and rejects work/school storage. No password or API key is entered in GrOverview.
2. Return to **Journal storage → Refresh accounts** and select the account.
3. Set the local photo cache limit and select **Use OneDrive for this journal**. This authorizes uploading the shared installation's journal, photos, room/planter records and sensor history into that account's Home Assistant app folder.
4. Wait for a verified sync. Uploads run every five minutes. After verification, HA keeps the working journal metadata, the latest 1,000 readings, the selected photo cache and any unsent changes. Uncached photos and older charts need OneDrive access; local journaling continues during outages. The cache may exceed its limit while offline or while photos are in use.

This is primary journal storage with a local working cache, not a Home Assistant backup destination. Doser configuration, operational settings, secrets, HA Recorder and existing HA backup files stay local. All administrators of the installation share this journal/account; this does not create separate journals for individual HA logins.

Use **Download all & use local storage** before disconnecting OneDrive, downgrading to a version without this feature, or preparing a fully offline journal backup. It downloads the complete history and referenced photos before disabling cloud mode. The OneDrive copy is retained. Ensure sufficient local space for that download. A routine HA backup in cloud mode contains only the local cache and connection configuration, not every offloaded photo/history chunk.

For recovery on a fresh installation, connect the same Microsoft account, open **Recover an existing OneDrive journal → Find my journals**, select the library and restore it. Recovery refuses to replace a journal containing local plants, events or readings. Restart Home Assistant after recovery to reload restored device links. Keep a separate full HA backup for account configuration, operational device settings and credentials. Do not let two live installations write to the same cloud library: conflicting revisions stop sync instead of silently overwriting records.

The PC Supervisor lab verified real personal Microsoft sign-in, upload and readback of 1,008 readings and 16 photos, local cache eviction, recovery into an empty journal and download back to local storage. Automated tests also cover outages, corrupt uploads, conflicting writers and failed local writes. This does not establish production-scale throughput or every account/network condition.

API references: [Home Assistant OneDrive](https://www.home-assistant.io/integrations/onedrive/), [Microsoft app folders](https://learn.microsoft.com/en-us/graph/onedrive-sharepoint-appfolder), [file upload](https://learn.microsoft.com/en-us/graph/api/driveitem-put-content), [conditional metadata updates](https://learn.microsoft.com/en-us/graph/api/driveitem-update).

Use a full Home Assistant backup including **Home Assistant and GrOverview**. The connector's existing SQLite backup hooks remain bundled. An add-on-only backup contains installer state and rollback copies, not the journal or photos in HA's configuration directory.

Uninstalling the add-on does not erase journal records or remove the connector. Removing the connector is a separate administrative action; first stop relevant automations and retain a verified full backup.

## External components

This package preserves existing integrations. It does not bundle a vision model, the Windows Plant Sense worker, Wyze Bridge or a video transport process. Existing configured services remain usable through the connector, but a fresh user's camera transport and local AI need their own portable setup work before a complete public release. This beta does not claim those external components are automatically installed.

Camera/entity dialogs use the parent Home Assistant frontend when opened through ingress. Standalone browser testing shows an entity-information fallback. Voice input still requires browser microphone permission and an HTTPS Home Assistant session.

## Help

Use **Add-on setup → Check connection** for setup problems and the app's **Diagnostics** page for equipment and sensor problems. See HA logs for configuration-check errors. Do not put account passwords, API keys or backup contents in public bug reports.
