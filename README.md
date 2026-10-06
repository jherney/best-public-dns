# Best Public DNS

A zero-build web app that helps identify the best public DNS resolver for the visitor's current network. It sends real DNS-over-HTTPS (DoH) queries from the browser and ranks resolvers by speed, privacy, malware filtering, family filtering, or ad/tracker blocking.

## Features

- Benchmarks Cloudflare, Google, Quad9, and AdGuard resolver variants
- Measures cached and uncached lookup latency
- Uses median timing across multiple rounds
- Tracks failed queries in the ranking
- Runs entirely in the browser, with no accounts, analytics, or backend
- Deploys automatically to GitHub Pages

## Run locally

```bash
python3 -m http.server 8000
```

Open http://localhost:8000.

## Method

The app builds DNS A-record queries and submits them to resolver DNS-over-HTTPS endpoints. Common domains approximate cached lookup performance. Random subdomains under `example.com` encourage a recursive lookup. Results measure browser DoH latency, not necessarily ordinary UDP or TCP DNS latency.

## Limitations

Performance changes with your network, ISP, routing, location, and time of day. Browser CORS policies or network controls may cause a resolver to fail. Privacy and filtering values are editable heuristics in `index.html`, not measured or legal assessments.

## Deployment

The included GitHub Actions workflow deploys each `main` push to GitHub Pages. In **Settings → Pages**, select **GitHub Actions** as the source.

Expected URL: `https://jherney.github.io/best-public-dns/`

## License

MIT
