# security-llm-leaderboard

The public leaderboard for the **Security Router** project — which LLM is best at each security
task, measured on real benchmarks. A static site with **no logic and no secrets**: it renders a
`rankings.json` produced by [security-llm-eval-harness](../security-llm-eval-harness).

Live domains: **Threat-Intel Reasoning** and **Malware Analysis** (CyberSOCEval). The **Coverage
map** view shows all 19 security domains, their target benchmarks, and status.

## Run it locally

It's a single static page. Because it loads `data/rankings.js` via a `<script>` tag, it works
straight from disk:

```bash
open index.html            # macOS — or just double-click
# or serve it:
python3 -m http.server 8000   # then visit http://localhost:8000
```

## Updating the data

Data lives in `data/rankings.js` (`window.RANKINGS`, conforming to the harness's
`spec/results.schema.json`). To refresh from new eval runs:

```bash
# in the harness repo:
python3 scripts/export_rankings.py
cp rankings.js ../security-llm-leaderboard/data/rankings.js
```

The site never contains model outputs, keys, or private scoring — only the published rankings.

## Deploy

Any static host (GitHub Pages, Vercel, Netlify). It's fully self-contained: one HTML file + one
data file, no build step, no external requests.

## License

MIT — see [LICENSE](LICENSE).
