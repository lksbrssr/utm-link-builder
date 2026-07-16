# UTM Link Builder

A tiny, zero-dependency tool for building UTM-tagged campaign links for **any
Protocol Labs site**. Drop a link, pick your channels, copy the tagged URLs — and
grab a QR code for each.

**▶ Live tool:** https://lksbrssr.github.io/utm-link-builder/

## What it does
- Paste a page URL on **any PL domain** → auto-derives the campaign from the URL slug.
- Quick-pick buttons for common PL domains (plrd.org, protocol.ai, plcapital.xyz, plneuro.xyz, filecoin.io, ipfs.tech, libp2p.io).
- Toggle channels: X/Twitter, LinkedIn, **Telegram**, Bluesky, Mastodon, Farcaster, Reddit, HN, Newsletter.
- Instantly generates every tagged URL with per-link **Copy**, **QR code** (download PNG), **Copy all**, and **Download CSV** (for a campaign log).
- Built-in **"What is a UTM?"** explainer (including what `medium` means, and how to tag a blog *series*).

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
medium**, so keep it to `social` / `email` / `referral` or traffic lands in
"Unassigned".

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
Edit the `DOMAINS` and `CHANNELS` arrays near the top of the `<script>` in
`index.html` to change the quick-pick domains or channel/source/medium mappings.

## Credits
QR generation via [qrcode-generator](https://github.com/kazuhikoarase/qrcode-generator) (MIT), bundled locally.
