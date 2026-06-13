ScoutFootball_for_World_Cup — Detailed Installation & Run Guide

This document provides step-by-step installation and run instructions for `ScoutFootball_for_World_Cup` on Windows, macOS/Linux, and using Docker.

1) Local Python (recommended for development)

Windows (PowerShell):

```powershell
# create and activate venv
python -m venv .venv
.\.venv\Scripts\Activate.ps1

# upgrade pip and install deps
python -m pip install --upgrade pip
pip install -r requirements.txt

# if using uv (optional)
curl -LsSf https://astral.sh/uv/install.sh | sh
uv sync
```

macOS / Linux:

```bash
python3 -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
pip install -r requirements.txt
uv sync
```

2) One-command demo

```bash
bash scripts/demo.sh
```

This will validate data, run a short pipeline, and start the demo servers.

3) Manual pipeline (step-by-step)

```bash
# validate data
PYTHONPATH=src uv run python -m scoutfootball validate

# ingest and build features
PYTHONPATH=src uv run python -m scoutfootball ingest
PYTHONPATH=src uv run python -m scoutfootball build-features

# train ratings (may take long)
PYTHONPATH=src uv run python -m scoutfootball train

# optional: train supervised NN candidate
PYTHONPATH=src uv run python -m scoutfootball train-rating-nn
```

4) Start API + static frontend

```bash
# API (FastAPI)
PYTHONPATH=src uv run python -m scoutfootball serve --host 0.0.0.0 --port 8600

# static frontend
python3 -m http.server 8601 --directory frontend

# open http://localhost:8601
```

5) Docker (for reproducible runs)

```bash
# build image (from project root)
docker build -t scoutfootball:latest -f ScoutFootball_for_World_Cup/Dockerfile .

# run container, mounting local data for persistence
docker run --rm -p 8600:8600 -p 8601:8601 -v $(pwd)/ScoutFootball_for_World_Cup/data:/app/data scoutfootball:latest
```

6) Windows tips

- Run PowerShell as Administrator if you need to open firewall ports.
- Install `ffmpeg` and ensure it's in PATH for MP4 export of the tactical board.

7) Troubleshooting

- If `uv sync` fails, ensure `uv` is installed and in PATH.
- On first run, ingestion downloads public sources — allow network access.
- If tests or scripts fail due to missing data, run `PYTHONPATH=src uv run python -m scoutfootball ingest` to populate the cache.


If you want, I can also create a `docs/setup_windows.ps1` helper script to automate the Windows setup steps above.
