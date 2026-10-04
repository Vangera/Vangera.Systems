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

The founder is **Nakhonekham (Lohn) Xongmixay**, based in Vientiane. His career data (roles, employers, years,
projects, training) comes **only** from `https://www.lohn.cc/profile.json` — see section 4b. Pre-opening hotel
experience applies to **Avani+ Lanexang Vientiane** only.

**Legal/honesty rule:** organisations in the founder's history are **past employers, not clients**. Always keep the
note "Listed organisations are past employers of the founder, not clients or endorsements." Never display their logos
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
- **No ads shown, no affiliate links, no analytics or trackers** on this site. It's a professional services site.
  `static/ads.txt` and the `google-adsense-account` verification `<meta>` (`params.adsenseClient`) only declare
  the owner's AdSense publisher ID; they load nothing. Showing ads would need the owner's decision, a consent
  banner, a Privacy update and a CSP change on the server — don't add ad code.

### Design system (UI refinement, Oct 2026)

- **Colours only via tokens** in `assets/styles.css` (`--bg`, `--surface`, `--ink`, `--muted`, `--line`, `--alt`, `--label`, `--stat`, `--link`, `--navy`, `--amber`…).
  Never hard-code colours in components and never add new `@media (prefers-color-scheme: dark)` rules —
  dark mode is the two token blocks at the top (automatic **and** `:root[data-theme="dark"]` for the manual toggle).
  Every text colour pair must meet WCAG AA (4.5:1 for normal text); dark-mode text is deliberately softened (~12–14:1).
- **Typography:** body 18px; no text smaller than 13px (13px only for short uppercase labels).
- **Icons:** use `{{ partial "icon.html" "name" }}` (inline SVG, `currentColor`). No emoji as icons.
  Available: pin, mail, linkedin, arrow-right, external, sun, moon, menu, close, code, server, network, health, compass, check.
- **JavaScript:** only `assets/js/site.js` (theme toggle + mobile menu), loaded fingerprinted in `<head>`. The site must still
  work without it (links wrap on small screens, theme follows the device).
- **Hierarchy:** at most one primary and one secondary button per section; tap targets ≥ 44px.

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
| Founder's track record (years, sectors, projects, employers, training) | **Not in this repo** — fetched at build time from `https://www.lohn.cc/profile.json` by `layouts/_partials/founder.html` |
| "How I work" steps | `data/steps.yaml` |
| Privacy policy | `content/privacy.md` |
| Form result pages | `content/contact/thanks.md`, `content/contact/error.md` |
| Page frame / head / header / footer | `layouts/baseof.html`, `layouts/_partials/*.html` |
| Title, description, canonical, Open Graph tags | `layouts/_partials/head.html` |
| Search-engine data: Organization + WebSite (home only) | `layouts/_partials/jsonld-org.html` |
| Search-engine data: breadcrumbs, guides (`schema_type`) | `layouts/_partials/jsonld-page.html` |
| robots.txt (sitemap is Hugo's built-in `/sitemap.xml`) | `layouts/robots.txt` |
| AdSense seller declaration (no ads shown) | `static/ads.txt` |
| Home page sections | `layouts/home.html` |
| Styles | `assets/styles.css` — Hugo fingerprints it (`styles.<hash>.css`) so browsers never use a stale copy; never link it by a fixed URL |

Brand: navy `#0b1530` / `#13214a`, amber accent `#f5a524`, link blue `#1d4ed8`; bold sans-serif headings;
"V" chevron logo (inline SVG in `layouts/_partials/header.html`, favicon in `static/favicon.svg`); radius 16px.
Header, hero, contact and footer are always navy; content sections switch between light and dark.

Possible future pages (only when the owner asks): individual service pages (`content/services/<slug>.md`),
case studies (only real, approved ones), a Lao-language version (Hugo multilingual).

## 4a. SEO — keep these true

**Structured data (JSON-LD)** is built from `hugo.toml`, `data/services.yaml` and the founder's profile.json —
never type facts into it. Home: `Organization` (`#organization`: name, description, email, logo, area served Laos,
founder, services as an `OfferCatalog`) and `WebSite`. No address, phone or prices until the owner publishes them.
The founder is the `Person` with `@id` `https://www.lohn.cc/#person` — the same entity www.lohn.cc describes — and
www.lohn.cc points back to `https://www.vangera.systems/#organization`; keep both @ids stable.
Other pages get a `BreadcrumbList`; a guide gets `schema_type: "TechArticle"` in front matter.
Check changes with Google's Rich Results Test and validator.schema.org.

**Front matter for pages:** `seo_title` (shorter `<title>` if needed), `description`, `lastmod` (set when the page
changes substantially — it feeds the sitemap), `schema_type`, and `robots: "noindex"` for pages that must stay out
of search results (not a robots.txt `Disallow`, which would hide the noindex).

**Checklist for every page**
- [ ] `<title>` ≤ ~60 characters including " — Vangera Systems" (use `seo_title` otherwise); main words first.
- [ ] `description` 120–160 characters: what the visitor gets, in plain words.
- [ ] Exactly one `h1`, then `h2` for sections, `h3` inside them, `h4` inside those — never skip a level for
  looks (style with CSS instead).
- [ ] Open Graph title/description/URL and the Twitter card are automatic; there is no share image yet (needs a
  1200×630 brand image from the owner).
- [ ] Images: descriptive `alt`, width and height.
- [ ] Meaningful link text; link services to the contact section.
- [ ] Set `lastmod` after a substantial change.

## 4b. Founder data comes from lohn.cc — do not duplicate it

The founder's CV lives only in the **lohn.cc** repo (`data/*.yaml`), published as `https://www.lohn.cc/profile.json`
(schema v1). This site fetches it at build time (`layouts/_partials/founder.html`) and renders the
"Founder's track record" section. Rules:
- Never copy CV facts (years, employers, projects, training) into this repo — change them in lohn.cc instead.
- Never hard-code computed numbers (years, organisation count); use `$f.summary.*` / `$f.sectors`.
- The build **fails on purpose** if profile.json can't be fetched or has an unknown schema — fix the feed, don't
  add a silent fallback.
- Remote fetches are restricted to `^https://www\.lohn\.cc/` (`[security.http]` in hugo.toml).
- The workflow also rebuilds daily at 05:30 Laos time (cron) so CV updates appear without a push here.
- Keep the note that listed organisations are past employers of the founder, not clients or endorsements.
- Local preview needs internet access (it fetches the live profile.json).

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
