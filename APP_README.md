# Nimply for Make

[Nimply](https://nimply.io) is an all-in-one social media management platform — publishing, planning, approvals, and analytics for **Facebook, Instagram, X (Twitter), LinkedIn, TikTok, YouTube, Pinterest, Threads, and Google Business Profile**.

This app connects your Make scenarios to your Nimply workspace: fill your posting queue automatically, and react the moment posts go live or fail.

## Getting started

1. Add any Nimply module to a scenario and click **Create a connection**.
2. Log in to Nimply, choose the **workspace** the connection may use, review the permissions, and click **Allow access**.
3. That's it — no API keys to copy. Access is scoped to that one workspace and can be revoked at any time from Nimply.

> You need the **Owner** or **Admin** role in the Nimply workspace to authorize the connection. API access is included on every Nimply plan.

## Modules

### Triggers

| Module | Fires when |
| --- | --- |
| **Watch Events** (instant) | A post is **published** or **fails**, a draft is **sent for approval**, **approved**, or **rejected**, or a channel **disconnects** — delivered by webhook the moment it happens, no polling. |

### Actions

| Module | What it does |
| --- | --- |
| **Create a Post** | Creates a post on one or more channels — as a draft, into each channel's next free posting slot, published immediately, or scheduled at a specific time. Attach media via the upload modules. |
| **Create a YouTube Video** | Uploads a video or Short to a YouTube channel with full video options: category, visibility, license, subscriber notification, embedding, and made-for-kids. |
| **Create a TikTok Post** | Posts a video or photos to TikTok with privacy level (loaded from the account), comment/Duet/Stitch settings, and commercial-content disclosure. |
| **Create a Pinterest Pin** | Creates a pin on a specific board (picked from a dropdown) with a destination link and alt text. |
| **Create a LinkedIn Post** | Posts to a LinkedIn profile or company page with visibility control (public or connections only). |
| **Update a Post** | Edits the content and/or title of a draft or scheduled post. |
| **Schedule a Post** | Sets or changes when a draft or scheduled post will publish. |
| **Unschedule a Post** | Moves a scheduled post back to draft and clears its publish time — it won't publish until scheduled again. |
| **Upload Media from URL** | Imports a file from a public URL into your media library; returns a media ID for posts. |
| **Upload Media (Binary)** | Uploads file data from a previous module (downloads, form uploads, generated files). |
| **Add Link Block** | Adds a link button, text, product, coupon, countdown, FAQ or testimonial block to your nimply.link page (your link in bio). |
| **Publish Link Page** | Publishes the page so the new blocks are live at nimply.link within about a minute. |

### Searches

| Module | What it does |
| --- | --- |
| **List Channels** | Returns your connected social channels — useful for routers and filters. |
| **List Link Pages** | Returns your nimply.link pages with status and public URL. |

## Scenario ideas

- **Content calendar → queue**: Airtable / Google Sheets rows become scheduled posts with media, each at its row's publish date.
- **Never miss a failure**: *Watch Events (post failed)* → Slack message with the error — fix it before the client notices.
- **RSS autoposting**: new feed item → *Create a Post* into the next free slot on every channel.
- **Client approvals**: *Watch Events (approval requested)* → email the client; their reply approves the post via Nimply.
- **Reporting**: *Watch Events (post published)* → log the post and its URL to a spreadsheet.
- **Latest video on your link page**: YouTube *Watch Videos* → *Add Link Block* (featured) → *Publish Link Page*.

## Notes

- **Scheduling values** in *Create a Post*: `draft`, `next_slot`, `now`, or an ISO 8601 datetime such as `2026-08-01T09:00:00Z`. Anything except `draft` publishes real content — test with drafts first.
- Publishing is asynchronous: a "publish now" post returns as `SCHEDULED` and goes live within moments; *Watch Events* tells you when it's `PUBLISHED` or `FAILED`.
- Multiple media on a post become a **carousel**; use content type `REEL`, `STORY`, or `VIDEO` for those formats.

## Resources

- 📘 [Developer documentation](https://developer.nimply.io) — full API reference and guides
- 🔗 [Make integration guide](https://developer.nimply.io/docs/integrations/make)
- 💬 [Contact support](https://nimply.io/contact)
