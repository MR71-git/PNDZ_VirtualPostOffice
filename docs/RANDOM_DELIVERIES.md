# Random Delivery Design — v0.3

**Status:** Requirements and design only; no scripts.
**Group integration:** LBmaster's Advanced Groups (integration API/version to be verified).

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
- Which version of LBmaster's Advanced Groups is installed, and what supported server-side interface exposes group membership?
- Should the player receive map coordinates, a marker, or just a town name?
- Should the six-hour timer run while the recipient is offline? Proposed: yes, real time.
- What minimum safe distance from toxic zones, water, roads and structures should be enforced?
- Are parcel locations shared among group members automatically?

## External group integration — design decision v0.4
- **Confirmed:** **LBmaster's Advanced Groups** is the selected external group system. Its version and supported server-side integration interface still need verification.
- **Not selected:** DayZ Expansion Groups or a custom PNDZ group system.
- Keep group lookup behind a conceptual integration boundary so the postal system is not tied to an unconfirmed API.
- Verify collection rights server-side; never trust client-supplied group membership.
- **Confirmed policy:** evaluate membership at pickup time. Players joining the recipient's group gain access; players leaving lose access.
- If the group mod is missing or fails to respond, proposed safe fallback: only the notified recipient can collect (requires approval).

## Selected group dependency — v0.5
- Selected: **LBmaster's Advanced Groups**.
- Confirm compatibility with the installed release and its supported server-side group membership API before implementation.
- Confirm supported API for current membership at collection time; group membership changes must take effect immediately for access control.
- No API classes, method names, or dependency declarations are assumed until documentation or mod files are reviewed.

## Confirmed access-control policy — v0.6
- The notified recipient **always** has collection permission for their own unexpired parcel.
- Current members of the recipient's LBmaster's Advanced Groups party may collect the parcel.
- Membership is evaluated **at the moment of collection**, not frozen at delivery.
- Newly joined group members gain access; former members immediately lose access.
- Every other player is **denied collection**, even if they locate the parcel.
- Authorization must be enforced server-side, and successful collection is atomic (only one claimant receives the parcel).
- Implementation details remain pending verification of the group's supported server-side interface.

## Physical parcel object — confirmed design v0.7
- Each random delivery appears as a **physical postbox/mailbox mounted on a stand** at the validated town/city location.
- A **flashing indicator light** makes the mailbox noticeable in the world.
- The mailbox object is **removed when the parcel is successfully collected** by the notified recipient or a current member of their LBmaster's Advanced Groups party.
- The mailbox object is also **removed when the parcel is deleted or expires** (6 real-world hours after first notification).
- Access remains server-authorized; finding the object does not allow unrelated players to collect it.
- Proposed safeguards: synchronize object removal to clients, prevent duplicate collection, and clean up orphaned objects after server restart.
- Visual details (mailbox shape, stand, lamp color and blink pattern) and final model/assets are still to be determined.
- Open decision: whether unauthorized players may see the mailbox but cannot interact with it (recommended), or whether visibility should be restricted.

## Public mailbox visibility and personalized token — v0.8
### Confirmed
- Every player can see the physical mailbox and flashing indicator.
- The intended recipient receives a **personalized access token** for the random parcel.
- To open the mailbox, a player must present the correct token **in their hands**.
- If the player does not have a token in hand, the mailbox prompts for the intended recipient's token.
- An incorrect token does not unlock the mailbox.
- The mailbox and its flashing light are removed when the parcel is collected, deleted, or expires.
- Previous confirmed collection eligibility still applies: recipient or **current** members of their LBmaster's Advanced Groups party; all others are denied.

### Design proposals pending approval
- Bind each token to the parcel ID and intended recipient, and verify it server-side; prevent re-use and duplication.
- Require **both** a valid token and recipient/current-group membership to release the parcel, so a stolen token alone cannot grant access.
- Group members could physically borrow the recipient's token to collect; define whether token transfer is permitted and how the recipient receives the token.
- Prompt wording: 'This mailbox is locked. Present the recipient's delivery token in your hands.'
- Decide whether the token is consumed on successful collection and removed when the parcel expires.
- Decide token delivery/replacement behavior if the recipient is offline, has full inventory, loses the token, or dies.
