# PNDZ Post Office — Standalone Project

**Status:** Design only. No scripts.

## Purpose
A persistent postal service for players and administrators to send packages to other players, including when sender or recipient is offline. The recipient retrieves the package later through their own inbox/collection system.

## Scope
- Player-to-player and administrator-to-player parcel sending; admin parcel management.
- Offline mail and durable server-side parcel storage across restarts.
- Private inboxes and configurable physical postal collection points.
- Ordinary parcels expire after seven real-world days if unclaimed.
- Secure item serialization, duplication prevention, capacity checks, logging, and permission management.
- Optional features from the existing functional wishlist must be assessed for this project independently.

## Excluded
- Random missed deliveries, six-hour timed events, random mailbox spawning, flashing beacons and recipient delivery tokens. These belong exclusively to **PNDZ Missed Package**.

## Conventions
- Classnames begin with `PNDZ_`; author `PNDZ`.
- Proposed settings: `$profile:PNDZ/PostOffice/`.
- If a types XML is required: nominal 0, min 0, lifetime 7200.

## Open decisions
- Exact send/receive UI and physical collection flow.
- Moderation privileges, item storage limits and blacklist.
- Whether optional wishlist features belong here.
