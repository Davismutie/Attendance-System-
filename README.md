# TROD Log

A lightweight staff attendance web app for workplaces — workers clock in/out themselves, and administrators manage staff and review records. Built as a single self-contained HTML file: no backend, no build step, no dependencies to install.

![Status](https://img.shields.io/badge/status-active-3fa796) ![Type](https://img.shields.io/badge/type-single--file%20web%20app-e8a93b)

## Features

**Worker portal**
- Sign in with a Staff ID + PIN
- One-tap Clock In / Clock Out with a punch-card style receipt
- Automatic "Late" status if clocking in after 09:15
- Personal attendance history (last 12 punches)

**Administrator dashboard**
- Separate admin login (username + password)
- Live "Present / Absent / Late / On Leave" counts for today
- Today's log of everyone who has punched in
- Workforce directory — add, edit, deactivate, or remove staff; assign departments and PINs
- Full attendance records — searchable, filterable by status, manual entry/edit, CSV export
- Change admin password from the dashboard

## Demo credentials

| Role  | Login |
|-------|-------|
| Admin | `admin` / `admin123` |
| Worker | Staff ID `STF001`, PIN `1234` (seeded sample worker) |

Change the admin password after first login, and update or remove the sample workers from the **Workers** tab.

## Getting started

No installation needed — it's a single HTML file.

1. Download `TROD log.html` from this repo.
2. Open it directly in a browser, **or** deploy it as a static site (GitHub Pages, Netlify, Vercel, or any static host).
3. Sign in as admin to add your real staff list, then share the page link with your team.

### Deploying to GitHub Pages

1. Push `TROD log.html` to your repo (rename to `index.html` if you want it served at the root).
2. In the repo settings, enable **Pages** and point it at the branch/folder containing the file.
3. Visit the published URL — workers and admins can both use the same link.

## How data is stored

TROD Log saves everything in the browser's `localStorage` — there is no server or database. This means:

- Data is **per device / per browser**. A worker punching in on their own phone stores that record on their phone, not on a shared server.
- Clearing browser data/cache will erase the stored records.
- It's well suited for a single shared kiosk device (e.g. a tablet at the entrance where everyone clocks in) or for quick internal testing — not for a live team spread across many personal devices needing one shared record.

If you need everyone's punches to sync to one shared source of truth, that requires adding a small backend (e.g. Firebase, Supabase, or a simple REST API) in place of the `localStorage` calls — happy to help build that as a next step.

## Project structure

```
TROD log.html   → everything: markup, styles, and app logic in one file
```

## Customization

- **Departments**: edit the `<select id="mw-dept">` options in the HTML, or just use "Custom…" when adding a worker.
- **Late cutoff time**: change the `'09:15'` check inside the `workerClockIn()` function in the `<script>` section.
- **Colors/branding**: all design tokens are CSS custom properties at the top of the `<style>` block (`--accent`, `--present`, `--absent`, etc.).

## Security note

PINs and passwords are stored in plain text in browser `localStorage`. This is fine for a small internal tool but is **not** suitable for handling sensitive credentials at scale. Don't reuse important passwords as admin credentials here.

## License

Add a license of your choice (e.g. MIT) before publishing publicly.
