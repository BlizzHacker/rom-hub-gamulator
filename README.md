# Gamulator provider for ROM Hub / ROMarr

**Status: not installable. The site is down. This repository is documentation
and a catalogue entry.**

| Capability | Status |
|---|---|
| `search` | **Unavailable — there is no origin server to talk to** |
| `importer` | Unavailable, same reason |
| `stream` | Unavailable, same reason |

## The finding

Gamulator did not fail a parse, a challenge or an authentication check. It
failed DNS.

**The apex does not resolve at all.** `gamulator.com` returns NXDOMAIN — no
address record of any kind:

```
$ nslookup gamulator.com 8.8.8.8
Name:    gamulator.com
(no addresses)
```

**The `www` host resolves, but only as far as Cloudflare.**
`www.gamulator.com` points at 104.26.8.39, 104.26.9.39 and 172.67.68.38 — all
Cloudflare edge addresses — and every path returns:

```
HTTP/1.1 530
error code: 1016
```

Cloudflare's **1016 is "Origin DNS error"**: the edge still has a
configuration for the hostname, but the DNS record it is supposed to proxy to
no longer resolves to anything. In other words the front door is still
standing and there is no building behind it.

Checked on `/`, `/roms` and `/robots.txt` — 530 on all three, on 2026-08-12.

## What this means

There is nothing to survey and nothing to index. This is not a site that is
hard to read, or that refuses bots, or that stopped hosting files while
keeping its catalogue — it is a hostname whose origin is gone.

**Recommendation: drop Gamulator from the target list.**

If it ever returns, the work is a straightforward clone of
`romarr-plugin-retrostic`, which is the reference provider for this family —
but the survey has to start from scratch, because nothing about the site's
structure was observable and this repository guesses at none of it.

## Terms

Nothing here fetches, indexes or redistributes anything. This repository
records a finding.

## License

MIT — see `LICENSE`.
