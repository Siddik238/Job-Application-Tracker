# Application Pipeline — Job Application Tracker

A single-page dashboard for tracking job applications: status, dates, sources, follow-ups, and notes — all in one place, with a bulk import from Excel/CSV.

**Live demo:** https://siddik238.github.io/Job-Application-Tracker/

## Features

- **Pipeline overview** — total applications, active count, offers, ghosted, response rate, and applications this week, at a glance
- **Status tracking** — Applied, Interview, Offer, Rejected, Withdrawn, and an auto-detected **Ghosted** status (any application left untouched for 30+ days)
- **Auto-computed follow-ups** — a follow-up date is set automatically 3 days after the applied date, and flagged in the table when it's due
- **Bulk import** — upload an Excel/CSV export from your own job-search tracking and map columns to fields, with a live preview and duplicate detection before committing
- **CSV export** — download your full pipeline at any time
- **Notes per application** — click a company name to see notes for that application without leaving the table
- **Light/dark mode** — follows your system theme
- **No backend, no account** — everything runs client-side and is stored in your browser's `localStorage`. Nothing is uploaded anywhere.

## Tech stack

Vanilla HTML, CSS, and JavaScript — no framework, no build step. Excel/CSV parsing via [SheetJS](https://sheetjs.com/).

## Running it locally

This is a single static file, so any of these work:

- Open `index.html` directly in a browser, or
- Serve it locally:

  ```bash
  python3 -m http.server 8000
  ```

  then visit `http://localhost:8000/`

## Deploying your own copy

1. Fork or clone this repo
2. In the repo settings on GitHub, go to **Pages** → set the source branch to `main` (root)
3. GitHub will publish it at `https://YOUR-USERNAME.github.io/Job-Application-Tracker/` within a minute or two

## Data & privacy

All data lives in `localStorage` in your own browser. It is never sent to a server, and it does not sync across browsers or devices — clearing your browser data will clear the tracker too. Use the CSV export regularly if you want a backup.

## License

MIT — see [LICENSE](LICENSE).
