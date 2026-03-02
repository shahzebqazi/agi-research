# Playbook — AI Research & Testing Toolkit

Step-by-step guide for running the dev environment and deploying documentation.

---

## 1. Prerequisites

- **Git** — [Install](https://git-scm.com/downloads)
- **Python 3.10+** — [python.org](https://www.python.org/downloads/)
- **Docker & Docker Compose** — [Docker Desktop](https://docs.docker.com/get-docker/) or [Compose install](https://docs.docker.com/compose/install/)

---

## 2. Clone and Branch

```bash
git clone https://github.com/shahzebqazi/agi-research.git
cd agi-research
git checkout research
```

---

## 3. Virtual Environment (venv)

Create and activate the venv:

**macOS / Linux:**
```bash
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

**Windows (PowerShell):**
```powershell
python -m venv venv
.\venv\Scripts\Activate.ps1
pip install -r requirements.txt
```

Verify:
```bash
python -c "import sys; print(sys.prefix)"
# Should print path ending in .../agi-research/venv
```

---

## 4. Docker Compose

From the repo root:

```bash
# Build and run the app service (profile: full)
docker compose --profile full up --build

# Run in background
docker compose --profile full up -d --build

# Stop
docker compose --profile full down
```

Optional: run Ollama locally for LFM2 inference — uncomment the `ollama` service and `volumes` in `docker-compose.yml`, then:

```bash
docker compose --profile ollama up -d
# API at http://localhost:11434 — see https://docs.ollama.com/api
```

---

## 5. Environment Variables

```bash
cp .env.example .env
# Edit .env: set GITHUB_EMAIL, GITHUB_TOKEN, and any API keys (OpenAI, Anthropic, etc.)
```

Never commit `.env`. It is listed in `.gitignore`.

---

## 6. Deploy Documentation to GitHub Pages

### Option A: Docs from `main` (default branch)

1. Push `research` to GitHub and merge to `main` (or make `main` the docs source).
2. **GitHub repo** → **Settings** → **Pages**.
3. **Source:** Deploy from a branch.
4. **Branch:** `main` (or `research`) → `/ (root)` or `/docs` if you use a `docs` folder.
5. Save. Site will be at `https://shahzebqazi.github.io/agi-research/`.

### Option B: Use GitHub Actions (e.g. Jekyll / MkDocs)

1. Add a workflow under `.github/workflows/` that builds the site and deploys to `gh-pages`.
2. In **Settings → Pages**, set source to **GitHub Actions**.

### Option C: Static export from `research`

```bash
git checkout research
git push origin research
# Then in Settings → Pages choose branch: research, folder: / (root)
```

---

## 7. Quick Reference

| Task              | Command |
|-------------------|--------|
| Activate venv     | `source venv/bin/activate` (Unix) or `.\venv\Scripts\Activate.ps1` (Windows) |
| Run Docker stack  | `docker compose --profile full up --build` |
| Run tests (future)| `pytest` or `python -m pytest` (when added) |
| Lint (future)     | `ruff check .` / `black .` (when added) |

---

## 8. Verified Reference Links

- **Hugging Face:** [Transformers](https://huggingface.co/docs/transformers) · [Accelerate](https://huggingface.co/docs/accelerate) · [PEFT](https://huggingface.co/docs/peft) · [smolagents](https://huggingface.co/docs/smolagents)
- **Ollama:** [API](https://docs.ollama.com/api) · [LFM2 model](https://ollama.com/library/lfm2)
- **OpenAI:** [API](https://platform.openai.com/docs) · [MCP](https://developers.openai.com/codex/mcp)
- **Anthropic:** [API & SDKs](https://docs.anthropic.com/en/api/client-sdks)
- **DeepSeek:** [API](https://api-docs.deepseek.com/) · [DeepSeek-MoE](https://github.com/deepseek-ai/DeepSeek-MoE)
- **Kaggle:** [Kaggle API](https://github.com/Kaggle/kaggle-api) · [User docs](https://github.com/Kaggle/kaggle-api/blob/main/docs/README.md)
