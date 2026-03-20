# Qlik Sense on Windows — LLM Integration Patterns

Qlik Cloud delivers AI-assisted analytics natively — Insight Advisor, natural language queries, and AI-generated summaries are available out of the box.

Organizations running **Qlik Sense Enterprise on Windows** follow a different release cycle and do not have access to these cloud-native AI features by default.

This does not mean AI integration is impossible. It means it requires architecture.

This repository documents three patterns to integrate language models into a Qlik Sense on-premises deployment. Each pattern addresses a different business problem and is compatible with any OpenAI-compatible LLM — local (LM Studio, Ollama) or remote (OpenAI, Anthropic, Azure OpenAI).

> **These are reference architectures, not a code library.** The goal is to show that these integrations are possible and production-tested. How you implement them is up to you.

---

## Why on-premises?

Many organizations in regulated industries — financial services, healthcare, energy — cannot or choose not to send business data to a public cloud API. Running the LLM on-premises (or in a private cloud) keeps data within the organization's boundary.

These patterns were designed with that constraint in mind.

---

## Three integration patterns

| # | Pattern | What it enables | Integration point |
|---|---------|----------------|-------------------|
| 1 | [AI Assistant on Dashboards](docs/pattern-1-extension-proxy.md) | Ask questions about chart data in natural language | Qlik visualization extension |
| 2 | [LLM in Qlik Expressions](docs/pattern-2-sse-expressions.md) | Use LLM output in load scripts and expressions | Qlik Server-Side Extension (SSE) |
| 3 | [Ask Your Documents](docs/pattern-3-rag-documents.md) | Query internal PDF documents using natural language | Standalone RAG pipeline |

---

## High-level architecture

```mermaid
graph LR
    QS["Qlik Sense\nEnterprise on Windows"]

    QS -->|"Pattern 1 — Visualization Extension + Proxy"| P1["LLM API\n(local or remote)"]
    QS -->|"Pattern 2 — Server-Side Extension (gRPC)"| P2["LLM Server\n(OpenAI-compatible)"]
    QS -. "Pattern 3 — External Pipeline" .-> P3["RAG Pipeline\nPDFs → Vector DB → LLM"]
```

Patterns 1 and 2 integrate directly with Qlik Sense. Pattern 3 is a standalone pipeline that can feed results back into Qlik or operate independently.

---

## Screenshots

Screenshots of each pattern running in Qlik Sense are planned for a future update. See the [`screenshots/`](screenshots/) folder.

---

## Tested on

- Qlik Sense Enterprise on Windows
- LM Studio with local models (Llama, Mistral)
- Anthropic Claude API

---

## Author

Miguel A. Baeyens · [linkedin.com/in/mabaeyens](https://linkedin.com/in/mabaeyens)
