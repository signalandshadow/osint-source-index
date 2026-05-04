# Deployment guide

Step-by-step for getting the OSINT Source Index live and embedded at signalandshadow.io/osint-source-index.

This guide assumes a GitHub account exists. If not, create one at github.com first.

## Part 1: Create the repository

1. Go to github.com and click the **+** icon top right, then **New repository**.
2. Repository name: `osint-source-index` (recommended; matches the URL path).
3. Description: `OSINT Source Index — a curated register of institutional sources for investigative journalism. signalandshadow.io.`
4. Visibility: **Public**. The repository must be public for free GitHub Pages.
5. **Do not** initialise with a README, .gitignore, or licence — the package already contains these.
6. Click **Create repository**.

The repository is now created at `https://github.com/USERNAME/osint-source-index` (replace USERNAME with your GitHub username).

## Part 2: Upload the files

Two options. Pick whichever you prefer.

### Option A: Web upload (no command line)

1. On the repository page, click **uploading an existing file** (or use the **Add file** dropdown then **Upload files**).
2. Drag the following files from your local download into the upload area:
   - `index.html`
   - `README.md`
   - `CHANGELOG.md`
   - `LICENSE-CODE.txt`
   - `LICENSE-DATA.txt`
   - `.gitignore`
   - `DEPLOYMENT.md` (this file)
3. Commit message: `Initial release — OSINT Source Index issue 065`.
4. Click **Commit changes**.

The web upload supports files up to 100 MB. `index.html` is around 2.7 MB, well within limits.

### Option B: Command line (git CLI)

```bash
cd path/to/where/you/extracted/the/files
git init
git add .
git commit -m "Initial release — OSINT Source Index issue 065"
git branch -M main
git remote add origin https://github.com/USERNAME/osint-source-index.git
git push -u origin main
```

Replace `USERNAME` with your GitHub username.

## Part 3: Enable GitHub Pages

1. On the repository page, click **Settings** (top nav, right side).
2. In the left sidebar, click **Pages** under "Code and automation".
3. Under **Build and deployment**:
   - **Source**: Deploy from a branch
   - **Branch**: `main` (or `master` if your default branch is named that), `/ (root)` folder
4. Click **Save**.

GitHub will start building the site. After 30 to 90 seconds, refresh the Pages settings page. A green banner appears at the top:

> Your site is live at `https://USERNAME.github.io/osint-source-index/`

That URL is the canonical deployed location. Open it in a browser to confirm the Index loads.

## Part 4: Embed at signalandshadow.io/osint-source-index

The Index is served from GitHub Pages. The signalandshadow.io page contains an iframe pointing at it.

In your beehiiv site (or wherever signalandshadow.io is hosted), create a page at the path `/osint-source-index` with the following HTML embed:

```html
<iframe
  src="https://USERNAME.github.io/osint-source-index/"
  style="width: 100%; height: 100vh; min-height: 800px; border: 0; display: block;"
  title="OSINT Source Index"
  loading="lazy"
></iframe>
```

Replace `USERNAME` with your GitHub username.

If beehiiv's page editor restricts iframe embedding, two alternatives:

1. Use beehiiv's HTML/embed block if available.
2. Host the wrapper page elsewhere (e.g. a Cloudflare Worker, Netlify, or a single static HTML file on a subdomain) and point a custom domain at it.

## Part 5: Test the deployment

1. Visit `https://USERNAME.github.io/osint-source-index/` directly. Verify:
   - The Index loads with 1,811 sources counted in the top bar
   - The Database view renders cards on the right
   - Search filters work and surface facets in the left rail
   - The Map / Database toggle switches views
   - Clicking a card opens the detail overlay
   - Download sources.json button produces a valid JSON file

2. Visit `signalandshadow.io/osint-source-index`. Verify:
   - The iframe loads with no scrollbars on the parent page
   - The Index inside the iframe is fully usable
   - Clicking external account links (Twitter, etc) opens new tabs

## Part 6: Updating the Index

When the dataset is updated to a new issue:

1. Replace `index.html` in the repository with the new build.
2. Update `CHANGELOG.md` with the new issue notes.
3. Commit. GitHub Pages rebuilds automatically within 30 to 90 seconds.

## Custom domain (optional)

If you want the GitHub Pages URL to be `atlas.signalandshadow.io` or similar instead of `username.github.io/osint-source-index`:

1. In the repository, add a `CNAME` file containing one line: `atlas.signalandshadow.io`
2. In your DNS provider (Cloudflare, Namecheap, wherever signalandshadow.io is registered), add a CNAME record:
   - Name: `atlas` (or whatever subdomain)
   - Value: `USERNAME.github.io`
3. In the repository's Pages settings, enter the custom domain and save.
4. Wait for DNS propagation (usually under an hour), then enable "Enforce HTTPS".

Then update the iframe `src` to use the custom domain.

## Troubleshooting

**Index doesn't load on GitHub Pages.**
Wait two minutes after enabling Pages, then hard-refresh (Cmd+Shift+R / Ctrl+Shift+R). The first build can take a moment.

**Iframe shows blank or "refused to connect".**
Check that the `src` URL is correct and reachable directly in a browser. GitHub Pages requires HTTPS, so any non-HTTPS embed page will be blocked by browser security.

**Search or filters don't work.**
Open browser dev tools (F12) and check the Console tab for errors. The most common cause is a CSP (Content Security Policy) on the parent page blocking inline scripts. The Index is self-contained but uses inline JavaScript.

**Custom domain shows "site not found".**
DNS hasn't propagated yet. Wait an hour and check `dig atlas.signalandshadow.io` (or use a DNS lookup site) to confirm the CNAME points at GitHub.

## Maintenance

GitHub Pages is free and stable. Once configured, no ongoing maintenance is required unless you're updating content. The repository is the source of truth; everything else is auto-derived.
