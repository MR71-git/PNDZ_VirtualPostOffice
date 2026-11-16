# PNDZ Virtual Post Office

**DayZ mod — Planning & Design (v0.1)**  
**Author:** PNDZ  
**Status:** Requirements gathering; no scripts or mod binaries created.

A persistent virtual postal service for DayZ: players and moderators send items, administrators manage parcels, and configurable parcel pickup locations bring deliveries into the game world.

## Confirmed requirements
- Players and moderators can send items to other players.
- Administrators can add and remove items/parcels.
- Each player has a private inbox.
- Parcels remain available for **7 real-world days** after delivery to the inbox; uncollected parcels are automatically deleted by the server.
- Standalone parcel pickup points can be placed in the world. The custom 3D object will be supplied later.
- Periodic random deliveries generate a player notification: the courier was missed and a parcel awaits collection at a pickup point.
- All project communication and documentation are in English, even if requirements arrive in Dutch.
- Do not begin scripting until explicitly approved.

## PNDZ development conventions
- Item and mod classnames use the `PNDZ_` prefix.
- Author: `PNDZ`.
- Configuration lives under `$profile:PNDZ/<ModName>/`; proposed project path: `$profile:PNDZ/VirtualPostOffice/`.
- Use JSON settings.
- If a types XML is needed, default to nominal 0, min 0, lifetime 7200 seconds.
- Provide settings documentation and a README.

## Design proposals — NOT YET APPROVED
- Client + server mod for UI, pickup objects, and server-authoritative parcel data.
- Identify players with their persistent DayZ player identity; store parcels persistently across restarts.
- Prevent duplicate claims, invalid item states, and unauthorized admin actions.
- Preserve relevant item state (attachments, condition, ammunition, contents where supported).
- Validate available inventory space when collecting a parcel.
- Audit all sends, collections, expirations and administrative changes.
- Configurable delivery interval, probability, eligible players, loot tables, and personal cooldown.
- Multilingual player messages (English, German, French, Spanish, Russian; Dutch optional).
- Hybrid delivery model: send through a menu, collect at a physical pickup point (recommended, not selected).

## Open decisions
1. Physical, fully virtual, or hybrid sending/collection?
2. May moderators administer other players' mail, or only send packages?
3. Can parcels contain nested containers, weapons with attachments, liquids, and damaged items?
4. How are offline recipients addressed and discovered?
5. Are random deliveries for online players only or also offline players?
6. Which pickup point receives a parcel; can a player choose?
7. What happens if collection fails due to inventory capacity?
8. What are the delivery interval, odds, loot tables and limits?
9. Should expiry return packages to sender or delete permanently? Current requirement is deletion.
10. How should UI interactions, translations and logging be implemented?

## Planning roadmap
1. Define functional scope and decisions.
2. Design parcel lifecycle and data integrity.
3. Design pickup point placement and interactions.
4. Design random delivery events and loot selection.
5. Define moderator/admin permissions and audit logs.
6. Design UI, notifications and localization.
7. Review technical architecture, storage, compatibility and security.
8. Begin development **only after explicit approval**.
9. Test, optimize and prepare release.

## Requested functional extensions (design wishlist)
The following **10 extensions have been explicitly requested** and are tracked in [Functional Wishlist](docs/FUNCTIONAL_WISHLIST.md): parcel tracking; nearest pickup point; loot categories; personal cooldown; weighted loot tables; audit log; item blacklist; offline mail; sending limits; webhooks.

These are design requirements awaiting detailed decisions, **not implemented features**.

## Other potential extensions (ideas only)
Parcel tracking; shipping fees; cash on delivery; anonymous parcels; returns to sender; map markers; nearest pickup point; pickup capacity; role-restricted pickup points; weighted common/rare/epic/legendary reward tiers; special delivery events; player cooldowns; prohibited-item blacklist; send limits; offline mail; Discord webhooks.

See the GitHub Issues for individual design decisions and planning work. No implementation code is part of this initial repository.
