# Drink Tracker

Personal alcohol tracker for Android, as an installable web app (PWA). It counts in
Belgian standard drinks (1 standaardglas / verre standard = 10 g pure alcohol). Data is
kept on the phone. When you choose, you can back it up to a private GitHub repository.

- **Log**: three tables of drink buttons. Each button shows that drink's standard drinks.
  Beer: 25, 33 and 50 cl at 4–10%. Wine: 12, 15 and 20 cl at 12%. Spirits: 2, 4 and 6 cl at
  20% or 40%. Tap one to add it now. **+** on a logged drink adds the same drink again.
  Use "Other drink" for anything else. Use ‹ › or tap the date to log on another day.
  You can undo from the toast, or remove a drink with ×.
- **Blood alcohol**: once your weight is set (Settings), a card shows the estimated level in
  g/L (‰) over time, with lines at 0,5 don't drive (Belgian limit), 0,8 drunk, 1,2 very
  drunk and 1,6 dangerous (blackout risk). It also shows when you'll be below 0,5 and back
  to 0. Logging a drink that will push you into a higher level triggers a warning, and the
  dangerous level opens a safety screen. The model is Widmark (r = 0,68 men, 0,55 women),
  with a 10 min absorption half-life and Michaelis-Menten elimination (~0,15 g/L/h around
  0,5). **It is only an estimate. Never use it to decide whether you can drive.**
- **Trends**: bar chart per day, week or month, with the weekly guideline, plus total,
  average per week, alcohol-free days and heaviest day.
- **Settings**: set the weekly limit (default 10), the hour a new day starts (default
  05:00, so a 01:30 drink counts for the night before), and your weight and sex. Back up
  to GitHub, or export and import a JSON file.

## Files

`index.html` is the whole app. `manifest.webmanifest`, `sw.js` and the icons make it
installable and let it work offline.

## Install on the phone

The app must be served over HTTPS, for example with GitHub Pages:

1. Push this folder to a GitHub repo, then turn on Settings → Pages (branch `main`, root).
2. On the phone, open `https://<user>.github.io/<repo>/` in Chrome.
3. Open the ⋮ menu, choose **Install app** (or **Add to home screen**), and confirm.

The app updates in the background. A new version shows up the next time it is opened.
If you change the list of files, bump `CACHE` in `sw.js`.

## Backup to GitHub

Drinks are only saved on the phone until you tap **Settings → Back up now**. That makes
one commit of `drinks.json` in a **private** GitHub repository. Nothing is sent
automatically. Settings shows when changes haven't been backed up yet. A backup first
merges in what's already in the repository. Restoring a new phone is simply connecting
it and backing up, and a drink removed on one phone is removed on the other at the next
backup.

One-time setup:

1. Create a **private** repository, for example `drink-data` (an empty one is fine).
2. Go to GitHub → Settings → Developer settings → Personal access tokens →
   **Fine-grained tokens** → Generate new token.
   - Repository access: **Only select repositories**, then pick `drink-data`.
   - Permissions → Repository permissions → **Contents: Read and write**.
   - Expiration: pick the longest you're comfortable with. When it expires, the app
     shows "Token rejected". Paste a new token to fix it.
3. In the app: Settings → Backup to GitHub. Enter `your-name/drink-data`, paste the
   token, and tap **Connect and back up**.

The token stays on the phone and can only touch that one repository. The app refuses to
connect to a public repository.

## Backup file

**Settings → Export** downloads a JSON file. **Import** merges a file back in and skips
duplicates. Anything not backed up lives only in the app on the phone: uninstalling it or
clearing Chrome's site data deletes it.
