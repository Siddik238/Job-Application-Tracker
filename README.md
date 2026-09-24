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

## Sourcing jobs to import

This dashboard doesn't scrape job boards itself — that's deliberate. Finding jobs and importing what you've applied to are two separate steps.

**Finding jobs:** matching postings are sourced with [Apify](https://apify.com)'s [`curious_coder/linkedin-jobs-scraper`](https://apify.com/curious_coder/linkedin-jobs-scraper) actor (scrapes LinkedIn's public jobs search, no login/cookies required), then scored against a resume by an AI assistant. A two-step prompt works best — one step to fetch raw postings, a separate step to judge fit — since a scraper has no way to know what's actually a good match:

```
Step 1 — Search: Use the Apify actor curious_coder/linkedin-jobs-scraper with
keywords "<role title>", location "<location>", datePosted "past24Hours",
limitPerSource 50. Return the raw results.

Step 2 — Match: My resume is attached. For each job returned, compare its
description against my resume and score it 0–100 on actual overlap: required
tools/skills present in my resume, years of experience required vs. what I
have, and any hard requirements (citizenship, clearance, on-site only) I
clearly don't meet. Drop anything under 60(Upto you). Output the rest as a table with
columns: Company, Role, Source, Link, Notes — where Notes contains the match
score, a one-line reason, the location, and the posted date.
```

**Importing them:** trim that table down to the jobs you actually applied to, then save as `.xlsx`/`.csv` with exactly these headers so the bulk import auto-maps every column:

`Company | Role | Source | Link | Notes`

Leave **Status** and **Date applied** out of the sheet — the import dialog has its own "default status" and "default date" fields that apply to the whole batch (default status: Applied, default date: today), which is more accurate than baking a status into the sheet before you've actually applied.

## Deploying your own copy

1. Fork or clone this repo
2. In the repo settings on GitHub, go to **Pages** → set the source branch to `main` (root)
3. GitHub will publish it at `https://YOUR_NAME.github.io/Job-Application-Tracker/` within a minute or two

## Data & privacy

All data lives in `localStorage` in your own browser. It is never sent to a server, and it does not sync across browsers or devices — clearing your browser data will clear the tracker too. Use the CSV export regularly if you want a backup.

## License

MIT — see [LICENSE](LICENSE).
