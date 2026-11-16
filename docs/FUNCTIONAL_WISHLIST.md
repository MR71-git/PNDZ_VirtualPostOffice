# Functional Wishlist — PNDZ Virtual Post Office

**Version:** 0.2 (design only)  
**Status:** Requested additions; details and acceptance criteria to be finalized.  
**No scripts, configuration files or game assets are authorized by this document.**

## Requested features (10)

| ID | Feature | Functional intent | Open design questions |
| --- | --- | --- | --- |
| FW-01 | Parcel tracking | Allow sender and recipient to see parcel status and relevant timestamps (e.g. sent, available, collected, expired). | Which statuses are visible to whom? Is there a unique tracking number? |
| FW-02 | Nearest pickup point | Determine a suitable pickup location based on the recipient's position or another defined reference point. | Use last known position or current location? What happens if no point is available? |
| FW-03 | Loot categories | Group random delivery rewards into configurable tiers (e.g. Common, Rare, Epic, Legendary). | Tier names, eligibility and balance? |
| FW-04 | Personal cooldown | Limit how frequently an individual player can receive a random delivery. | Cooldown duration, persistence, moderator override? |
| FW-05 | Weighted loot tables | Configure item and category selection probabilities for random packages. | Weights per item, tier, map, event or player? |
| FW-06 | Audit log | Record sending, receipt, collection, expiration, admin modifications, and relevant errors. | Retention, access, privacy and log rotation? |
| FW-07 | Item blacklist | Block specified item classnames or item categories from being sent or generated. | Attachments and nested contents? Admin exceptions? |
| FW-08 | Offline mail | Permit parcels to be sent to recipients who are offline and retained for later collection. | How are recipients identified and selected? |
| FW-09 | Sending limits | Limit number, size, or frequency of parcels sent by a player. | Limits per day, recipient, role, or mailbox? |
| FW-10 | Webhooks | Optional external event notifications, such as Discord-compatible webhooks. | Which events, filtering, security, retry and rate limiting? |

## Cross-cutting design rules
- All player data and permission-sensitive operations should be server authoritative.
- Parcel expiration remains **7 real-world days** from inbox availability unless the owner changes that requirement.
- Prevent duplicate collections and preserve parcel integrity across restarts.
- Keep player-facing notifications and documentation in English first; localization remains a design proposal.
- The PNDZ naming and configuration conventions remain unchanged.
- No selected extension is considered implemented or technically validated.

## Prioritization proposal (not approved)
- **Foundational:** FW-06 Audit log, FW-07 Item blacklist, FW-08 Offline mail, FW-09 Sending limits.
- **Delivery experience:** FW-01 Parcel tracking, FW-02 Nearest pickup point.
- **Random rewards:** FW-03 Loot categories, FW-04 Personal cooldown, FW-05 Weighted loot tables.
- **Integrations:** FW-10 Webhooks.

## Next design decisions
1. Define the tracking lifecycle and data visible to senders/recipients.
2. Decide which player location is used for nearest pickup point.
3. Specify reward tier definitions and weighted loot rules.
4. Set cooldown and sending-limit policies.
5. Define offline recipient identification.
6. Decide audit retention and webhook event payload/privacy requirements.
