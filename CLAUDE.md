# The Rollin' Rust — working notes for Claude

## Tracking rules (from the owner)

- **Every Meta event must be sent from both the browser and the server**, with one shared `event_id` so Meta deduplicates them. Never build a browser-only or server-only event.
- Never count one shopper action twice. When two paths could fire the same event, prove they can't overlap, or give them the same `event_id`.
- Build changes unpublished, export the GTM workspace, and review it before publishing.
- Keep all tracking in Stape + GTM. Don't add events through Meta's "Add events" tool or Shopify's Meta channel data sharing (it's off on purpose).

## Setup

- Shopify store: therollinrust.com
- Meta dataset/pixel: "The Rollin' Rust" (604708470177185). Ignore the old "The Rollin' Rust - Store" pixel.
- Web GTM: GTM-WPLM7JHB. Server GTM: GTM-NR7CDFQN (Stape, custom domain wwpiwhdy.therollinrust.com).
- Ticket sales from ticketweb.com send browser-only Purchase and InitiateCheckout to the same pixel. That's expected, not a bug.
