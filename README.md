# Français — Dossiers d'étude (site d'hébergement)

Static site hosting all Unit dossiers under one URL. No build step, no dependencies — every file here is served as-is.

## Structure

```
/index.html         → landing page, links to each unit
/unite-1/index.html → Unit 1 dossier (v3.1.0.1)
/unite-2/index.html → Unit 2 dossier (v1.2.0)
/unite-3/index.html → Unit 3 dossier (v1.1.2)
```

Each unit's dossier is the *exact* file already validated and used offline — nothing was changed except its location. Visiting `yoursite.pages.dev/unite-2/` shows the identical dossier a student would get by downloading the HTML file directly, including localStorage progress tracking (saved per browser/device).

## First-time setup (one-time, ~10 minutes)

1. Create a GitHub account (ideally under a shared or project email, not a personal one — makes future ownership transfer clean).
2. Create a new **public** repo, e.g. `francais-dossiers`.
3. Upload the contents of this folder to the repo root (drag-and-drop works fine in GitHub's web UI — no command line required).
4. Go to [pages.cloudflare.com](https://pages.cloudflare.com), sign up (free tier), and choose **"Connect to Git"**.
5. Select the repo. Build settings: leave the build command **blank** and set the output directory to `/` (this is a static site, nothing to build).
6. Deploy. Cloudflare gives you a URL like `francais-dossiers.pages.dev` immediately.
7. (Optional, later) Add a custom domain under the Cloudflare Pages project settings if you want something like `francais.example.org`.

## Updating a dossier (routine — do this every new version)

1. Open the repo on GitHub (web UI is fine).
2. Navigate to the relevant folder (`unite-2/`, etc.).
3. Click the existing `index.html` → **Edit** (pencil icon) or delete + re-upload the new file with the same name `index.html`.
4. Commit the change.
5. Cloudflare Pages redeploys automatically within ~30–60 seconds. No further action needed.

## Adding a new unit

1. Create a new folder in the repo, e.g. `unite-4/`.
2. Add the dossier file inside it, named `index.html`.
3. Add a new folder card to `index.html` at the repo root (copy an existing `<a class="folder">` block, update the unit number, chapter range, version, and `href="/unite-4/"`).
4. Commit — live within a minute.

## Access control (not yet configured)

Currently the site is open to anyone with the URL. To restrict access to specific accounts later:

- Cloudflare **Zero Trust → Access** can require login (Google Workspace, Microsoft Entra ID, or a One-Time-PIN via email) before the site loads at all — no changes needed to the dossier files themselves.
- This is a settings change in the Cloudflare dashboard, not a rebuild.

## Migration (if you move this off Cloudflare or add real user accounts later)

Because this is a plain static site, moving hosts is a copy-paste job, not a rebuild:

- To **GitHub Pages**: point Pages at the same repo.
- To **Azure Static Web Apps** (recommended if you want Microsoft/Entra ID-based login and cross-device saved progress down the line): same repo, same files — Azure's static hosting works the same way, and integrates with Entra ID for login if/when account-based progress tracking becomes a requirement.

No dossier file needs to change for a hosting migration. Only a real accounts/progress-sync system (a separate, later project) would require new code.
