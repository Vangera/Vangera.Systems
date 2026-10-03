# www.vangera.systems

Company site of Vangera Systems — built with [Hugo](https://gohugo.io), deployed automatically.

## Edit
| What | Where |
|---|---|
| Headline, intro, sectors, About text | `content/_index.md` |
| Services | `data/services.yaml` |
| Founder track record | Fetched from https://www.lohn.cc/profile.json at build time — edit the CV in the lohn.cc repo |
| How I work steps | `data/steps.yaml` |
| Privacy policy | `content/privacy.md` |
| Styles | `assets/styles.css` (fingerprinted at build: `styles.<hash>.css`) |

## Preview locally
```bash
hugo server
```

## Publish
Merge a pull request into `main` — GitHub Actions builds the site and deploys it in about 30 seconds.
The site also rebuilds daily at 05:30 (Laos time) to pick up CV changes from lohn.cc.
The workflow needs one repository secret: `DEPLOY_SSH_KEY`.

The contact form posts to `/api/contact`, served by the contact-form service on the server.
