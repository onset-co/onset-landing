# Onset Landing

The Persian, right-to-left Onset product site, built with Astro 5 and deployed as a Cloudflare Worker on `https://onset.ir`.

## Development

Use Node.js 22 or newer and npm:

```sh
npm ci
npm run dev
```

The development server runs at `http://localhost:4321`. Before opening a pull request, run:

```sh
npm run check
```

This builds the site, runs TypeScript, and checks the Worker deployment with Wrangler.

## Production deployment

Pushing to `main` runs the GitHub Actions workflow in `.github/workflows/deploy.yml`. Pull requests run the same validation but do not deploy. A production deployment can also be started manually from the Actions tab.

Add these repository secrets in GitHub under **Settings > Secrets and variables > Actions**:

- `CLOUDFLARE_API_TOKEN`: a scoped token with permission to edit Workers and configure the `onset.ir` custom domain.
- `CLOUDFLARE_ACCOUNT_ID`: the Cloudflare account that owns the Worker and the active `onset.ir` zone.

Both must be **repository Actions secrets** with these exact names. If they are stored in a GitHub environment instead, the deploy job must declare that environment before it can read them. A missing secret resolves to an empty value and stops the deploy step.

Wrangler configures `onset.ir` as a Worker Custom Domain. The zone must be active in the same Cloudflare account, and the hostname must not have a conflicting DNS record. For a local production deploy, run `npm run check` and then `npm run deploy` after authenticating Wrangler.

## Project structure

- `src/pages/index.astro`: page composition and Persian RTL document shell.
- `src/components/site/`: hero, BeatMic, Beaton roadmap, about, and footer sections.
- `src/styles/global.css`: shared typography, colors, and layout primitives.
- `public/`: logo and product imagery.
- `wrangler.json`: Worker entry point, static assets, and `onset.ir` custom domain.
