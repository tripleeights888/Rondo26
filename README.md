# Rondo

A World Cup 2026 sticker collection and trade tracker. Rondo runs entirely in your browser, works offline, and installs to your phone's home screen like a real app. Your data is saved on your own device.

Rondo is an unofficial fan-made tracker. Not affiliated with or endorsed by Panini or FIFA. All trademarks belong to their respective owners.

---

## For users

### Installing on your phone

1. Open the app's web address in Safari (iPhone) or Chrome (Android).
2. Tap the Share icon, then "Add to Home Screen."
3. Open it from the new icon. It runs full screen and works offline.

Your collection is saved on your device, tied to this app. It is not stored online, so it stays private to you.

### The three tabs

- **TRADE**: your duplicate stickers, the spares you can trade away.
- **WANT**: stickers you still need.
- **STICK IT!**: everything you already own (your album).

### Adding stickers as you open packs

Tap **+ Quick add**. Type a team code (like KOR), then all the numbers from that pile separated by spaces or commas (like `8 9 10`), and tap **Commit pile**. Each sticker is filed automatically: new ones go to STICK IT!, repeats become spares in TRADE. You get a summary of what landed where, then the fields clear so you can grab the next pile.

### Searching and acting on a sticker

Type into the search box. You can search by:

- **Player name** (like `salah`)
- **Team code** (like `EGY`)
- **Code and number** (like `EGY 17`) for an instant verdict

Tapping a sticker, or searching a code and number, brings up an action popup at the bottom of the screen. From there you can trade a spare away, mark a want as got, or correct a mistake. The popup never moves your place in the list.

### Fixing mistakes

Nothing is permanent. Tap any sticker to correct it:

- In STICK IT!, "Don't own this" moves it back to WANT.
- In TRADE, "Remove spare" deletes an accidental duplicate.
- Most actions have an Undo.

### Selecting several at once

Tap **Select**, then tap multiple stickers, and apply one action to all of them (trade away, mark as got, or remove), depending on the tab.

### Favorites and progress

- Tap the star on any team to favorite it. Each favorite shows its own progress bar in the header.
- The header always shows your overall album completion.
- The STICK IT! tab shows completion per group and per team.

### Color tiers

Stickers come in rarity colors. On the STICK IT! tab, tap a sticker you own and pick its color tier (White through Black, plus special variants). Tagged stickers show a colored dot, and a "Color tiers" breakdown on the STICK IT! tab counts how many of each you have. White is the default, so you only tag the rarer ones.

### Comparing with a friend

Tap **Compare** and paste a friend's list. Rondo shows what you can trade them and what they have that you want. It handles messy lists with flags, emoji, and codes with or without spaces.

### Backing up and restoring

Your data lives only on your device, so back it up regularly.

- **Export** then "Send to file" saves a backup (to Google Drive, Files, or email).
- **Export** also offers a pasteable **Want list** and **Trade list** for posting on marketplaces.
- **Import** loads a backup back in. This replaces whatever is currently in the app.

Always export a backup before reinstalling the app, clearing your browser, or switching phones, since those wipe the on-device data.

---

## For deployment (hosting your own copy)

Rondo is a set of static files. Any static host works; these instructions use GitHub Pages (free).

### Files

A complete copy is just these files in one folder:

- `index.html` (the app)
- `manifest.json` (app name and icon settings)
- `service-worker.js` (offline support and auto-update)
- `icon-192.png`, `icon-512.png`, `apple-touch-icon.png` (the app icon)

### Deploy on GitHub Pages

1. Create a public repository.
2. Upload the files above to the top level (not inside a subfolder). `index.html` must be lowercase.
3. Go to Settings, then Pages.
4. Under "Build and deployment," set Source to "Deploy from a branch," choose `main` and `/ (root)`, and Save.
5. Wait a minute, refresh, and the page shows your live URL: `https://<username>.github.io/<repo>/`.

### Updating

Upload the new files (same names, which replaces the old ones) and commit. The app updates itself: every time it opens it checks for a new version, and if found it refreshes automatically. No reinstall needed.

The one exception is the very first time you move onto the self-updating version: you need to remove the app from your home screen and re-add it once. After that, updates are automatic.

### Two editions

- **Personal**: your collection baked in as the starting point.
- **Shared (blank)**: starts empty so a friend builds their own collection. It uses a separate storage key, so the two never interfere even on the same device.

Each edition is its own repository with its own files. Don't mix them: uploading the blank `index.html` to your personal repo would replace your starting data, and vice versa.

### A note on data

Updating the code on GitHub never changes anyone's collection. Each person's data is saved in their own browser, not in the repository. Deploying, updating, or sharing the app only swaps the app itself, never the data.

---

## Tech notes

- Pure HTML, CSS, and JavaScript. No build step required to run, no dependencies, no backend.
- Data is stored in the browser's `localStorage`.
- Offline support and automatic updates are handled by the service worker, whose cache version is stamped fresh on each build so updates always propagate.
