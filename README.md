# www.vangera.systems

Company site of Vangera Systems — built with [Hugo](https://gohugo.io), deployed automatically.

## Edit
| What | Where |
|---|---|
| Headline, intro, sectors, About text | `content/_index.md` |
| Services | `data/services.yaml` |
| Founder experience | `data/roles.yaml` |
| How I work steps | `data/steps.yaml` |
| Privacy policy | `content/privacy.md` |
| Styles | `assets/styles.css` (fingerprinted at build: `styles.<hash>.css`) |

## Preview locally
```bash
hugo server
```

## Publish
Push to `main` — GitHub Actions builds the site and deploys it to the server in about 30 seconds.
The workflow needs one repository secret: `DEPLOY_SSH_KEY`.

The contact form posts to `/api/contact`, served by the contact-form service on the server.
