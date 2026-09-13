# RFD_IT_Publishing — retired, moved into RFDGameStudio

> **This repository is no longer maintained.** On 2026-09-13 the itch.io
> publisher moved into [RFDGameStudio](https://github.com/rfd62794/RFDGameStudio)
> as the self-contained package **`packages/itch_publisher`** (Python import
> `itch_publisher`, command `itch-publisher`). This repo's full commit history
> was merged there. Please make changes in RFDGameStudio, not here.

## Portfolio notes

A small, focused tool (May – September 2026, 6 commits, 13 unit tests): a
Python CLI that publishes game builds to itch.io through butler, driven by a
per-game YAML config. Its design paid off at retirement — it had no dependency
on its callers, so it moved into RFDGameStudio with its full history as a
self-contained package that can still be split back out (see below).

Licensed under the MIT License (see `LICENSE`).

## Where things went

| In this repo | In RFDGameStudio |
|---|---|
| `publisher.py` | `packages/itch_publisher/src/itch_publisher/cli.py` |
| `targets/itchio.py` | `packages/itch_publisher/src/itch_publisher/itchio.py` |
| `report_cross_pipeline_versions.py` | `packages/itch_publisher/src/itch_publisher/report.py` |
| `tests/test_itchio.py` | `packages/itch_publisher/tests/test_itchio.py` |
| `config/games.yaml` | `publishing/games.yaml` (owned by the studio; key `voidrift` is now `voiddrift`) |
| Direct writes to `game-metadata.json` | `on_published` hook, implemented in `studio_mcp/publishing.py` |

## Publishing now

From an RFDGameStudio checkout (run `butler login` once):

```bash
uv run python scripts/publish.py shoal            # dry run: prints the butler command
uv run python scripts/publish.py shoal --execute  # real push
```

See `docs/PUBLISHING.md` in RFDGameStudio.

## Splitting it back out

The package keeps no dependency on the studio, so it can become its own
repository again with its history:

```bash
git subtree split --prefix=packages/itch_publisher -b itch-publisher-split
```
