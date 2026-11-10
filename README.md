# Training log
Local-first PWA for quick logging on a phone. Data lives in the phone's IndexedDB, works offline,
and syncs to a **private** GitHub repo as append-only JSONL (see SCHEMA.md).

## Repos
- `HealthApp` (public): this folder. GitHub Pages serves it (Settings > Pages > main / root).
- `HealthData` (private): the app writes `data/*.jsonl` there. Only the `.jsonl` files and `exercises.json` belong in it.

## Setup on iPhone
1. Fine-grained token: only the HealthData repo, Contents read/write, set an expiry.
2. Open the Pages URL in **Safari** > Share > Add to Home Screen.
3. Open the installed app > Sync tab: enter `owner/HealthData` (a full GitHub URL also works) + token > Save & sync.

## Using it
- The date chip (top right) back-dates entries for every tab; it turns orange when not on today.
- Every save shows an Undo toast; every list row has a delete button.
- Lift: −/+ steppers, sets in progress survive app restarts, switching exercise auto-saves the current sets.
- Stretch: Morning / Night done toggles per day, 7-day grid (tap a dot to fix a past day), weekly count vs a 5/7 target, streaks. Routines are listed under each toggle.
- Trends > Insights: weight rate per week, estimated maintenance calories, protein per lb, most-improved lift, adherence.
- Tabs show a dot once something is logged today.
- The status chip (top left) shows unsynced count or sync errors; tap it for Sync & settings.
- After deploying a new version, the phone picks it up on the second launch (offline cache).
