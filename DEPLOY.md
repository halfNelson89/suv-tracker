# SUV Tracker — Deploy to a public URL

This folder is a complete PWA (Progressive Web App). You drop it on a free static-hosting service, get a public URL, and your wife taps "Add to Home Screen" on her iPhone — it shows up as an app icon, opens fullscreen, and looks like a real app.

## Files in this folder
- `index.html` — the app
- `manifest.json` — PWA manifest (so iOS/Android treat it as an installable app)
- `apple-touch-icon.png` — 180×180 icon iOS uses on the home screen
- `icon-192.png`, `icon-512.png` — Android & PWA icons
- `data.json` — the listing data (this file gets overwritten each morning by the scheduled task)

---

## Easiest first deploy: Netlify Drop (2 minutes, no account needed for first try)

1. Open https://app.netlify.com/drop in your browser
2. Drag this entire `suv-pwa` folder onto the page
3. You get an instant URL like `random-name-1234.netlify.app`
4. Optional: claim the site (free Netlify account) to keep it permanent and rename it
5. Text the URL to your wife

To update later: drag the folder onto Netlify Drop again. **Note:** without an account, the URL changes each time. With a free account, the URL is stable.

---

## Recommended for daily auto-updates: GitHub Pages (10 min setup, then automatic forever)

This path lets the daily scheduled task push fresh data automatically.

### One-time setup
1. Create a free GitHub account at https://github.com/signup if you don't have one
2. Install GitHub Desktop from https://desktop.github.com (easier than command line)
3. In GitHub.com, click **+ → New repository**. Name it `suv-tracker`. Set it **Public**. Click **Create repository**.
4. In GitHub Desktop: **File → Clone repository → suv-tracker** → pick a folder on your Mac (suggest `~/Documents/GitHub/suv-tracker`)
5. Copy ALL files from this `suv-pwa` folder into that cloned folder
6. Back in GitHub Desktop, you'll see the new files listed. Type a commit message ("initial deploy") and click **Commit to main**, then **Push origin**
7. On GitHub.com, go to your repo → **Settings → Pages**. Under "Build and deployment" set Source to **Deploy from a branch**, branch **main**, folder **/ (root)**. Click Save.
8. Wait ~1 minute. Your site is live at `https://YOUR-USERNAME.github.io/suv-tracker/`

### Wire it to the daily refresh
Once the site is live, paste your local repo path into the chat and I'll update the scheduled task `suv-deal-finder-daily` so it:
- Runs the daily scrape at 6:06 AM ET
- Writes the fresh `data.json` into your local repo folder
- Commits and pushes to GitHub
- GitHub Pages redeploys automatically (~1 min)

Your wife's installed app will show fresh listings the next time she opens it.

---

## How your wife installs the app on her iPhone

1. She opens the URL in **Safari** (must be Safari — not Chrome — on iOS for Add to Home Screen to work properly)
2. Taps the **Share** button (square with arrow up) at the bottom
3. Scrolls down, taps **Add to Home Screen**
4. Names it (default is "SUV Tracker")
5. Taps **Add**
6. The icon appears on her home screen. Tapping it opens the app fullscreen — no browser chrome — just like a real app.

---

## Things to know

- **No App Store**: this is a web app, not a native iOS app. App Store distribution requires an Apple Developer account ($99/yr) and 1–4 weeks of review. Add-to-Home-Screen is what 99% of "indie apps" use these days.
- **Data freshness**: the app caches the last loaded data, so it works offline. Each time she opens it with internet, it tries to fetch the latest `data.json`.
- **Her settings persist**: APR, term, down payment, insurance overrides are stored on her phone via localStorage and won't get blown away when the daily refresh updates the listings.
- **Cost**: Netlify and GitHub Pages are both free for personal use. No credit card needed.
