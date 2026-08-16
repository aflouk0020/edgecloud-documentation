# SCRUM-718 Device Organisation Dashboard

Device Inventory now provides a project selector, flat group selector, multi-tag filter (match all), clear-filter control, group display and organisation-tag display. Project selection loads only accessible projects and project-scoped organisation metadata.

Authorised users open **Manage groups and tags** to create, rename, search/list and delete metadata, view group members, assign or remove devices, and replace a device's multi-tag assignment. Confirmations and API conflict messages protect destructive actions. Loading, empty, success and error states are explicit, and the dialog collapses to one column for tablet-width layouts.

`PROJECT_ADMIN` can see Device Inventory and is forced into project-scoped access; `ADMIN` and `OPERATOR` retain their existing inventory capabilities. `VIEWER` has no organisation management controls.

Limitations intentionally match story scope: no nested or dynamic groups, bulk configuration, group alerting, maintenance windows, remote actions or firmware deployment. Manual evidence should capture group management, tag assignment, combined inventory filtering and tablet layout.
