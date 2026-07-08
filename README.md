# Momently Website

The marketing site for Momently — the on-demand content-creator app (Greenville, SC flagship launch). A static, multi-page site built with [Vite](https://vitejs.dev), no framework required.

## Pages

- `index.html` — homepage (hero, features, pricing, Greenville section, agent recruiting, waitlist form)
- `privacy-policy.html`, `terms-of-service.html`, `support.html` — draft legal/support pages (**have counsel review before publishing**)

## Requirements

- Node.js 18+ and npm

## Setup

```bash
npm install
cp .env.example .env   # then fill in the values below
```

## Environment variables

Set these in a `.env` file at the project root (never commit `.env` — it's already in `.gitignore`).

| Variable | Required? | What it does | Where to get it |
|---|---|---|---|
| `VITE_WAITLIST_ENDPOINT` | Yes, for the waitlist form to actually work | The homepage's "Join Waitlist" form POSTs the email here as JSON. Without it, the form shows a "not connected yet" message instead of submitting. | Create a free form at [formspree.io](https://formspree.io) (or Getform, Basin, etc.) and paste its endpoint URL, e.g. `https://formspree.io/f/abcd1234` |
| `VITE_ANALYTICS_ID` | No | If set, loads Google Analytics 4 (gtag.js) with this Measurement ID. Leave blank to skip analytics entirely. | Google Analytics Admin → Data Streams → Measurement ID (`G-XXXXXXXXXX`) |

Vite only exposes variables prefixed `VITE_` to the built site — this is intentional and required, don't rename them.

## Build command

```bash
npm run build
```

## Output directory

```
dist/
```

This is the folder to deploy — it contains the fully built, static `index.html`, `privacy-policy.html`, `terms-of-service.html`, `support.html`, and a `dist/assets/` folder with the bundled JS. Upload the contents of `dist/` to any static host.

## Local development

```bash
npm run dev       # starts a local dev server with hot reload
npm run preview   # serves the built dist/ folder locally, to sanity-check the production build
```

## Deploying

Any static host works since there's no server-side code:

- **Netlify / Vercel (easiest):** connect the git repo, set build command `npm run build` and publish/output directory `dist`, then add the environment variables above in the host's dashboard (not just your local `.env`) so the live build has them too.
- **Manual:** run `npm run build` locally and drag-and-drop the `dist/` folder into Netlify's deploy UI, or upload it to any static file host (S3 + CloudFront, GitHub Pages, etc.).

## Before going live

- [ ] Replace `VITE_WAITLIST_ENDPOINT` with a real, working form endpoint and test that a submission actually arrives somewhere you monitor.
- [ ] Have counsel review `privacy-policy.html` and `terms-of-service.html` — both are template drafts.
- [ ] Confirm "Momently" is clear for trademark use, or swap the name throughout before launch.
- [ ] Once the iOS app is live, replace the `#waitlist` calls-to-action with the official Apple "Download on the App Store" badge and a real App Store link (see the companion `Momently_App_Store_Launch_Requirements.docx`).
