# Project Management — Critical Path & Licensing

## Critical Path

```
main (stable)
  │
  ├── research ───────► PLAYBOOK, PM_DOC, PRD, RESEARCH_DOC, Ref-Agent links
  │       │
  │       ├── development ─► Feature branches, PRs into research/main
  │       │
  │       ├── training ───► Model training scripts, LFM2/MoE experiments
  │       │
  │       └── benchmarking ─► Evaluation suites, Kaggle/benchmark runs
  │
  └── Releases: merge research → main after QA
```

**Dependencies:** Docker + venv (PLAYBOOK) → Research onboarding → PRD alignment → Implementation (development/training/benchmarking).

---

## Research Onboarding

1. **Clone & branch:** `git clone ... && git checkout research`
2. **Environment:** Follow [PLAYBOOK.md](PLAYBOOK.md) (venv, `docker compose`, `.env`)
3. **Read:** [README.md](README.md), [PRD.md](PRD.md), [RESEARCH_DOC.md](RESEARCH_DOC.md)
4. **Ref-Agent:** Verify any new doc/repo links before adding; use [PLAYBOOK.md](PLAYBOOK.md) §8 as the canonical list
5. **Commits:** Use conventional messages; PR into `research` (or `development` for features)

---

## Open Source Licensing Strategy

- **License:** [Apache 2.0](https://www.apache.org/licenses/LICENSE-2.0)
- **Rationale:** Permissive, patent grant, compatible with Hugging Face / Ollama / Kaggle and commercial use.
- **Repo:** Include `LICENSE` at repo root with full Apache 2.0 text.
- **Headers:** Optional “SPDX-License-Identifier: Apache-2.0” in source files.
- **Third-party:** Document dependencies and their licenses in `requirements.txt` / `docs/THIRD_PARTY.md`; ensure no GPL-only code is linked if keeping Apache 2.0.

---

## Agent Roles (Swarm)

| Role         | Responsibility              | Branch focus    |
|-------------|-----------------------------|-----------------|
| Architect   | Repo structure, PRD        | main, research  |
| Researcher  | Links, RESEARCH_DOC        | research        |
| DevOps      | Docker, venv, PLAYBOOK     | research        |
| QA/Validator| Link checks, license audit | All             |
