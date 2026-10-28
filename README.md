# soar.studio

Marketing site for **SOAR** — a Shopify app development studio.

Pure static HTML / CSS. No build step. Deploys free on **DigitalOcean App Platform** static sites.

## Structure

```
soar-studio/
├── public/              # everything that gets served
│   ├── index.html
│   ├── styles.css
│   └── soar-logo.png
├── .do/app.yaml         # DigitalOcean App Platform spec
└── README.md
```

## Local preview

```bash
cd public && python3 -m http.server 8080
# → open http://localhost:8080
```

## Deploy to DigitalOcean

### Option A — one-time via dashboard (easiest)

1. Push this repo to GitHub.
2. Go to **https://cloud.digitalocean.com/apps** → **Create App**.
3. Pick the GitHub repo, branch `main`.
4. DO will detect `.do/app.yaml` and configure it as a Static Site.
   - Source directory: `public`
   - Output directory: `/`
   - Fallback / 404: `index.html`
5. Pick the **Starter — Free** plan ($0/mo, 1 static site).
6. Click **Create Resources**.

### Option B — via `doctl` CLI

```bash
# install if needed: brew install doctl && doctl auth init
doctl apps create --spec .do/app.yaml
```

### Custom domain

In the DO App dashboard → **Settings → Domains** → add `soar.studio`.

Then at your registrar, point:
- `soar.studio` → `A` or `ALIAS` to the DO-provided target
- `www.soar.studio` → `CNAME` to the DO-provided target

DO issues a free Let's Encrypt cert automatically.

## Contact form

The form currently points at `https://formspree.io/f/your-id`. Replace with:

- A real Formspree form id, OR
- Your own endpoint (`/api/contact` on a tiny Function), OR
- A `mailto:hello@soar.studio` form fallback.

## Branding

- Logo: `public/soar-logo.png` (black wordmark; CSS inverts to white on dark bg).
- Accent: `--accent: #c4ff3d` in `styles.css` — swap for your brand color.
- Fonts: Inter + Space Grotesk from Google Fonts.
