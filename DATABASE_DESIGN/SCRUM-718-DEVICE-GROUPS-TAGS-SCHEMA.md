# SCRUM-718 Device Groups and Tags Schema

Flyway migration `V4__add_device_groups_and_tags.sql` adds four Device Service-owned tables: `device_groups`, `device_group_memberships`, `device_tags`, and `device_tag_assignments`.

Groups are flat and membership is many-to-many, allowing a device to be in operationally overlapping groups. Tags are also many-to-many. `project_id` is a logical external identifier and deliberately has no cross-service foreign key. `(project_id, normalised_name)` is unique for groups and tags. Membership and assignment tables use composite primary keys plus reverse-lookup indexes. Project/name, device/group, device/tag and tag/device access paths are indexed for filtered inventory queries.

Local foreign keys may cascade membership or assignment metadata, but never delete `edge_devices`. The service blocks deletion of a populated group. Deleting a tag removes only local assignments; telemetry, monitoring history, lifecycle history and devices are unaffected.

SCRUM-717 configuration JSON may contain agent-facing configuration keys called `tags`. Those remain versioned configuration payload data. SCRUM-718 `device_tags` are the authoritative searchable inventory-organisation metadata; no unsafe implicit migration between those different concepts is performed.
