# UTM Link Builder

A tiny, zero-dependency tool for building UTM-tagged campaign links for **any
Protocol Labs site**. Drop a link, pick your channels, copy the tagged URLs — and
grab a QR code for each.

**▶ Live tool:** https://lksbrssr.github.io/utm-link-builder/

## What it does
- **Guided 5-step flow** with a **sticky** GA-style progress stepper (Paste URL → Campaign → Channels → Get links → See results). Completed input steps **collapse to a summary** and re-expand on click.
- **Inline tooltips** (hover / tap the ⓘ) explain every field — what `medium` is, how to tag a series, etc. — instead of a separate wall of text.
- Paste a page URL on **any PL domain** → auto-derives the campaign from the URL slug.
- Quick-pick buttons for common PL domains (plrd.org, protocol.ai, plcapital.xyz, plneuro.xyz, filecoin.io, ipfs.tech, libp2p.io).
- Toggle channels: X/Twitter, LinkedIn, **Telegram**, Bluesky, Mastodon, Farcaster, Reddit, HN, Newsletter, **Presentation / Slides** (for QR codes on decks/print — `medium=offline`).
- **Custom "Other" channel:** type any source (e.g. `discord`, `whatsapp`, a partner domain) and pick its medium on the fly.
- Generates every tagged URL (shown **abbreviated** to stay tidy) with per-link **Copy** and **QR code** (Download **or** Copy PNG). **Copy all** prefixes each line with its channel; **Download CSV** for the campaign log.
- **Newsletter Include button** on the newsletter row: copies a short note + the newsletter-tagged link and opens a Telegram chat with the newsletter manager (`@emilymvaughan`, configurable) to paste & send.
- **Step 5 — see results:** an **Open Traffic acquisition** button deep-links straight into the GA4 report (PL R&D property) + instructions (Session campaign; Realtime for an instant pulse).

## What is a UTM link? (short version)
A UTM link is a normal URL with tags on the end that tell Google Analytics
**where a visitor came from**. Nothing is registered anywhere — GA reads the tags
when someone clicks through. Works on any domain that has an analytics tag.

```
https://www.plrd.org/insights/post/?utm_source=twitter&utm_medium=social&utm_campaign=post
```

| Tag | Answers | Examples |
|---|---|---|
| `utm_source` | **Where** it's posted (the exact place) | `twitter`, `linkedin`, `telegram`, `newsletter` |
| `utm_medium` | **What type** of channel that is (the bucket) | `social`, `email`, `referral` |
| `utm_campaign` | **Which** post/push/series this is | `human-connectome` |
| `utm_content` | *(optional)* which **version/part** of the link | `part-1`, `thread-1`, `bio-link` |

**source vs medium:** Twitter, LinkedIn, Telegram and Bluesky are different *sources*
but the same *medium* = `social`. GA4 groups traffic into channels **based on the
medium**, so keep it to `social` / `email` / `referral` / `offline` or traffic lands in
"Unassigned".

**QR on slides/print:** use medium `offline` (source `presentation`). GA4 has no
default offline channel, so it shows under Unassigned — find it via the
**Session source / medium** dimension (`presentation / offline`).

**Blog series:** put the **series** in `utm_campaign` (e.g. `connectome-series`) and
the **part** in `utm_content` (`part-1`, `part-2`) so all parts group together but
stay distinguishable.

## Rules
- Lowercase, hyphens, no spaces.
- Reuse the **same** `utm_campaign` across all channels for one post/series.
- Only tag **external** links pointing to the site — never internal page-to-page links.

## Run it locally
Two files — `index.html` and `qrcode.js` (bundled, offline QR generation). Just open
`index.html` in a browser. No build, no install, no external calls.

## Configure
Edit these near the top of the `<script>` in `index.html`:
- `DOMAINS` — quick-pick domain buttons.
- `CHANNELS` — channel list + source/medium mappings.
- `NEWSLETTER_HANDLE` — the Telegram handle the "Hand off to the newsletter" button opens (default `emilymvaughan`).

> Note: the newsletter button copies the message and opens the chat — the person
> pastes & sends. True auto-send would need a Telegram bot backend (possible once
> deployed with a server, not on static hosting).

## Credits
QR generation via [qrcode-generator](https://github.com/kazuhikoarase/qrcode-generator) (MIT), bundled locally.
