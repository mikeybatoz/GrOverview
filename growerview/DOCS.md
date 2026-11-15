# Setup

1. Make a full Home Assistant backup, then [open GrOverview in Home Assistant](https://my.home-assistant.io/redirect/supervisor_app/?app=572737a2_growerview&repository_url=https%3A%2F%2Fgithub.com%2Fmikeybatoz%2FGrOverview). Enter your own Home Assistant address if asked, confirm adding the repository if prompted, and select **Install** on the GrOverview page. Requires Home Assistant OS with Supervisor; ARM64 and AMD64 are supported.
2. Start it and select **Open Web UI** while signed in as a Home Assistant administrator.
3. Select **Install connector & check configuration**. For an existing installation this reads **Update connector & check configuration**.
4. Setup preserves the prior connector and `configuration.yaml` in the add-on's private `/data/releases` folder. It adds `grow_journal:` only if the top-level configuration does not already contain it. Comments, `!secret` and `!include` entries are preserved.
5. If Home Assistant's configuration check passes, select **Restart Home Assistant** once. Existing installations with large journals can take several minutes to start.
6. The page verifies the running connector's release and opens the app. Enable **Show in sidebar** on the add-on page if desired.

Setup is never run automatically when the add-on starts. An update does not overwrite a customized connector without using the setup button. An incomplete install is reported rather than silently retried.

If the direct link does not open the app page, [add the GrOverview repository](https://my.home-assistant.io/redirect/supervisor_add_addon_repository/?repository_url=https%3A%2F%2Fgithub.com%2Fmikeybatoz%2FGrOverview), then find **GrOverview** under **Settings → Apps → Install app**. To add it manually, open that page's **⋮ → Repositories** and enter `https://github.com/mikeybatoz/GrOverview`. Older versions call these **Add-ons → Add-on Store**. If a link opens the wrong server, update the instance address at [My Home Assistant](https://my.home-assistant.io/).

## Updating without starting over

1. Keep dosing off and leave **Configuration → dosing_locked** enabled. Create a full Home Assistant backup including **Home Assistant and GrOverview**. The update dialog's app-only backup does not include the journal or photos.
2. In Home Assistant, open **Settings → Apps → GrOverview** and select **Update**. Older Home Assistant versions call this section **Add-ons**. Updates also appear in **Settings → System → Updates**. If the release is missing, use **Check for updates** on the Apps page.
3. Once the update finishes, select **Open Web UI → Update connector & check configuration**.
4. When the configuration check passes, select **Restart Home Assistant**. Wait for the app to verify the loaded release and reopen the journal.

Update the existing installation; there is no need to uninstall, create another journal or re-enter device credentials. The update replaces application/connector code, while keeping plants, care events, photos, sensor history, room/bed assignments, connection settings, pump calibration/limits, saved Veg/Flower recipes and OneDrive account/library preferences. Automatic dosing stays off after the connector restarts; the add-on lock remains enabled.

An app **Auto update** setting downloads the app image only. The connector update and Home Assistant restart above still need to be completed before the new interface opens. If the configuration check fails, setup restores the prior connector and reports the error. **Restore previous connector** restores code, not an older copy of your journal.

For OneDrive journals, keep the same connected account and library. A full HA backup still contains only the local cache plus local settings. Use **Download all & use local storage** first if the backup must contain every offloaded photo and historical reading for offline recovery.

## Dosing

`dosing_locked` defaults to `true`. Leave it enabled during installation, migration and pump calibration. It blocks arming and running doses through this add-on, including direct switch-on commands to configured pumps. Dose previews, sensor links, sliders, recipe presets, pump configuration and Stop remain accessible.

The lock does not control independent HA automations or Node-RED. A connector upgrade refuses to proceed if its dosing engine reports an active job or enabled reservoir. No setup operation runs pumps.

In **Reservoirs & dosing**, open **⚙ Settings**, then **Nutrients & pumps** for a reservoir. Add only the pumps you own, enter any product name (brand and line are optional), and assign each pump's on/off switch. Choose **Use in recipe** to include or exclude a pump; the arrow buttons set its mixing order. Removed pumps can be restored from **⚙ Settings → Removed pumps**.

Use the nutrient sliders and **Veg / Flower** buttons to save your own amounts. Product selection, pump connections, order, calibration and Bluelab setup live in **⚙ Settings**; the dashboard keeps the daily controls. Replacing a product, changing its purpose, moving it to another reservoir or restoring it clears that pump's previous amounts and commissioning confirmation. Changing its switch also clears the calibration rate and shutoff confirmation. These edits keep automatic dosing off; excluded pumps are omitted from previews and execution. Existing journal history is retained.

## Existing installations

The connector retains the `grow_journal` domain and storage paths. Records stay in `/homeassistant/.storage`, photos in `/homeassistant/grow_journal_media`, and existing entity identifiers remain unchanged. The UI is served by the add-on. The old `/grow-journal` panel and its files are not removed automatically, allowing rollback; hide/remove that duplicate panel only after validating the add-on.

**Restore previous connector** restores the saved code. If you edited `configuration.yaml` after setup, rollback keeps your newer edits. Restart HA after rollback. Use the original HA panel if the previous connector predates the add-on release endpoint.

On a fresh installation the same action removes the newly installed connector and restores the previous configuration, while retaining journal records. GrOverview keeps the existing `grow_journal` integration domain and `growerview` install slug so the name change does not create duplicate devices or storage.

## Device discovery

Native AC Infinity discovery starts with the connector and repeats every minute. Recognized, fresh and connectable Bluetooth devices are added once; disabled profiles stay disabled. A Home Assistant Bluetooth adapter or active proxy is required. No separate AC Infinity cloud integration is needed for these supported native devices.

Bluelab USB setup lists detected `/dev/serial/by-id` receivers. Select the correct receiver, release it from any other serial-reading software, then enable it once. The saved connection retries automatically and reconnects after restarts. It does not open every unknown serial port automatically. Edenic requires its own credentials. These measurement connections do not enable dosing.

### Leak detectors and phone alerts

Open **☰ → Equipment & connections → Leaks & alerts**, or **Govee devices → Water detectors & leak alerts**. Add a detector, assign a room/planter, and select any registered Home Assistant Companion phones/tablets as recipients. **Add a phone or tablet** explains registration; **Send test to saved recipients** checks the notification service. Optional SMS requires an existing Home Assistant SMS notify service and international-format phone numbers. No recipient is chosen automatically.

The Govee H5054 uses 433 MHz, which the Pi's Wi-Fi/Bluetooth radio cannot receive. For local discovery, connect a compatible RF receiver running rtl_433 and publish JSON **events** to Home Assistant's MQTT broker. Save its topic under **Govee H5054 connection setup** (default example `rtl_433/+/events`), press the dry detector's button, and select its received ID. No pre-existing Govee leak entity is required. Receiver hardware and rtl_433 are not bundled. A Govee H5040 gateway is a separate cloud route; this adapter does not configure that gateway or log into Govee. Existing HA moisture entities are an optional alternative.

Battery reports and last-heard times are shown when received. Leak incidents stay active across silence, battery packets, and restarts until a dry button report or a user-confirmed physical check. Acknowledging an incident does not clear it. History includes room/planter context and notification acceptance/failures; HA accepting a notification is not proof of handset delivery. Monitoring issues no pump or valve commands and remains available with dosing locked off.

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


### Sonoff and Broadlink

Open **Equipment & connections → Sonoff & Broadlink**. Existing Tasmota, SonoffLAN and Sonoff-labelled ESPHome devices appear automatically. Assign room labels here; use Room Designer’s sensor links for measurement placement. Pump-controller channels remain protected and are managed through Reservoirs & dosing.

The Broadlink tab shows connection status and lets you reconnect or add a device by IP. Open **Equipment & connections → Broadlink HVAC** to select a make/model from the pinned SmartIR code catalogue, link a Broadlink remote, or learn a custom remote. Existing SmartIR climate entities remain available; native catalogue profiles do not require that integration. The Broadlink app is needed for initial Wi-Fi setup; USB supplies power only. Mode, setpoint, fan and swing use the profile’s supported options. IR is one-way, so a requested setting is not proof of the equipment’s actual state. Named IR/RF learning and sending use Home Assistant’s Broadlink transport and notifications. This does not make an RM4 Pro a continuous leak receiver.

The 433 MHz tab accepts Tasmota `RfReceived` JSON from `tele/<bridge>/RESULT`. Listen and test the actual detector’s water contacts before mapping wet, dry or button codes. Retained packets cannot create live observations. An unrecognized `RfRaw` capture is shown as requiring decoding; timing bytes are never guessed to be a leak or battery value. Hardware/RF firmware support varies by Sonoff bridge revision. No automatic firmware flash is performed. Mapped detectors connect to Leaks & alerts for recipients, incident history and room/planter links. They remain unknown until a new report arrives; test/button packets do not clear an active leak. Users can explicitly confirm a detector is dry. Battery readings require a decoder that supplies them.

References: [Broadlink](https://www.home-assistant.io/integrations/broadlink/), [Tasmota RF Bridge](https://tasmota.github.io/docs/devices/Sonoff-RF-Bridge-433/), [Tasmota integration](https://www.home-assistant.io/integrations/tasmota/).
