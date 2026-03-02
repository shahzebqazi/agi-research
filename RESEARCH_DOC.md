# Research Document — Liquid FMs, MoE, and Agent Memory

*Academic-style review for the AI Research & Testing Toolkit.*

---

## 1. Liquid Foundation Models (LFM2)

**LFM2** (Liquid Foundation Model) is a family of efficient foundation models optimized for **on-device and edge** deployment via hardware-in-the-loop architecture search [1]. The backbone combines **gated short convolutions** with **grouped query attention (GQA)** blocks, improving prefill and decode speed (e.g. up to ~2× on CPU vs comparable dense models) while keeping a small memory footprint.

Key references:

- **Technical report:** [LFM2 Technical Report (arXiv:2511.23404)](https://arxiv.org/abs/2511.23404)
- **LFM2-8B-A1B (MoE):** [Liquid AI blog — Efficient On-device MoE](https://www.liquid.ai/blog/lfm2-8b-a1b-an-efficient-on-device-mixture-of-experts)
- **LFM2-24B-A2B:** [Scaling Up the LFM2 Architecture](https://www.liquid.ai/blog/lfm2-24b-a2b)
- **Hugging Face:** [Lfm2Moe in Transformers](https://huggingface.co/docs/transformers/model_doc/lfm2_moe)

“Liquid” state transitions here refer to efficient, adaptive computation and state flow across layers and experts, rather than a fixed dense forward pass—enabling better performance/size tradeoffs for edge deployment.

---

## 2. MoE Scaling Laws

**Mixture-of-Experts (MoE)** models scale total parameters while keeping **active** parameters per token low (e.g. LFM2-8B-A1B: ~8.3B total, ~1.5B active; LFM2-24B-A2B: ~24B total, ~2.3B active). Benefits:

- **Compute efficiency:** Quality comparable to larger dense models with a fraction of the compute per token.
- **Scaling laws:** Quality gains scale with total parameters and expert capacity; routing and load balancing are critical (e.g. [DeepSeek-MoE](https://github.com/deepseek-ai/DeepSeek-MoE)).

LFM2 uses tempered, decoupled Top-K knowledge distillation; curriculum learning; and a three-stage post-training recipe (SFT, length-normalized preference optimization, model merging). These practices inform how we design training and benchmarking branches (e.g. distillation, preference data, eval suites).

---

## 3. Perpetual Agent Memory

“Perpetual agent memory” here denotes **long-lived, updatable context** for agents across sessions or tasks:

- **External memory:** Vector stores, caches, or stateful APIs that persist across turns.
- **Context refresh:** Summarization, pruning, or chunked retrieval so that context stays within model limits while retaining important history.
- **MCP (Model Context Protocol):** [Specification](https://spec.modelcontextprotocol.io/specification/2025-03-26/) and [OpenAI MCP](https://developers.openai.com/codex/mcp) enable standardized tools and context injection—relevant for swarm tool use and memory interfaces.

Combined with LFM2-style efficiency, this suggests an architecture where agents use bounded active context plus refreshable external state, rather than unbounded in-memory history.

---

## 4. Synthesis for the Toolkit

| Topic              | Implication for toolkit                                      |
|--------------------|--------------------------------------------------------------|
| LFM2 efficiency    | Prefer edge-compatible stacks (Ollama, small MoE), document in PLAYBOOK. |
| MoE scaling        | Training/benchmarking branches should support MoE evals and scaling experiments. |
| Agent memory       | PRD goals (infinite context scaling, context refresh) and MCP integration. |
| Ref-Agent          | Verified links in PLAYBOOK and RESEARCH_DOC; no broken URLs. |

---

## References

[1] LFM2 Technical Report. arXiv:2511.23404.  
[2] Liquid AI. LFM2-8B-A1B and LFM2-24B-A2B blog posts. https://www.liquid.ai/blog  
[3] Hugging Face. Transformers (Lfm2Moe), Accelerate, PEFT, smolagents. https://huggingface.co/docs  
[4] Model Context Protocol. https://spec.modelcontextprotocol.io/  
[5] DeepSeek-MoE. https://github.com/deepseek-ai/DeepSeek-MoE  
