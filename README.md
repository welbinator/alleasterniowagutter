# alleasterniowagutter.com

All Eastern Iowa Seamless Gutter, Inc. — static site on **Cloudflare Pages** (project `alleasterniowagutter`).
Migrated off the Hetzner box (was plain static HTML served by nginx).

## Structure
- `public/` — the deployed site: 8 static HTML pages + `includes/` (CSS) + `siteimages/`.
- Contact form is an embedded **Cognito Forms** widget (external, nothing to host).
- `public/_redirects` — www -> apex 301.

## Migration fixes applied
- `contact.html` nav links were pointing at dead `.asp` files -> rewritten to `.html`.
- Removed dead `javascript/angular.min.js` + `contactController.js` script tags (the real
  form is Cognito, hosted externally; those local files never existed on the server).
- Dropped leftover server-side `.asp` includes and the cPanel `.htaccess`.

## Deploy
```
export CLOUDFLARE_API_TOKEN=$(python3 ~/.hermes/scripts/creds.py get cloudflare_api_token)
npx wrangler pages deploy public --project-name alleasterniowagutter --branch main --commit-dirty=true
```
