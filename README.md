# security-llm-leaderboard

The public leaderboard for **Security LLM Evals** — which LLM is best at each security task,
measured on publicly available benchmarks across accuracy, cost, and reliability. Live at
[secllmleaderboard.dev](https://secllmleaderboard.dev).

A fully static site with **no build step, no dependencies, and no secrets**: one HTML file
rendering the `rankings.json` produced by
[security-llm-eval-harness](https://github.com/OpenSource-Security-Stack/security-llm-eval-harness).

Currently: **4 domains, 7 benchmarks, 6 models** — threat intelligence, malware analysis,
detection engineering, and vulnerability management.

## Setup

```bash
git clone https://github.com/OpenSource-Security-Stack/security-llm-leaderboard.git
cd security-llm-leaderboard

open index.html                  # works straight from disk — or serve it:
python3 -m http.server 8000      # http://localhost:8000
```

To refresh the data from new eval runs:

```bash
# in the harness repo:
python3 scripts/export.py
cp rankings.js ../security-llm-leaderboard/data/rankings.js
```

Deploys on any static host (GitHub Pages, Vercel, Netlify) — no configuration needed.

## Contributing

The site is intentionally simple: `index.html` (markup, styles, rendering) + `data/rankings.js`
(the data). UI improvements are welcome as PRs. Two rules:

- **Data comes only from the harness** — never hand-edit `data/rankings.js`; scores, models,
  and benchmarks change upstream.
- **No external requests** — the site stays self-contained (no CDNs, no analytics, no fonts).

For new benchmarks or models, contribute to the
[eval harness](https://github.com/OpenSource-Security-Stack/security-llm-eval-harness) instead —
the leaderboard picks them up automatically from the data.

## License

MIT — see [LICENSE](LICENSE). Benchmark data belongs to its original authors — see the
Benchmarks & Credits page on the site.
