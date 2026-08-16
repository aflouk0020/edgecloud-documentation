# SCRUM-717 Device Configuration Management

Device Service owns centrally managed device-agent settings: polling, heartbeat and metrics intervals, environment, API endpoint, logging level, and tags. Device identity remains in SCRUM-716 metadata; Project Service remains the sole owner of device-to-project associations; alert thresholds remain in Alert Service. No duplicate project, device-name, or alert ownership was introduced.

Configuration is platform-scoped because the existing Device Inventory is restricted to platform ADMIN and OPERATOR roles. Project-scoped roles are explicitly denied and therefore cannot cross project boundaries through this API. Configuration templates are reusable platform defaults: ADMIN creates/updates them, while ADMIN and OPERATOR can list/apply them. Future project-specific template policy should be orchestrated through Project Service rather than copying project membership into Device Service.

Each device has at most one current configuration and an immutable, ordered version history. Mutation locks the device and current configuration, applies the settings, increments the version, and records action, changed fields, actor, timestamp, and a complete snapshot in one transaction. An unchanged PUT is idempotent and creates no history. Restore copies a historical snapshot into a new version; history is never rewritten.

Inactive configurations are readable for evidence but immutable. Missing/deleted devices are rejected. Device lifecycle and identity rows are not mutated. Settings are stored centrally only: remote distribution, acknowledgement, drift detection, or automatic agent synchronisation belongs to later Sprint 9 work.
