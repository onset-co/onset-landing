# Repository Instructions

## Project Shape

- This is a small Astro 5 landing site deployed as a Cloudflare Worker; `src/pages/index.astro` is the main route and `public/` holds static assets.
- The landing page is the custom Persian RTL page in `src/pages/index.astro`, composed from `src/components/site/`.
- `README.md` still contains starter-template text in places. Treat `package.json`, `astro.config.mjs`, `wrangler.json`, and the source tree as the current source of truth.

## Commands

- Use Node `>=22` and npm; `package-lock.json` is the lockfile.
- `npm run dev` starts the Astro development server on port 4321.
- `npm run check` is the canonical validation command: it builds Astro, runs `tsc`, then runs `wrangler deploy --dry-run`.
- `npm run preview` builds first and then starts `wrangler dev`; it is not the standard Astro preview command.
- Deploy with `npm run build && npm run deploy`; `npm run deploy` alone does not build the site.
- Run `npm run cf-typegen` after changing Wrangler bindings/config; it regenerates `worker-configuration.d.ts`.
- There are no repository lint or test scripts/configs; do not invent a test command when `npm run check` is the relevant verification.

## Generated And Deployment Files

- Do not edit `.astro/` or `dist/` by hand; Astro generates them and both are ignored.
- `wrangler.json` serves `dist/` as Worker assets and uses `dist/_worker.js/index.js` as the Worker entrypoint.
- `worker-configuration.d.ts` is Wrangler-generated; regenerate it rather than manually maintaining its bindings.
- `astro.config.mjs` sets `site` to `https://onset.ir`, which is used for canonical URLs and sitemap output; update it if the production domain changes.
