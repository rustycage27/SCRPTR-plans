# SCRPTR Reading Plans

Curated reading plans for the [SCRPTR](https://github.com/rustycage27/SCRPTR) iOS Bible study app. Each plan is a JSON file following the schema validated by `scripts/generate_plan.py` in the main repo.

## Structure

```
plans-manifest.json     # Index — lists all available plans with metadata and URLs
plans/
└── {plan-id}.json      # Individual plan files, one per plan
```

The SCRPTR app polls `plans-manifest.json` in the background (at most once every 24 hours) and downloads any new or updated plans it finds. Plan IDs are stable; bump `file_version` to push an update for an existing plan.

## Adding a plan

1. Generate the plan JSON with `scripts/generate_plan.py` in the main repo. Use `--base-url https://raw.githubusercontent.com/rustycage27/SCRPTR-plans/main/plans` so the manifest stub's `url` field points at this repo.
2. Drop the generated JSON into `plans/` and append/update the stub in `plans-manifest.json`.
3. Commit and push to `main`. The raw GitHub CDN picks it up within ~5 minutes.

## Schema

See `Scrptr/Models/ReadingPlan.swift` in the main repo for the authoritative Codable definitions. High level:

- Each plan has `id`, `title`, `description`, `category`, `duration_days`, `tags`, `thumbnail_color`, and a `days` array.
- Each day has a `day` number, `title`, and one or more `readings` (book_id, chapter/verse range).
- Book IDs follow standard canonical order: Genesis = 1 through Revelation = 66.

## License

The plan JSON files in this repo are public domain. You may fork, modify, or generate your own.
