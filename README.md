# Contract Risk Review — LLM Fine-Tuning + Agentic Reasoning

Fine-tuned LLM pipeline that flags risky clauses in vendor contracts (unlimited liability, auto-renewal, weak termination rights) and generates plain-English risk summaries — built to cut down the manual review bottleneck legal/compliance teams face.

## Problem

Legal and compliance teams manually review vendor contracts clause-by-clause to catch risky terms. This is slow, inconsistent across reviewers, and doesn't scale with contract volume.

## What this does

1. **Fine-tunes** a small open-source LLM (LLaMA-3-8B / Mistral-7B) using LoRA on [CUAD — Contract Understanding Atticus Dataset] to detect and classify risky clause types.
2. **Agentic pipeline** (LangChain/LangGraph) that runs: extract clauses → classify risk → generate plain-English summary → flag items for human review.
3. **RAG lookup** against a clause library using embeddings stored in a vector database (Weaviate/Chroma).
4. **Deployed demo** on Hugging Face Spaces.
5. **Guardrails**: bias/fairness checks on flagged clauses, explainability for why a clause was flagged, human-in-the-loop override.

## Architecture

```
Contract PDF/text
      │
      ▼
Clause extraction ──► Risk classification (fine-tuned LLM)
      │                        │
      ▼                        ▼
RAG lookup vs.          Plain-English risk summary
clause library                 │
                                ▼
                    Flag for human review (if low-confidence
                    or high-risk category)
```

## Tech stack

- **Model**: [LLaMA-3-8B / Mistral-7B] + LoRA fine-tuning
- **Agent framework**: LangChain / LangGraph
- **Vector store**: Weaviate / Chroma (free tier)
- **Deployment**: Hugging Face Spaces
- **Dataset**: CUAD (Contract Understanding Atticus Dataset)

## Setup

```bash
git clone [repo-url]
cd contract-risk-review
pip install -r requirements.txt
```

Set environment variables (`.env`):
```
HF_TOKEN=your_huggingface_token
VECTOR_DB_API_KEY=your_key
```

Run the notebook:
```bash
jupyter notebook contract_risk_review.ipynb
```

## Results

| Metric | Value |
|---|---|
| Risky-clause detection precision | [ ] |
| Risky-clause detection recall | [ ] |
| Avg. inference latency per contract | [ ] |
| Estimated reviewer time saved | [ ]% |

## Guardrails & limitations

- Bias/fairness checks run on flagged-clause distribution across contract types.
- Explainability layer surfaces the specific clause text and reasoning behind each flag.
- All high-risk and low-confidence flags route to human review — this system assists review, it does not replace legal judgment.
- Fine-tuned on public contract data; performance on highly specialized or jurisdiction-specific contracts is not validated.

## Demo

[Hugging Face Spaces link]

## License

MIT
