# Training log
Local-first PWA. Data lives in the phone's IndexedDB and syncs to a **private** GitHub repo as JSONL.

## Deploy
1. Public repo `workout-app`: push this folder's contents (not data-seed), enable Pages (Settings > Pages > main / root).
2. Private repo `workout-data`: copy `data-seed/` in (exercises.json + SCHEMA.md).
3. Fine-grained token: only `workout-data`, Contents read/write, set an expiry.
4. iPhone: open the Pages URL in **Safari** > Share > Add to Home Screen. Open the installed app, then Sync tab: paste repo + token.
