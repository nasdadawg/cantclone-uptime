# CANTCLONE availability monitor

Private Upptime-based uptime monitor for the CANTCLONE backend. Powered by
GitHub Actions — no server required.

## What it monitors

| Name | URL | Expected |
| --- | --- | --- |
| CANTCLONE Admin Login | `https://flow-ruby-two.vercel.app/admin/login` | HTTP 200 |

## How it runs

- The workflow (`.github/workflows/uptime.yml`) runs every **5 minutes**
  (`cron: "*/5 * * * *"`) and on manual `workflow_dispatch`.
- Each run checks the site via the `upptime/uptime-monitor` action and commits
  the result history to `history/` in this repo.

## Incident workflow (Upptime's normal behavior)

1. **Failure detected** — a check that does not return an expected status code
   (HTTP 200) marks the site **down**.
2. **Incident opened** — Upptime opens a GitHub **issue** in this repo for the
   affected site, titled with the site name and the failure.
3. **Repeat failures** — while the site stays down, subsequent checks **update
   the existing issue** (adding status changes) rather than opening duplicates.
4. **Recovery** — once a check succeeds again, Upptime **closes the issue**
   (auto-resolving the incident) and the site is marked **up** again.

No Production action is taken by this monitor: it only performs unauthenticated
GET requests against the public `/admin/login` page and records the outcome.

## Notes

- Monitoring + incident issues only (no status website). To add a public status
  page, add a `status-website:` block to `.upptimerc.yml` and the `site.yml`
  workflow, then enable GitHub Pages.
