# Best Public DNS

A zero-build web app that helps identify the best public DNS resolver for the visitor's current network. It sends real DNS-over-HTTPS (DoH) queries from the browser and ranks 33 resolvers by speed, privacy, malware filtering, family filtering, or ad/tracker blocking.

## Features

**Benchmarking**
- Tests 33 public resolvers: Cloudflare, Google, Quad9, AdGuard, NextDNS, Control D, DNS4EU, LibreDNS, DNS.WATCH, UncensoredDNS, Digitale Gesellschaft, DNS0.eu, Mullvad, CleanBrowsing, Comodo, OpenDNS, Yandex, Hurricane Electric, CIRA Canadian Shield, Alibaba, DNSPod
- Measures cached and uncached lookup latency with median timing across multiple rounds
- Configurable query type (A, AAAA, HTTPS, TXT, MX, NS, CNAME, CAA), rounds (1–15), and timeout (2/5/10 s)
- Parallel or sequential test modes, plus randomize-order option to reduce bias
- Per-round timing bars, min/median/max, standard deviation, and jitter per resolver
- Failure tracking with failed resolvers ranked last
- Live progress bar, per-resolver status, and a cancel button
- Re-test any single resolver without re-running the whole benchmark
- Add your own custom DoH resolver to the list
- Add custom test domains

**Ranking**
- Rank presets: Fastest, Balanced, Privacy, Malware protection, Family filtering, Ad & tracker blocking
- Custom ranking with seven weight sliders (speed, privacy, security, family, ads, reliability, DNSSEC)
- Weighted score breakdown shown per resolver
- Winner-by-metric chips: fastest cached, fastest uncached, best privacy/security/family/ads, most reliable
- Sortable table columns and text search/filter

**Analysis**
- DNSSEC validation probe per resolver (`dnssec-failed.org` SERVFAIL test)
- Minimum TTL observed per resolver
- Run history (last 20 runs, stored locally) with a canvas chart comparing the current run against the previous one
- Per-resolver deltas versus the previous run
- Client network info: your public IP as seen by Google's resolver

**Sharing & export**
- Export results as CSV or JSON
- Copy results as a Markdown table
- Shareable settings link (all options encoded in the URL hash)
- Settings, custom resolvers, and history persist in localStorage

**Setup help**
- Per-resolver setup guide dialog with step-by-step instructions for Windows, macOS, Linux, iOS, Android, and routers
- One-click copy for IP address, DoH URL, and DNS-over-TLS/Android Private DNS hostname

**Interface**
- Dark and light themes (persisted), print-friendly stylesheet
- Keyboard shortcuts: Ctrl/Cmd+Enter to run, `/` to search, Esc to close dialogs
- Optional completion sound, ARIA live status, and progress role
- Runs entirely in the browser: no accounts, analytics, or backend
- Deploys automatically to GitHub Pages

## Run locally

```bash
python3 -m http.server 8000
```

Open http://localhost:8000.

## Method

The app builds DNS queries and submits them to resolver DNS-over-HTTPS endpoints using the GET form of DoH. Common domains approximate cached lookup performance. Random subdomains under `example.com` encourage a recursive lookup. Results measure browser DoH latency, not necessarily ordinary UDP or TCP DNS latency.

DNSSEC validation is probed by querying `dnssec-failed.org`, a deliberately mis-signed domain: validating resolvers answer SERVFAIL, non-validating resolvers return a record. A failed probe is reported as unknown.

## Limitations

Performance changes with your network, ISP, routing, location, and time of day. Browser CORS policies or network controls may cause a resolver to fail. Privacy, security, family, and ad-blocking values are editable heuristics in `index.html`, not measured or legal assessments.

## Deployment

The included GitHub Actions workflow deploys each `main` push to GitHub Pages. In **Settings → Pages**, select **GitHub Actions** as the source.

Expected URL: `https://jherney.github.io/best-public-dns/`

## License

MIT
