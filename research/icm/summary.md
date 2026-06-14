# Interpretable Context Methodology (ICM) — Practical Summary

**Paper title:** Interpretable Context Methodology: Folder Structure as Agent Architecture
**Author:** RinDig (contact: theceo@eduba.io) — full author information at arXiv
**arXiv:** 2603.16021v2 (submitted March 2026, v2)
**License:** arXiv non-exclusive distribution license — see https://info.arxiv.org/help/license/index.html
**GitHub:** https://github.com/RinDig/Interpretable-Context-Methodology-ICM-
**Paper location:** `research/icm/interpretable-context-methodology.pdf`

> **About this document:** This is our practical interpretation of the paper, written as
> learning material for this project. It is not a verbatim summary. We have applied judgment
> about what is most useful, included the paper's own stated limitations, and noted where
> claims should be treated as preliminary rather than proven.

---

## What ICM Is

ICM is a way to design AI agent workflows using folder structure and markdown files instead of
orchestration frameworks. The core idea: a folder of numbered subfolders is a pipeline. Each
subfolder is a stage. The AI reads a different set of context files at each stage and produces an
output. A human reviews that output before the next stage runs.

There is no special runtime, no framework to install, and no code beyond simple shell scripts.
The architecture lives in the filesystem.

---

## The Central Principle: Layered Context Loading

Every ICM workflow uses five context layers, loaded in order:

| Layer | File | Size (approx.) | What the agent learns |
|-------|------|----------------|----------------------|
| 0 | `CLAUDE.md` (global) | ~800 tokens | "Where am I? What are the rules?" |
| 1 | `CONTEXT.md` (workspace) | ~300 tokens | "What stages exist? Where do I go?" |
| 2 | `stages/NN/CONTEXT.md` | 200–500 tokens | "What do I do in this stage?" |
| 3 | `stages/NN/references/` | 500–2k tokens | "What rules apply? (stable across runs)" |
| 4 | `stages/NN/output/` | varies | "What am I working with right now? (per run)" |

**Why layers matter:** LLMs degrade when context is too long or unstructured — called "lost in
the middle" degradation. Layering means each stage loads only what is relevant to that stage, not
everything at once.

---

## Five Design Principles

**1. One stage, one job.**
Each stage has a single, clear purpose. If a stage needs "and" to describe what it does, split it.

**2. Plain text as the interface.**
Every input and output is Markdown or JSON. No binary formats, no databases, no SDK calls in
the context layer.

**3. Layered context loading.**
Load the minimum context needed for each stage. Reference material stays in `references/`.
Per-run artifacts go in `output/`. Never mix them.

**4. Every output is an edit surface.**
Intermediate outputs are files, not database rows. The human can open, inspect, and edit any
output before the next stage begins.

**5. Configure the factory, not the product.**
When a stage produces wrong output repeatedly, edit `CONTEXT.md` or `references/`. Editing the
output fixes one run. Editing the source fixes every future run.

---

## Stage Contracts

Each stage defines a contract in its `CONTEXT.md`. The contract specifies:

- **Purpose** — one sentence description of the stage's job
- **Inputs** — what files the stage reads (and from which layer)
- **Reference context** — stable rules, schemas, or style guides from `references/`
- **Process** — what the agent does
- **Output schema** — what the stage must produce
- **Verification** — checks the agent can run before handing off
- **Human review gate** — explicit note that a human must approve before Stage N+1 runs

---

## Human Review Gates

ICM treats human review as a first-class part of the workflow, not an afterthought. Between
every stage:

1. The previous stage's output is a readable file
2. A human opens it and checks it
3. The human edits it if needed
4. Only then does the next stage begin

This is the opposite of "autonomous agents" that chain stages together automatically. ICM
optimizes for correctability, not speed.

---

## Where ICM Works Well

- Content production pipelines (research → outline → draft → polish)
- Document processing workflows (extract → normalize → classify → report)
- Sequential analysis workflows where each step depends on the previous
- Any workflow where you want to inspect and approve intermediate outputs
- Repeatable processes where the same stages run many times

---

## Where ICM Does Not Work

- **Real-time collaboration between agents** — ICM is single-agent with human gates, not
  multi-agent
- **High-concurrency systems** — parallel branches require locking, state isolation, and queuing
  that ICM's filesystem approach does not provide
- **Complex automated branching** — decision logic that routes dynamically between many paths
  belongs in application code, not context files
- **Events and triggers** — ICM stages are manually invoked, not event-driven

For these use cases, application code, frameworks, or orchestration infrastructure are better tools.

---

## Evidence Limitations

The paper's claims should be read with these caveats in mind:

- Data came from a 52-person invite-only community — not a random sample
- Data collection was informal (practitioner conversations, not structured interviews)
- Practitioners who joined the community likely already believed in the approach (enthusiasm bias)
- Testing was concentrated in content production workflows
- All testing used a single model family (Claude Opus/Sonnet)
- No controlled comparison between ICM and monolithic prompting was conducted
- Reported improvements (token reduction, output quality) are self-reported, not independently measured

This does not mean ICM is wrong. It means the evidence is preliminary and field-tested, not
scientifically validated. Use it as a pattern to evaluate, not a proven methodology to follow
uncritically.

---

## The Hybrid Architecture Principle

ICM handles context, stage structure, and intermediate artifacts. Application code handles
everything else:

| ICM handles | Application code handles |
|-------------|------------------------|
| Context layering | API calls and retries |
| Stage contracts | State management |
| Intermediate file artifacts | Concurrency and parallelism |
| Human review gates | Authentication and authorization |
| Reference material organization | Deployment and infrastructure |
| Prompt structure | Error recovery and logging |

The two layers are complementary. ICM is not a replacement for engineering — it is a structure
for the AI reasoning layer that sits on top of your engineering layer.
