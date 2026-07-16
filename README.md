# UTM Link Builder

A tiny, zero-dependency tool for building UTM-tagged campaign links for
**plrd.org** (and beyond). Drop a link, pick your channels, copy the tagged URLs.

**▶ Live tool:** https://lksbrssr.github.io/utm-link-builder/

## What it does
- Paste a page URL → auto-derives the campaign from the URL slug.
- Toggle channels (X/Twitter, LinkedIn, Bluesky, Mastodon, Farcaster, Reddit, HN, Newsletter).
- Instantly generates every tagged URL with per-link **Copy**, **Copy all**, and **Download CSV** (for a campaign log).
- Built-in **"What is a UTM?"** explainer (including what `medium` means).

## What is a UTM link? (short version)
A UTM link is a normal URL with tags on the end that tell Google Analytics
**where a visitor came from**. Nothing is registered anywhere — GA reads the tags
when someone clicks through.

```
https://www.plrd.org/insights/post/?utm_source=twitter&utm_medium=social&utm_campaign=post
```

| Tag | Answers | Examples |
|---|---|---|
| `utm_source` | **Where** it's posted (the exact place) | `twitter`, `linkedin`, `newsletter` |
| `utm_medium` | **What type** of channel that is (the bucket) | `social`, `email`, `referral` |
| `utm_campaign` | **Which** post/push this is | `human-connectome` |
| `utm_content` | *(optional)* which **version** of the link | `thread-1`, `bio-link` |

**source vs medium:** Twitter, LinkedIn and Bluesky are different *sources* but the
same *medium* = `social`. GA4 groups traffic into channels **based on the medium**,
so keep it to `social` / `email` / `referral` or the traffic lands in "Unassigned".

## Rules
- Lowercase, hyphens, no spaces.
- Reuse the **same** `utm_campaign` across all channels for one post.
- Only tag **external** links pointing to the site — never internal page-to-page links.

## Run it locally
It's a single `index.html` — just open it in a browser. No build, no install.

## Configure channels
Edit the `CHANNELS` array near the top of the `<script>` in `index.html` to add or
change source/medium mappings.
