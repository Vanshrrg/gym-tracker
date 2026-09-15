# Gym Tracker

A single-file, mobile-first gym tracking web app. No frameworks, no backend — just `index.html`, with optional GitHub Gist sync for backup/cross-device access.

## Features

- Log workouts by date, exercise, weight, sets/reps, and notes
- Auto-infers your split (push/pull/legs/upper/lower) from session history, with manual override
- Warm-up suggestions per exercise (50% × 10, 70% × 5 of working weight)
- Progressive overload suggestions based on your last session for that exercise
- Detects undertrained muscle groups for the current session type and suggests exercises
- Bodyweight auto-added to load for bodyweight exercises (pull-ups, dips, push-ups)
- "Export for AI" button — copies a ready-to-paste coaching prompt (with last 4 sessions + today) for Claude/ChatGPT
- Dark mode, large tap targets, works fully offline (data stored in `localStorage`)

## Running it

Just open `index.html` in a browser, or deploy it as a static site (e.g. GitHub Pages).

## Deploying to GitHub Pages

```bash
git init
git add index.html README.md
git commit -m "Initial gym tracker"
gh repo create gym-tracker --public --source=. --push
gh api repos/:owner/gym-tracker/pages -X POST -f "source[branch]=main" -f "source[path]=/"
```

Or manually: create a repo named `gym-tracker` on GitHub, push `main`, then enable Pages in **Settings → Pages** with source set to the `main` branch, root folder.

Your app will be live at `https://<your-username>.github.io/gym-tracker/`.

## Setting up GitHub Gist sync (optional)

Gist sync lets you back up your workout data and access it from multiple devices. Without it, data just stays in your browser's local storage.

1. **Create a Personal Access Token (PAT):**
   - Go to [github.com/settings/tokens](https://github.com/settings/tokens) → *Generate new token (classic)*
   - Give it a name like "gym-tracker"
   - Select only the **`gist`** scope
   - Generate and copy the token (you won't see it again)

2. **In the app:** open **Settings → GitHub Gist Sync**, paste the token, leave Gist ID blank, and hit **Save & Sync**. This creates a new private Gist called `gym-tracker.json` and fills in the Gist ID automatically.

3. **On another device:** enter the same token and the Gist ID shown in Settings, then hit **Pull from Gist** to load your data.

Your token is stored only in your browser's `localStorage` — it's never sent anywhere except directly to the GitHub API.

## Data model

All data lives in `localStorage` under the key `gymTrackerData_v1`, and mirrors to a Gist file `gym-tracker.json` when sync is configured. Wipe local data any time from **Settings → Danger Zone**.
