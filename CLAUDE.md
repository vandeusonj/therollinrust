# The Rollin' Rust — working notes for Claude

## Tracking rules (from the owner)

- **Every Meta event must be sent from both the browser and the server**, with one shared `event_id` so Meta deduplicates them. Never build a browser-only or server-only event.
- Never count one shopper action twice. When two paths could fire the same event, prove they can't overlap, or give them the same `event_id`.
- Build changes unpublished, export the GTM workspace, and review it before publishing.
- Keep all tracking in Stape + GTM. Don't add events through Meta's "Add events" tool or Shopify's Meta channel data sharing (it's off on purpose).

## Setup

- Shopify store: therollinrust.com
- Two Meta pixels, kept strictly separate:
  - **Merch:** "The Rollin' Rust" (604708470177185). Only merch shopping on therollinrust.com. All hoodie/merch campaigns optimize on this one.
  - **Tickets:** "The Rollin' Rust - Tickets" (1401516072094248). Renamed from "The Rollin' Rust - Store" on 2026-10-08. Only ticket activity: ticketing sites (Ticketweb, venue platforms like ThunderTix) and the Tour page "Tickets"/RSVP clicks. Never put it on the store or checkout.
- Web GTM: GTM-WPLM7JHB. Server GTM: GTM-NR7CDFQN (Stape, custom domain wwpiwhdy.therollinrust.com).
- Ticketing sites can only send browser events (we don't control them). That's the one accepted exception to the browser + server rule. Tracking we build ourselves for tickets (Tour page clicks) still goes browser + server through Stape.
- Give venues the **ticket** pixel ID, never the merch one. Account-wide on the venue's platform is OK (owner decision 2026-10-08), with these conditions:
  - Isolate our show with a custom conversion. Build it only after checking what the venue's real Purchase events contain (URL, content IDs/names). Don't assume the confirmation URL carries the event ID.
  - Ticket campaigns optimize on that custom conversion, never on plain Purchase.
  - Audiences built from the ticket pixel use the same filter, unless the goal is deliberately "local ticket buyers at this venue".
- The current Ticketweb show (Oct 17) stays on the merch pixel; the owner decided not to switch it this close to the date. Every show from here on uses the ticket pixel.

## Ad economics (confirmed by owner 2026-10-08)

- Hoodies sell at $55; free shipping on hoodie orders; shipping label ≈ $6; payment fees ≈ 2.9% + $0.30.
- Full product cost: tie-dye hoodie $22.05; solid hoodies $13.05.
- Break-even cost per purchase: tie-dye ≈ $25 full price / ≈ $20 with the 10%-off code; solid hoodies ≈ $34 / ≈ $29.
- Budget rule for the hoodie CBO: 4-day cost per purchase under $22 → raise budget 20%; $22–28 → hold and add creative; over $28 → no raise, new creative first.
