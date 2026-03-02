# Product Requirements — Harnessed Agent Swarm

## Vision

A **Harnessed Agent Swarm** for high-performance AI research and testing: multiple specialized agents (Architect, Researcher, DevOps, QA) operating with shared context, infinite-scale context handling, multi-modal support, and HCI/UX guardrails—aligned with LFM2 efficiency and edge compatibility.

---

## Goals

### 1. Infinite Context Scaling & Context Refreshing

- **Infinite context scaling:** Support long contexts (e.g. 32K+; extend toward 128K+) with efficient attention or state management (e.g. sliding window, summarization, chunking).
- **Context refreshing:** Mechanisms to update, compress, or replace context without full recompute; reference LFM2’s efficient state and hardware-in-the-loop design where applicable.
- **Non-goal:** Requiring unbounded context in a single call; bounded but large context with refresh is acceptable.

### 2. Multi-Modal Support

| Modality   | Scope                                      |
|-----------|---------------------------------------------|
| **Vision**| Image inputs for VLMs; optional local (e.g. Ollama LFM2) or cloud APIs. |
| **Reasoning** | Chain-of-thought, plan-and-execute, tool use (MCP, SDKs). |
| **Coding**| Code generation, execution sandbox, dataset/benchmark scripting (e.g. Kaggle, custom evals). |

Integration points: [OpenAI API](https://platform.openai.com/docs), [Anthropic](https://docs.anthropic.com/en/api/getting-started), [Ollama](https://docs.ollama.com/api), [DeepSeek](https://api-docs.deepseek.com/).

### 3. HCI/UX for AI Guardrails

- **Human-in-the-loop:** Clear handoff points (e.g. approvals, confirmations) for sensitive or irreversible actions.
- **Transparency:** Logs, trace IDs, and optional explanations for agent decisions.
- **Safety defaults:** Rate limits, sandboxing, and configurable guardrails (e.g. PII filters, content policy).
- **UX:** CLI and/or minimal UI for runs, config, and inspection; documentation first (PLAYBOOK, README).

---

## Out of Scope (Initial 2 Months)

- Full production deployment and SLAs
- Custom model training (beyond scripting on `training` branch)
- Legal/compliance certification

---

## Success Criteria

- PLAYBOOK executable (venv + Docker + GitHub Pages).
- Ref-Agent link list verified and documented.
- PRD and RESEARCH_DOC published; Apache 2.0 in place.
- Clear path to add first “swarm” workflow (e.g. research → validate → commit).
