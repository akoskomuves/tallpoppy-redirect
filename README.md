# tallpoppy.xyz → tallpoppystudio.com

Path-preserving redirect for the old studio domain, served by GitHub Pages (DNS stays at GoDaddy).

- Every known studio path (e.g. `/notehunter/privacy/`) has a generated stub `index.html` that answers **HTTP 200** with a meta refresh, `rel=canonical` and `noindex` pointing at the same path on [tallpoppystudio.com](https://tallpoppystudio.com), plus a JS `location.replace` that keeps the query string and hash.
- `404.html` catches anything else and forwards it to the same path (canonical: the studio home).
- `google24ee0e2d9f547ea5.html` is a verbatim copy of the Search Console verification file, so the tallpoppy.xyz property stays verified.

When the studio site adds pages, regenerate the stubs:

```sh
python3 scripts/generate_stubs.py   # reads the live sitemap + ../akoskomuves.github.io
```

GitHub Pages can't send a real 301 on a custom domain. For that, move DNS to Cloudflare (Redirect Rule) or use GoDaddy forwarding with path preservation.
