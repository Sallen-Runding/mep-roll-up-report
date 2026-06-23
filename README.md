# MEP Roll-Up Report

The Runding **MEP Roll-Up Report** — a private-equity deal tracker and newsletter for the U.S.
commercial MEP contractor market. This repository holds the published page and its source files.

## What's in here

```
index.html                         The report page (deal tracker + newsletter). This is what gets hosted/embedded.
downloads/
  MEP-Roll-Up-Report-2026-06.pdf   Print/share version of the June 2026 issue.
newsletter/
  2026-06.md                       The newsletter copy (for posting to LinkedIn).
README.md                          This file.
```

## View it locally
Double-click `index.html` — it opens in any browser. No build step, no dependencies.

## Publish it

You have two options. Either works; they are not mutually exclusive.

### Option A — GitHub Pages (fastest, no developer needed)
1. In this repo on GitHub, go to **Settings → Pages**.
2. Under **Build and deployment → Source**, choose **Deploy from a branch**.
3. Branch: **main**, folder: **/ (root)**. Click **Save**.
4. Wait ~1 minute. GitHub shows a live URL like `https://YOUR-ORG.github.io/mep-roll-up-report/`.

### Option B — Azure Static Web Apps (for your developers)
Your developers connect this repo to a new **Azure Static Web App**. When they do, Azure
automatically adds a GitHub Action to the repo that redeploys on every push to `main`.
App location: `/`. No build command and no output/API location are needed (this is a static site).

## Embed it in the website
Once the page has a public URL, drop this into a Webflow **Embed** element (or any page's HTML):

```html
<iframe
  src="https://YOUR-PUBLIC-URL/"
  title="MEP Roll-Up Report"
  width="100%"
  height="3200"
  style="border:0;"
  loading="lazy">
</iframe>
```

Note: `height` is fixed here (≈3200px for this issue). If the inner content grows, raise it, or
ask a developer to add an auto-resize script (`postMessage`) so the frame sizes itself.

## Updating for the next issue
1. Replace `index.html` with the new issue's page.
2. Add the new PDF to `downloads/` (e.g., `MEP-Roll-Up-Report-2026-07.pdf`).
3. Add the new newsletter copy to `newsletter/` (e.g., `2026-07.md`).
4. Commit the changes. If hosting is connected (Option A or B), the live site updates automatically.

## Roadmap
A small refactor would move the deal records out of `index.html` and into a `deals.json` file, so
future updates mean editing a structured list instead of regenerating the whole page. Recommended
once the cadence is regular.
