# scverse × GSCN 2026

Landing page for the workshop **"Computational single-cell genomics for stem cell
biologists"**, Berlin, 7–8 September 2026.

**Live site:** https://scverse.org/gscn2026/
**Workshop materials (notebooks):** https://github.com/scverse/202609_workshop_GSCN

Built with [Hugo](https://gohugo.io) from the scverse
[event-template](https://github.com/scverse/event-template), stripped down to a single
page: hero → facts → schedule → before you arrive → instructors → contact.

## Editing

Almost everything is data or front matter — you rarely need to touch the templates.

| What | Where |
|---|---|
| Dates, venue, links, colours | `website/hugo.toml` |
| Intro text | `website/content/_index.md` |
| Setup instructions, data downloads | `website/content/setup.md` |
| Agenda | `website/data/schedule.yml` |
| Instructors | `website/data/organisers.yml` |

Clearing `data/schedule.yml` makes the schedule section show "Schedule TBA".
Clearing `data/organisers.yml` removes the instructors section.

## Local preview

Requires [Hugo extended](https://gohugo.io/installation/) ≥ 0.128.

```bash
hugo server -s website --buildFuture
```

## Deploy

Pushing to `main` builds the site and publishes it to the `gh-pages` branch via
`.github/workflows/gh-pages.yml`. GitHub Pages serves that branch at
`https://scverse.org/gscn2026/`.

## TODO before the workshop

- [ ] Create the `2026-09: Workshop GSCN` Zulip channel and set `zulipChannel` in `hugo.toml`
- [ ] Pin package versions in `content/setup.md` after a clean test install
