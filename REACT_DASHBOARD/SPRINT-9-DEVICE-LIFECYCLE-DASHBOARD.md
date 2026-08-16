# Sprint 9 Device Lifecycle Dashboard

The existing `/devices` inventory now provides an integrated lifecycle workflow. ADMIN sees Register, Edit, Deactivate/Reactivate, Remove, and History controls. OPERATOR sees Edit, Deactivate/Reactivate, and History; VIEWER has no Device Inventory navigation/access under the established role convention.

Registration/editing uses a responsive modal with mandatory name, type, and IP validation plus description, location, firmware, and operating system fields. Mutation success refreshes server-backed inventory; backend validation and conflict messages are surfaced. Removal requires explicit confirmation and appears only for inactive devices. History is read from the durable lifecycle table.

Project assignment continues to display only when a supported Project Service association is available. It is not editable here and no placeholder data is created.
