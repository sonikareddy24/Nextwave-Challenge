# Build Your First AI Project in 60 Minutes: Registration Website

A working prototype built for the NxtWave Growth Intern Challenge. The goal: get 500 final-year engineering students to register for a free workshop with ₹2,000 and 7 days.

**Live site:** https://claude.ai/artifact/55yB2oGaoCL7j3PYnB3JWJ
**File:** `ai-workshop-registration.html` (single self-contained file: HTML, CSS and JavaScript, no build step)

## Why this and not just a landing page

A landing page only collects signups. This site turns every signup into a distributor. Each student gets a personal referral link, ambassadors get their own tracking links, and the organizer dashboard shows which channel is working so effort can go where it pays off.

## Pages

| Page | Route | Purpose |
|---|---|---|
| Home | `#/` | Pitch, interactive 60-minute slider, live counter toward 500 |
| Workshop | `#/workshop` | Minute-by-minute agenda, who it's for, what students get |
| Register | `#/register` | Validated signup, then a personal referral link and WhatsApp share button |
| Leaderboard | `#/leaderboard` | Top referrers, drives the ₹200 reward competition |
| Showcase | `#/showcase` | Students submit projects and get an instant score out of 10 |
| Ambassadors | `#/ambassador` | Application form that generates a tracking link and a ready-to-forward WhatsApp message |
| FAQ | `#/faq` | Common student questions |
| Organizer | `#/admin` | Dashboard: registrations by source and college, ambassador and project counts, CSV view, demo data |

The Organizer page is not in the main nav. Open it from the footer link or add `#/admin` to the site address.

## How the features work

**Registration.** Checks name, a valid Indian mobile number (starts with 6 to 9, 10 digits), email, college, branch and year. Blocks duplicate phone numbers. On success, creates a code like `RAVI482` and a link like `…?src=referral&ref=RAVI482`.

**Referral tracking.** When someone opens a link with `?ref=CODE`, their registration is credited to that code. The leaderboard counts registrations per code.

**Source tracking.** The `src` parameter in a link (`wa`, `club`, `email`, `referral`, or none for direct) is stored with every registration, so the dashboard shows registrations per channel.

**Project scoring (Showcase).** A simple rubric out of 10: base points, description length, whether it calls an AI model, whether others can use it unaided, and a secure (https) link.

**Safety.** All user-entered text is escaped before it is displayed, and project links must be http or https.

## Using it during the campaign

1. Open `#/ambassador`, fill the form for each ambassador or club lead, and send them the generated message and link.
2. Share the main link in other channels with a source tag, for example `…?src=email` for the club emails.
3. Check `#/admin` daily to see which source is converting, then push harder on that channel.
4. At close, read the top referrers from `#/leaderboard` to pick the six ₹200 winners.

## Important limitation: data storage

This prototype saves data in the visitor's own browser (`localStorage`). That means:

- Data is **not shared** between devices or visitors, so the dashboard only shows what was entered in the same browser.
- Clearing browser data removes it.
- "Load demo data" on the Organizer page fills sample entries so the dashboard and leaderboard can be demonstrated.

**For production**, replace the `put()` and `get()` functions in the script with a call to a backend:

1. Create a Google Sheet (or Supabase table) with columns: name, phone, email, college, branch, year, code, ref, src, timestamp.
2. Create an n8n webhook that appends each submission to the sheet.
3. Post the form data to the webhook on submit, and read counts back for the live counter and leaderboard.
4. Add n8n WhatsApp reminders 24 hours and 1 hour before the workshop to reduce no-shows.

## Tech notes

- Plain HTML, CSS and JavaScript. No frameworks or dependencies besides Google Fonts (Bricolage Grotesque, Figtree, IBM Plex Mono).
- Page switching uses hash routes (`#/register`), so it behaves like a multi-page site from a single file.
- Responsive for phones and laptops, with automatic light and dark themes.
- To run locally, open `ai-workshop-registration.html` in any browser.
- To host elsewhere, upload the file to any static host (GitHub Pages, Netlify, Vercel).

## Ideas for the next 24 hours

- Connect to Google Sheets through n8n (shared data and automatic reminders).
- Replace the rubric on the Showcase page with AI-based project evaluation.
- Add a real certificate generator for attendees who submit a project.
- Test the invite message with a few real students and replace the assumed conversion rates with measured ones.
