# worldcup-analysis

World Cup match analysis workspace — integrates three independent football prediction toolkits (MonteCarlo, ScoutTactical, StatsMarkets) to produce structured match reports. Three analysts generate independent reports and a final consensus is derived through cross-debate.

## Overview

This repository contains three complementary analysis toolsets:

- `2026-world-cup-predictor`: Quantitative models and simulation scripts based on Elo, Poisson and Monte Carlo.
- `ScoutFootball_for_World_Cup`: Scout/tactical models, squad data, and a tactical whiteboard frontend.
- `Football-2026`: Market/odds-focused quantitative engine and Chrome extension (de-margin, Kelly, odds-movement detection).

The goal is to merge independent analyst conclusions into reproducible, source-attributed match reports for strategy and investment reference.

## Repository Layout (short)

- `2026-world-cup-predictor/` — Model code, simulation scripts and data.
- `ScoutFootball_for_World_Cup/` — Scout models, squad data and frontend tactical tools.
- `Football-2026/` — Chrome extension and JS-based quant engine.
- `reports/` — Independent analyst reports and consolidated match analyses.
- `ANALYSIS_CHECKLIST.md` — Pre-flight checklist (Elo verification, squad validation, odds sources, etc.).

See subproject `README.md` files for detailed instructions.

## Quickstart (example)

Prerequisites: Python 3.8+ and Node.js if you will run frontend or extension-related scripts.

```bash
git clone https://github.com/1561040647/worldcup-analysis.git
cd worldcup-analysis
```

Python example (2026-world-cup-predictor):

```bash
python -m venv .venv
source .venv/bin/activate  # Windows PowerShell: .\.venv\Scripts\Activate.ps1
pip install -r 2026-world-cup-predictor/requirements.txt
cd 2026-world-cup-predictor
python scripts/report.py --match "TeamA vs TeamB"
```

## Notes

- Always read `ANALYSIS_CHECKLIST.md` and `CLAUDE.md` for mandatory validation steps before producing reports.
- Use the provided ingestion scripts to refresh local data caches.

## Contributing

Contributions welcome: open issues, PRs, or add new reports under `reports/`. Follow the data validation and reporting rules in `CLAUDE.md` before submitting.

## License

Check each subproject for its LICENSE file; some submodules may carry separate licensing terms.
