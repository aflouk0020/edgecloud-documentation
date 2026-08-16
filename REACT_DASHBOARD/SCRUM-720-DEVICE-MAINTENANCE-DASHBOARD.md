# SCRUM-720 Dashboard and User Guide

## Inventory experience

Device Inventory displays a dedicated `MAINTENANCE` badge and reason in the desktop table and responsive card. The badge is separate from lifecycle and heartbeat indicators so intentional maintenance is not confused with `INACTIVE` or `OFFLINE`.

The **Maintenance** action opens a responsive details dialog containing current state, reason, enabled time, enabling actor UUID, scheduled end, lifecycle/heartbeat context, and newest-first maintenance history.

## Operator workflow

`ADMIN` and `OPERATOR` users can:

1. enter an optional reason and scheduled end;
2. review a confirmation before enabling maintenance;
3. receive loading, success, validation, or API-error feedback;
4. review `ENABLED`, `DISABLED`, and `EXPIRED` events;
5. confirm manual disable.

The scheduled end must be in the future. `PROJECT_ADMIN` and `VIEWER` do not receive mutation controls under the current backend contract. UI visibility is only a convenience; Device Service remains the security authority.

Existing inventory search, pagination, sorting, lifecycle actions, configuration, group/tag organisation, and heartbeat details remain available.

## Current limitations

Actor identity is displayed as a UUID because the Dashboard does not perform a user-directory lookup. Scheduled future start, remote distribution, remote commands/remediation, and firmware operations are outside this story. Interactive browser screenshots remain **PENDING MANUAL CAPTURE**.
