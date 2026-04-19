# Daily Scorecard — Claude Guidelines

## Project
- Single-file app: `index.html`
- Firebase project: `daily-scorecard-62031` (Firestore, not Realtime DB)
- Auth: Google sign-in via Firebase Auth
- GitHub repo: `cphelps85/daily-scorecard`
- Live site: GitHub Pages, deploys from `main` branch

## Dev Mode
- `IS_DEV = window.location.protocol === 'file:'`
- Dev uses `dev_users` Firestore collection prefix instead of `users`
- Orange DEV MODE banner shown when running locally
- Always test locally before pushing

## Data Structure
Firestore path: `users/{uid}/checkins/{YYYY-MM-DD}`
- mood: 0-4 (index into MOODS emoji array)
- dayPlanned: bool
- caffeine: number (limit is 1)
- meals: { Breakfast, Lunch, Dinner } each { rating: 'good'|'okay'|'struggled', trigger: string|null }
- snacks: [{ rating, trigger }]
- ran: bool
- otherMove: bool
- weighed: bool
- weightDir: 'up'|'down'|'same'|null
- homeOrg: bool
- submitted: bool
- pct, filled, total: computed on save

Settings path: `users/{uid}/settings/prefs`
- runDays: number[] (day-of-week, 0=Sun)

## Key Constants
- SOBRIETY_START: 2025-11-05 — do not change
- DEFAULT_RUN_DAYS: [3, 5, 0] (Wed, Fri, Sun)
- Caffeine limit: 1 per day

## Verification
- After any schema changes, verify Firestore reads/writes work in dev mode before pushing
