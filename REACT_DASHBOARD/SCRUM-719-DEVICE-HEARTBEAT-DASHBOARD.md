# SCRUM-719 Dashboard Guide

Device Inventory now includes a five-state heartbeat filter and shows status, next expected heartbeat, and missed-heartbeat count without crowding the core device metadata.

Select **Heartbeat** on a device row/card to open the responsive details dialog. It displays current policy/state, last and next heartbeat, missed count, recovery time, connection duration, statistics, and paginated transition history. The dialog includes loading, empty, and error states. Device Configuration includes heartbeat timeout and prevents a timeout that is not greater than twice the interval.

Access remains role-aware: platform administrators/operators use global details; project administrators use verified project-scoped endpoints. This UI does not send remote commands or create alerts.
