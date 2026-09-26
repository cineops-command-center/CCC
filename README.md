# CineOps Command Center — Unified Content Operations

A single-page, client-side dashboard for managing DCP (Digital Cinema Package)
bookings, a theatre status matrix, and a KDM/key vault tracker.

## How it works

- **Pure static site.** Everything lives in one file: `index.html`. There is
  no server, no build step, and no backend API.
- **Data storage.** All records (DCP bookings, matrix rows/columns, vault
  nodes) are saved in the visitor's own browser via `localStorage`. Nothing
  is sent to a server, and nothing is shared between visitors or devices.
  Clearing browser data/localStorage for the site will reset it.
- **Spreadsheet import/export.** Uses `xlsx.js` and `jszip.js` (loaded from
  the `cdnjs.cloudflare.com` CDN) for importing `.xlsx` files and exporting
  CSV/ZIP downloads.
- **Fonts.** Loaded from Google Fonts (`Plus Jakarta Sans`, `JetBrains Mono`).

Because it's fully static, it can be hosted on **GitHub Pages** for free with
no configuration beyond enabling Pages on the repo.

## Repository contents

```
cineops-command-center/
├── index.html      # the entire application
├── README.md        # this file
└── .gitignore
```

## Deploy it yourself

### 1. Create the GitHub repository
1. Go to https://github.com/new
2. Name it (e.g. `cineops-command-center`), choose Public or Private, and
   create the repo **without** a README (you already have one here).

### 2. Push this package to GitHub
From inside this folder, run:

```bash
git init
git add .
git commit -m "Initial commit: CineOps Command Center dashboard"
git branch -M main
git remote add origin https://github.com/<your-username>/<your-repo>.git
git push -u origin main
```

### 3. Turn on GitHub Pages
1. In your repo on GitHub, go to **Settings → Pages**.
2. Under **Build and deployment → Source**, choose **Deploy from a branch**.
3. Under **Branch**, choose `main` and folder `/ (root)`, then **Save**.
4. Wait 30–60 seconds. GitHub will show your live URL, typically:
   ```
   https://<your-username>.github.io/<your-repo>/
   ```

That's it — no build tools, no `npm install`, no server required.

### Alternative hosts (also zero-config, drag-and-drop friendly)
- **Netlify**: netlify.com/drop → drag the folder in, done.
- **Vercel**: `vercel --prod` from the folder (after `npm i -g vercel`).
- **Cloudflare Pages**: connect the GitHub repo, framework preset "None",
  build command empty, output directory `/`.

## Notes / limitations to be aware of

- **Private within a browser only.** Since data is stored in `localStorage`,
  each teammate visiting the deployed link will see their *own* empty
  dashboard, not shared data. This tool is best used as a personal/local
  tracker, or by a single team member on one browser/machine, unless you
  extend it with a real backend (e.g., Supabase, Firebase, a small API) to
  centralize storage.
- If you fork/rename the repo, GitHub Pages will change to match the new
  repo name unless you configure a custom domain.
- To use a custom domain, add a `CNAME` file to the repo root with your
  domain, and configure the DNS records GitHub specifies under
  **Settings → Pages → Custom domain**.
- The "Google Drive" / "OneDrive" mount options in the Vault tab are UI
  placeholders in the current code — check `index.html` if you intend to
  wire up real cloud storage connections.

## License
MIT — see `LICENSE`.
