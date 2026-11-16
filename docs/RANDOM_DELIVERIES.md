# Random Delivery Design — v0.3

**Status:** Requirements and design only; no scripts.
**Group integration:** External third-party party/group mod (exact mod to be supplied later).

## Confirmed requirements
1. Random parcels expire no later than **6 real-world hours after the first notification** to the selected player.
2. The server selects a **random suitable location within a city or town** on the map.
3. Exclude water, toxic areas and unsafe/unsuitable terrain.
4. Collection is authorized **only for the notified player or a member of that player's group**.
5. The regular seven-day inbox expiration remains unchanged for ordinary mail.

## Proposed lifecycle
1. Select an eligible recipient and reward.
2. Select a random candidate city/town location.
3. Validate against water, toxic zones, terrain suitability and object collisions; retry or skip if no safe point exists.
4. Persist package ID, intended recipient, eligible group identity policy, location and first-notification time.
5. Notify the player and start a fixed 6-hour deadline.
6. Allow server-authorized pickup once; deny unauthorized access.
7. Remove or invalidate the package at expiration; record the outcome in the audit log.

## Design safeguards
- Server-authoritative location validation and pickup permission checks.
- A repeat notification or restart must not extend the original deadline.
- Define whether group membership is checked at delivery time or collection time.
- Integrate with an external party/group mod (name/API unknown until supplied); do not assume DayZ Expansion Groups or implement a custom group system.
- Define what location information is shown and whether it is visible to group members.
- Decide whether packages are physical spawned objects or logical inventory attached to a pickup point.
- Define fallback when no safe city/town location is found.
- Define cleanup if a package object is destroyed, moved or inaccessible.

## Example notification (proposed wording)
> You missed your delivery! Your parcel is waiting at a pickup location. You or a member of your group have 6 hours from this notification to collect it.

## Open design questions
- Which external party/group mod and version is installed? How can membership be queried securely?
- Should the player receive map coordinates, a marker, or just a town name?
- Should the six-hour timer run while the recipient is offline? Proposed: yes, real time.
- What minimum safe distance from toxic zones, water, roads and structures should be enforced?
- Are parcel locations shared among group members automatically?

## External group integration — design decision v0.4
- **Confirmed:** An existing third-party party/group mod will be used; its name and integration details will follow.
- **Not selected:** DayZ Expansion Groups or a custom PNDZ group system.
- Keep group lookup behind a conceptual integration boundary so the postal system is not tied to an unconfirmed API.
- Verify collection rights server-side; never trust client-supplied group membership.
- Pending policy: membership at first notification versus at pickup, including players who join or leave the group.
- If the group mod is missing or fails to respond, proposed safe fallback: only the notified recipient can collect (requires approval).
