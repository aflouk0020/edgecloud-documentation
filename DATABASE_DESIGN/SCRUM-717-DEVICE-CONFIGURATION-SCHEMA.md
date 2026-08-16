# SCRUM-717 Device Configuration Schema

Flyway `V3__add_device_configuration_management.sql` adds:

- `device_configurations`: one current configuration per Device Service UUID, with version and audit columns.
- `device_configuration_versions`: immutable snapshots, unique `(device_id, version)`, indexed newest-first.
- `device_configuration_templates`: unique platform template names with configuration and creator/updater audit data.

Tags are bounded JSON arrays stored in `VARCHAR(2000)` and serialized/deserialized by the service. No cross-service foreign key is created. Device existence and lifecycle are enforced transactionally in the service, allowing independently owned Project, Monitoring, and Alert evidence to remain decoupled.
