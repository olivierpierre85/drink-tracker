# Drink Tracker

Personal alcohol tracker for Android, as an installable web app (PWA). It counts in
Belgian standard drinks (1 standaardglas / verre standard = 10 g pure alcohol). Data is
kept on the phone. You can also back it up to a private GitHub repository of your own.

- **Log**: saved drinks appear in rows by glass size (4, 12, 15, 20, 25, 33 cl). Tap one
  to add it now. **+** on a logged drink adds the same drink again. Use "Other drink" for
  anything else, and tick "Save to my drinks" to keep it. Use ‹ › or tap the date to log
  on another day. You can undo from the toast, or remove a drink with ×.
- **Trends**: bar chart per day, week or month, with the weekly guideline, plus total,
  average per week, alcohol-free days and heaviest day.
- **Settings**: manage saved drinks, set the weekly limit (default 10), set the hour a new
  day starts (default 05:00, so a 01:30 drink counts for the night before), and
  export or import a JSON backup.

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

## Online backup

The app saves all drinks to `drinks.json` in a **private** GitHub repository. It syncs a
few seconds after each change and every time the app is opened. Each sync is a commit,
so the repo history doubles as a log. With the same repo, a second phone stays in sync.
Removed drinks are removed everywhere.

One-time setup:

1. Create a **private** repository, for example `drink-data` (an empty one is fine).
2. Go to GitHub → Settings → Developer settings → Personal access tokens →
   **Fine-grained tokens** → Generate new token.
   - Repository access: **Only select repositories**, then pick `drink-data`.
   - Permissions → Repository permissions → **Contents: Read and write**.
   - Expiration: pick the longest you're comfortable with. When it expires, the app
     shows "Token rejected". Paste a new token to fix it.
3. In the app: Settings → Online backup. Enter `your-name/drink-data`, paste the token,
   and tap **Connect**.

The token stays on the phone and can only touch that one repository. The app refuses to
connect to a public repository.

## Backup file

**Settings → Export** downloads a JSON file. **Import** merges a file back in and skips
duplicates. Without online backup, data lives only in the app on the phone: uninstalling
it or clearing Chrome's site data deletes it.
