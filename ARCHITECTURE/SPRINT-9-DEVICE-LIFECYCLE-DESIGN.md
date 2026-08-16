# Sprint 9 Device Lifecycle Design

Device Service remains the source of truth for registration metadata and lifecycle state. Flyway now owns the production schema: V1 describes the pre-existing inventory table for new installations, while V2 safely upgrades existing installations with metadata, `active`, `updated_at`, query indexes, and `device_lifecycle_history`. Existing populated schemas are baselined at V1, so only the additive V2 migration runs.

`ONLINE`/`OFFLINE` remains operational state; `active` is the lifecycle gate. Deactivation marks a device inactive and offline. Inactive devices remain visible in inventory, cannot send a heartbeat, and are skipped by status evaluation. Reactivation leaves the device offline until a real heartbeat arrives.

Lifecycle operations are transactional. Each successful registration, metadata update, deactivation, reactivation, and deletion records time, acting user ID, device snapshot, resulting active flag, and detail. Duplicate detection is backed by the existing unique device-name constraint. Permanent deletion requires an inactive device and removes only the Device Service row; history and independently owned monitoring evidence remain intact.

The existing Gateway `/api/v1/devices/**` route and JWT propagation already cover these paths, so no Gateway change was required. ADMIN owns registration/removal; ADMIN and OPERATOR may read, edit, deactivate, reactivate, and inspect history. VIEWER and unauthenticated callers cannot manage devices.
