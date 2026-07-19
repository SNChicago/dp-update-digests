---
name: dp-updates
description: >
  Show Walter the last 3 DP update-digest batches from the dp-update-digests repo. Trigger on
  "/dp-updates", "what's changed", "show me the update digest", "latest source updates", "any news
  on my tools/plugins". Reads the newest digests from GitHub and renders them verbatim — pull-only,
  no notifications. NOT for creating or editing the digest (that is the Mon/Fri Routine's job).
---

# dp-updates — pull the last 3 update digests

When invoked, fetch and render the three newest digest batches from the `dp-update-digests` repo.

1. List `digests/` in `SNChicago/dp-update-digests`
   (GitHub API `https://api.github.com/repos/SNChicago/dp-update-digests/contents/digests`, or `gh`).
   Filenames are `YYYY-MM-DD-<mon|fri>.md`; sort descending; take the top 3.
2. Fetch each raw
   (`https://raw.githubusercontent.com/SNChicago/dp-update-digests/main/digests/<file>`).
3. Render them newest-first, exactly as written. Lead with one line: "Last 3 digests: <dates>".
   Do NOT summarize away the per-source state lines — Walter wants the full state, STEADY sources
   included (that's the design).
4. If the ask is specifically "what changed", surface only the 🔺 CHANGED entries across the three;
   otherwise show everything.

Notes
- GH owner is `SNChicago` (filled at repo creation, 2026-07-19).
- Works from web, Cowork, or Code — it only reads public GitHub over HTTPS, no connectors required.
- If the repo is private, use `gh` (authenticated) instead of the raw URL.
