# Sprint 9 Device Inventory Dashboard

The `/devices` page is a responsive, read-only inventory for platform administrators and operators. Its navigation entry is hidden from viewers, matching backend authorisation.

The desktop presentation uses a horizontally safe table. Tablet and narrow layouts switch to inventory cards. Both show status badges, heartbeat state, identifiers, type, registration, last communication and all currently supported optional metadata.

Search is submitted to the backend and accepts device name or exact device ID. Sorting supports name, status, last seen and registration date in either direction. Pagination requests ten devices per page and preserves offline entries. Loading, initial-empty, filtered-empty and recoverable error states use the existing Dashboard UI components.

The page does not expose editing, configuration, grouping, firmware deployment, remote commands or maintenance controls.
