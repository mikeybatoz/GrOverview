# Dependency and source notices

The application includes its existing attribution and source links. The release packager preserves text notices inside the bundled source directories.

- JSZip: bundled frontend vendor library, MIT option selected from its dual license. See `notices/JSZip-LICENSE.txt`.
- Edenic endpoint implementation reference: `farm-urban/fufarm_ha_edenic`. The existing MIT notice is retained at `notices/EDENIC-NOTICE.txt`.
- Govee cloud protocol reference: `lasswellt/govee-homeassistant` v2026.11.0 (MIT). The notice is retained at `notices/GOVEE-NOTICES.txt`. The current API-key setup uses that separately installed Home Assistant integration; existing Bluetooth sensor support is independent. Earlier native protocol helpers remain for compatibility. `aiomqtt` (BSD-3-Clause) is installed by Home Assistant from its published distribution.
- `ac-infinity-ble` (MIT), `pypdf` (BSD-3-Clause), `pyserial` (BSD): declared Python dependencies of the HA connector. Installed by HA, not vendored into this repository; their distributions retain their license metadata.
- AC Infinity protocol references include Viss/ha-ac-infinity-ble (MIT) and hunterjm/ac-infinity-ble (MIT). Their notices are included in `notices/AC-INFINITY-NOTICES.txt`; any adapted portions remain under those licenses.
- `aiohttp` (Apache-2.0 and MIT) and PyYAML (MIT): container dependencies, installed from their published packages with license metadata.
- Wyze Bridge: optional external service, AGPL-3.0. Its code/image is not included in this bundle. Linking or using it does not make it a proprietary implementation of GrOverview.
- PlantVillage, PlantNet and LLM Vision references in the UI do not mean their datasets, models or services are shipped in this add-on. The existing Windows AI worker is excluded.

Original GrOverview material is distributed under the Personal and Internal Use License in LICENSE. It does not replace or restrict the licenses of third-party materials. The Python/Alpine container base and its operating-system packages retain their upstream licenses and notices; see https://github.com/docker-library/python and https://pkgs.alpinelinux.org/ for their sources and package information.

- SmartIR climate catalogue (MIT, copyright 2019 Vassilis Panos): make/model metadata is pinned to the source revision recorded in `minisplit_catalog.json`. Selected Broadlink IR tables are downloaded on demand and cached locally. The MIT notice is retained in `notices/SMARTIR-LICENSE.txt`. Source: https://github.com/smartHomeHub/SmartIR. GrOverview does not require the SmartIR integration for these native profiles.
