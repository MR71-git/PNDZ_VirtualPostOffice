# PNDZ Missed Package — Standalone Project

**Status:** Design only. No scripts.

## Purpose
Server-triggered surprise parcel events with a limited collection window. This mod does not depend on PNDZ Post Office.

## Confirmed rules
- Server selects a random suitable location in a city or town, avoiding water, toxic zones and unsuitable terrain.
- A physical mailbox/postbox on a stand appears at the location with a flashing indicator light; everyone can see it.
- Selected recipient receives a personalized physical token for that specific parcel.
- The recipient or a **current member of their LBmaster's Advanced Groups party** can collect only while **physically holding the recipient's correct token in hand**.
- Current group membership is checked server-side at pickup. A new member gains eligibility; a departed member loses eligibility. All unrelated players are denied, even if they hold the token.
- Without the token in hand, the mailbox prompts the player to present the recipient's token.
- The six-real-world-hour deadline begins with the first notification and must not reset after restarts or repeat notifications.
- The mailbox and flashing light are removed upon successful collection, deletion or expiry.
- Collection is single-use and must not duplicate rewards.

## Excluded
- General player-to-player parcel sending, private postal inboxes, seven-day retention, and ordinary postal pickup points. These belong exclusively to **PNDZ Post Office**.

## Conventions
- Classnames begin with `PNDZ_`; author `PNDZ`.
- Proposed settings: `$profile:PNDZ/MissedPackage/`.
- If a types XML is required: nominal 0, min 0, lifetime 7200.

## Open decisions
- Token issuance, loss/replacement and cleanup.
- Exact mailbox model, lamp behavior and supported Advanced Groups integration interface.
- Recipient notification/location marker policy and safe-location selection thresholds.
