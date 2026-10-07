# taiuto.co.uk

One-page website for Taiuto Ltd, a technical consultancy with a focus on AI projects,
founded by Andy Benedetti.

Live at <https://taiuto.co.uk>.

## What's in the repo

| File | Purpose |
|------|---------|
| `index.html` | The entire site. Single file, inline CSS, no build step. Fonts from Google Fonts. |
| `CNAME` | Tells GitHub Pages the custom domain. Do not delete or rename. |
| `.nojekyll` | Stops GitHub Pages running Jekyll, so the HTML is served as-is. |
| `dns-records.md` | Reference copy of every DNS record, including the DKIM key. |

## Hosting

The site is served by **GitHub Pages** from the `main` branch, root folder, in the
repo `andybenedetti/taiuto.co.uk`. Hosting is free.

Pushing to `main` deploys automatically. A deploy takes about a minute.

Settings live at <https://github.com/andybenedetti/taiuto.co.uk/settings/pages>.
The custom domain is `taiuto.co.uk` and "Enforce HTTPS" is on. GitHub's certificate covers
the apex only; `www` is handled by Cloudflare (see below).

## Domain and DNS

| Concern | Where | Notes |
|---------|-------|-------|
| Registration and renewal | Tide (resells Dreamscape / Crazy Domains) | Expires 27 June 2027. Only the name servers are set here. |
| DNS records | Cloudflare, free plan | Name servers `beau.ns.cloudflare.com` and `ximena.ns.cloudflare.com`. All records "DNS only". |
| Website | GitHub Pages | Four A records on the apex, DNS only. `www` is a CNAME to `andybenedetti.github.io` but **proxied** through Cloudflare, with a Cloudflare redirect rule sending it to `https://taiuto.co.uk`. |
| Email | Tide / Crazy Domains mail hosting | `hello@taiuto.co.uk`. MX to `mail.taiuto.co.uk`, SPF and DKIM published. |

Full record list: [`dns-records.md`](dns-records.md).

### Why DNS is on Cloudflare rather than Tide

Tide's panel offers DNS editing, but its name servers (`ns1/ns2.crazydomains.com`) never
published the SPF and DKIM records and kept returning the old parking address for a share
of lookups. Moving the records to Cloudflare fixed both problems within minutes. Domain
registration was not moved.

## Editing the site

1. Edit `index.html`. Open it in a browser to preview.
2. Commit and push to `main`.
3. Check <https://taiuto.co.uk> after a minute.

Design and copy notes:

- Single dark theme by choice: slate background with a faint drafting grid, Libre Caslon
  for the wordmark and headings, Work Sans for text, JetBrains Mono for the footer.
- The wordmark is `taiuto` with the `ai` in amber (`#f2b134`). Amber is the only accent.
- The page is deliberately minimal: wordmark, three service items, a "make contact" line
  with the email, and the footer with the registered company details. No navigation,
  no biography, no client list.
- Fonts load from Google Fonts; everything else is inline.

## Company details

| | |
|---|---|
| Registered name | Taiuto Ltd |
| Company number | 15801670 |
| Registered office | 3rd Floor, 86-90 Paul Street, London EC2A 4NE |
| Contact | hello@taiuto.co.uk |
| LinkedIn | <https://www.linkedin.com/in/andy-benedetti/> |

Source: Companies House, 4 October 2026.

## TODO

- **Move `www` back to GitHub.** The `www` host is currently proxied through Cloudflare with a
  redirect rule because GitHub issued its certificate for the apex only. Once the site no longer
  needs to be guaranteed stable (there is an external verification of the domain in progress),
  undo this: delete the "www to apex" redirect rule in Cloudflare, switch the `www` record back
  to DNS only, then remove and re-add the custom domain in GitHub Pages settings so it issues a
  fresh certificate covering both names. Expect up to an hour where `https://taiuto.co.uk` shows
  a certificate warning while GitHub re-issues. Verify with
  `openssl s_client -servername taiuto.co.uk -connect taiuto.co.uk:443 | openssl x509 -noout -ext subjectAltName`
  and check both names are listed.
