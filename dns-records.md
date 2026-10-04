# taiuto.co.uk DNS records

DNS is hosted on Cloudflare (free plan) since 4 October 2026. The name servers are
`beau.ns.cloudflare.com` and `ximena.ns.cloudflare.com`, set in the Tide domain panel.
Edit records at dash.cloudflare.com, not in the Tide panel.

Keep every record set to "DNS only" (grey cloud). The mail host must never be proxied, and
GitHub Pages needs a direct view of the apex records to issue and renew its certificate.

This list is the reference copy. Use it to verify the zone or recreate it at another DNS host.

| Type | Name | Value | Priority | Purpose |
|------|------|-------|----------|---------|
| A | @ | 185.199.108.153 | | GitHub Pages |
| A | @ | 185.199.109.153 | | GitHub Pages |
| A | @ | 185.199.110.153 | | GitHub Pages |
| A | @ | 185.199.111.153 | | GitHub Pages |
| CNAME | www | andybenedetti.github.io | | GitHub Pages |
| A | mail | 203.28.49.145 | | Mail host (Tide / Crazy Domains) |
| MX | @ | mail.taiuto.co.uk | 1 | Incoming mail |
| TXT | @ | v=spf1 +mx +a +ip4:122.201.124.79 ~all | | SPF |
| TXT | default._domainkey | see below | | DKIM |

DKIM value (one string, no spaces or line breaks):

```
v=DKIM1;k=rsa;p=MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEA3xgLGPHomjgLY7l9v1ArAfrzB1zSLPRSxNVVF2JibrIo0xd1sAdKH9LT+QsiGGiF+qdmR2g0NW/CmCGr/mFfOd1rW0zu7iHic8dfjzUI+dniJ8uMAGGexDzuAjqDQviCqY0YWoyFp/J/Y2p+B3fbUKcA9ZpapDM2p/mXtCyuKKW5zhUBSOpu0+vLlJ2mkIITVcV+5eVe8WvfnoYmRcvrMejoBVgseNU/gtkVzgHxW90B9kSPgXe9HKrpuPQhwuprMfeTrA6sdcXQk6iXdxEc0S6a5b2wpPlpmhsrKQHT5tswPXst0r5g4J6Xm+lDAJjnWk2hy2Tp+XIIXkeZuLdzzQIDAQAB;
```
