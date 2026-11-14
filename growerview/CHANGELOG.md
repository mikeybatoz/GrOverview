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
