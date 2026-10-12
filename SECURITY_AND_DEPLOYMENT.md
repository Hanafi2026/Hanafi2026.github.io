# Deployment and security notes

## Files
Upload `index.html`, `robots.txt`, `sitemap.xml`, and the complete `assets/` folder to the root of the GitHub Pages repository. Keep your existing `photo.jpg` and Google Search Console verification HTML file in the repository root. Do not remove either.

## Implemented controls
- Restrictive Content Security Policy in an HTML meta tag (no third-party scripts, network fetches, embeds, forms, or inline executable JavaScript). The sole inline JSON-LD block is allowed by a SHA-256 CSP hash.
- External, first-party JavaScript and CSS; no inline event handler; no `eval`, external fonts, analytics or third-party dependencies.
- `noopener noreferrer` on outbound links; no client-side secrets or API keys.
- Search metadata, canonical URL, social previews, Person JSON-LD, sitemap, robots.txt.

## Important limitations
No website is attack-proof. GitHub Pages does not let this repository set arbitrary HTTP response security headers. A meta CSP cannot enforce `frame-ancestors`, so this package does not prevent clickjacking through that directive. Other header-only controls such as `X-Frame-Options`, `X-Content-Type-Options`, HSTS, and Permissions-Policy require support at the hosting/CDN layer. A file named `_headers` would NOT activate these on GitHub Pages.

If you later move to a platform supporting custom response headers, set a header CSP including `frame-ancestors 'none'` and appropriate additional security headers after testing.

## Operational protection
1. Enable GitHub account two-factor authentication or passkeys.
2. Keep repository write access limited; use protected branches and review changes before publishing.
3. Never commit tokens, passwords, private files, research datasets, or credentials. Everything in a public GitHub Pages repository is public.
4. Maintain backups; periodically review GitHub repository activity and deployed page source.
5. Keep HTTPS enabled and check the deployed site after each update.
6. Avoid third-party scripts/widgets unless necessary; assess each before adding.
7. Run Google Search Console URL Inspection and submit sitemap.xml after deployment.
8. Review browser console for CSP violations and verify tabs, portrait, and external links.

## CSP maintenance
The inline JSON-LD block is authorized by a SHA-256 hash in the CSP. If you edit JSON-LD content, regenerate the hash or browsers may block that block. Alternatively, use a trusted build step to regenerate the hash on every deployment.

## Site functionality
The About Me and Contact tabs, current design and content, and local portrait file reference are preserved.
