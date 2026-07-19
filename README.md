# dp-update-digests

Walter's Diamond Protocol update tracker. A cloud Routine reads a curated list of sources every
**Monday and Friday at 07:00 CT** and writes a dated **digest** of where each one stands. No
notifications — you pull this repo when you want.

## Read it
Open [`digests/`](digests/) — the newest file is the latest batch. Each batch reports **every**
source's current state (changed *and* steady), so you always know where a source stands — not only
when it moves.

## Curate it
Edit [`sources.yml`](sources.yml) — add or remove sources, one entry each. `fetch: web` is the free
default; `fetch: firecrawl` is a per-source backup for gated pages only. Keep the env allowlist lean
(exact hosts, no wildcards).

## Why read-and-report, not change-monitors
A change-detector is blind to whatever is already true when it starts, and stays silent until an exact
future edit — it spends cost to tell you nothing and can't answer "what does this say *now*." This
digest reads each source and reports its current state every run. (Born from an inseglet Firecrawl
monitor that ran six days, billed daily, and surfaced nothing — because the Windows content it was
"watching for" was already in the README at baseline.)

## Layout
- `sources.yml` — the source registry (you edit)
- `digests/YYYY-MM-DD-<mon|fri>.md` — one file per run (the Routine writes; you read)
- `state.json` — last-seen state per source (machine-only; ignore it)
- `routine/sweep-prompt.md` — the read-and-report instruction the Routine follows
- `skill/dp-updates/SKILL.md` — the `/dp-updates` retrieval skill (last 3 batches, from anywhere)
- retention: repo history is permanent (the 60-day floor is met for free)

## Cost shape
Free fetch is the default, so credit burn scales with the **gated subset** (Firecrawl backup), not the
whole list — which matters at the 100+ sources this is built to grow into.
