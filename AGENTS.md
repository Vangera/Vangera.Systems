# AGENTS.md — www.vangera.systems

Instructions for AI coding agents (Antigravity, Claude, Copilot, etc.) working on this repository.
Read this whole file before making changes.

## 1. What this site is

**www.vangera.systems** is the company website of **Vangera Systems**, a **one-person software house and IT services
company in Laos**, founded and run by **Lohn** (IT Manager, Systems Engineer, Biomedical Engineer —
personal site: https://www.lohn.cc/).

Purpose: win clients. Explain the services clearly, build trust through the founder's real experience,
and make it easy to get in touch.

Services:
1. System & software development (custom business systems, internal tools, integrations)
2. System administration & maintenance (Linux/Windows servers: patching, monitoring, backups, security, documentation)
3. Infrastructure & networks (single or multi-site)
4. Email, web & hosting (own-domain email with SPF/DKIM/DMARC, secure websites, application hosting)
5. Healthcare IT & biomedical support
6. IT management & consulting (interim/outsourced IT manager, planning, vendor coordination, knowledge transfer)

Sectors: healthcare, hospitality, manufacturing, research, security systems, SMEs.

Tone: professional, direct and trustworthy. Plain language a non-technical business owner understands.
It's honest about being a one-person company — that's a selling point (one accountable engineer, no hand-offs).
Use "I" for the founder's voice and "Vangera Systems" for the company; don't pretend to be a large team.

## 2. Facts — do not invent anything

Only state facts that are already in this repo or that the owner gives you. **Never invent** clients, case studies,
testimonials, numbers ("100+ projects", "99.9% uptime"), years in business, certifications, partnerships, prices,
office addresses, phone numbers, or awards. If a section needs a fact you don't have, leave a clearly marked TODO
and ask the owner.

Founder's past roles (most recent first, order still to be confirmed):

| Organisation | Role |
|---|---|
| A children's hospital (name not yet given) | IT Manager & Biomedical Engineer |
| Everlao (Everbright Headwear, China — spelling to confirm) | IT Supervisor — IT facilities + process tracking across 3 factories |
| Avani+ Luang Prabang, Pullman Luang Prabang, Avani+ Lanexang Vientiane | IT Manager — hotel properties in two cities |
| Institut Pasteur du Laos | IT Manager & Facility Manager |
| Lao Tobacco | IT Executive |
| Eyetech Security Systems | Product Engineer — knowledge transfer from Robert Bosch Thailand to Laos |

**Legal/honesty rule:** these are the founder's **past employers, not clients**. Always keep the note
"Listed organisations are past employers of the founder, not clients or endorsements." Never display their logos
or imply they endorse Vangera Systems.

Open questions to ask the owner: business registration/legal name, city/address to show, phone/WhatsApp,
pricing or packages (if any), real client projects that may be named, years of experience, languages
(English/Lao), whether a Lao-language version is wanted, logo files.

## 3. Tech stack and constraints

- **Hugo `0.167.0`** (pinned in `.github/workflows/deploy.yml` → `HUGO_VERSION`). Plain Hugo — no theme, no Node,
  no npm, no Tailwind, no Sass, no bundler. Keep it that way unless the owner explicitly asks.
- Uses Hugo's **new template system** (v0.146+): `layouts/baseof.html`, `layouts/home.html`, `layouts/page.html`,
  `layouts/404.html`, `layouts/_partials/`, `layouts/_shortcodes/`, `layouts/robots.txt`.
  Do **not** create `layouts/_default/` or `layouts/partials/` (old layout).
- Use current APIs: `hugo.Data` (not `.Site.Data`), `site.Language.Locale`, `locale` in config.
- CI builds with `hugo --gc --minify --panicOnWarning` — **any Hugo warning fails the deploy**.
- Plain CSS in `assets/styles.css` (fingerprinted via `resources.Get`) with CSS custom properties; light + dark mode via `prefers-color-scheme`.
- System font stacks only — **no web fonts, no Google Fonts, no external CDNs**.
- **No ads, no affiliate links, no analytics or trackers** on this site. It's a professional services site.

### Content Security Policy (enforced by the server — you cannot change it from this repo)

```
default-src 'self'; img-src 'self' data:; style-src 'self'; script-src 'self'; font-src 'self';
object-src 'none'; base-uri 'self'; form-action 'self' mailto:; frame-ancestors 'none'; upgrade-insecure-requests
```

This means:
- **No inline `<script>`** blocks or `onclick=` handlers. All JS goes in files under `static/js/`.
- **No inline `style="…"` attributes** and no `<style>` blocks. All CSS goes in `assets/styles.css`.
  (Presentation attributes inside inline SVG, like `fill=`, are fine.)
- **No external resources** (scripts, styles, fonts, images, iframes, maps, video embeds, chat widgets).
  Images must be committed to the repo (`static/images/`) — prefer WebP/AVIF/SVG, always set width/height and `alt`.
- If a feature genuinely needs an external resource, **stop and tell the owner** — the CSP must be changed on the server first.

## 4. Structure — where things live

| What | File |
|---|---|
| Site config | `hugo.toml` |
| Hero eyebrow/headline/lede, sectors, About heading + text | `content/_index.md` |
| Services | `data/services.yaml` |
| Founder's past roles | `data/roles.yaml` |
| "How I work" steps | `data/steps.yaml` |
| Privacy policy | `content/privacy.md` |
| Form result pages | `content/contact/thanks.md`, `content/contact/error.md` |
| Page frame / head / header / footer | `layouts/baseof.html`, `layouts/_partials/*.html` |
| Home page sections | `layouts/home.html` |
| Styles | `assets/styles.css` — Hugo fingerprints it (`styles.<hash>.css`) so browsers never use a stale copy; never link it by a fixed URL |

Brand: navy `#0b1530` / `#13214a`, amber accent `#f5a524`, link blue `#1d4ed8`; bold sans-serif headings;
"V" chevron logo (inline SVG in `layouts/_partials/header.html`, favicon in `static/favicon.svg`); radius 16px.
Header, hero, contact and footer are always navy; content sections switch between light and dark.

Possible future pages (only when the owner asks): individual service pages (`content/services/<slug>.md`),
case studies (only real, approved ones), a Lao-language version (Hugo multilingual).

## 5. Contact form — do not break this contract

The form is in `layouts/_partials/contact-form.html` and is handled by a backend service on the server
(not in this repo). Messages go to `info@vangera.systems`. The backend expects exactly:

- `GET /api/challenge` → ALTCHA challenge (fetched by the widget)
- `POST /api/contact` (form-encoded) with fields **`name`** (≤100 chars), **`email`**, **`message`** (10–5000 chars),
  **`website`** (honeypot — must stay hidden and empty), **`altcha`** (set by the widget)
- Responds `303` → `/contact/thanks/` or `/contact/error/` (those pages must keep existing)

The ALTCHA widget files are self-hosted in `static/assets/altcha/` (CSP-safe "external" build + PBKDF2 worker) and
loaded by `static/js/contact.js`. You may restyle the form or add a visible "subject"/"service" `<select>` only after
the owner confirms the backend accepts it — unknown fields are currently ignored. Keep the field names, the action
URL, the honeypot, and the `<altcha-widget challenge="/api/challenge">` element. Don't swap ALTCHA for another captcha.

## 6. Deployment

- `main` is production. **Every push to `main` deploys to the live site within ~30 seconds** via
  `.github/workflows/deploy.yml` (Hugo build → rsync over SSH to the server).
- Do not modify the deploy workflow, the `DEPLOY_SSH_KEY` secret, the pinned host key, or the action SHA pins
  unless the owner asks. To upgrade Hugo, change `HUGO_VERSION` only and test locally first.
- Prefer working on a branch and opening a pull request, so the owner can review before it goes live.
- Never commit secrets, API keys, or private data.

## 7. Before every commit — checklist

```bash
hugo --gc --minify --panicOnWarning     # must finish with no warnings
hugo server                              # check in a browser, light + dark mode, mobile width (~375px)
```
- [ ] No inline scripts/styles, no external URLs loaded by the page (links are fine)
- [ ] Every image has `alt`, width and height; headings in order; one `h1` per page
- [ ] Layout works at 375px wide with no horizontal scroll; nav still usable on mobile
- [ ] Colour contrast meets WCAG AA (amber text on white needs the darker `#c27c0e`)
- [ ] Contact form fields/action unchanged; `/contact/thanks/` and `/contact/error/` still build
- [ ] No invented facts, clients, numbers or testimonials; past-employer note still present
- [ ] `public/` is not committed (it's in `.gitignore`)

## 8. Out of scope (server-side — ask the owner)

Web server (Caddy) config and CSP, TLS, DNS, the contact-form backend, email (Mailcow), and the server itself are
managed separately. If a change needs any of these, describe what's needed and stop.
