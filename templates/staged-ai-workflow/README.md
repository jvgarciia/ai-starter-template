# Staged AI Workflow Template

A reusable template for building sequential, inspectable AI workflows using the Interpretable
Context Methodology (ICM) pattern. Copy this folder into any project and adapt it to the
specific workflow you are building.

---

## What This Template Is For

Use this structure when a task has multiple sequential steps and you want a human to review and
approve the output of each step before moving to the next one.

Good fits:
- Research → Outline → Draft → Polish pipelines
- Document processing workflows (extract → clean → analyze → report)
- Any process you run repeatedly with different inputs

Poor fits:
- Real-time workflows where steps must chain automatically with no human delay
- Parallel multi-agent tasks where agents share and modify state concurrently
- Event-driven systems that respond to triggers

Before starting, use the checklist at `research/icm/adoption-checklist.md` to evaluate fit.

---

## Folder Structure

```
staged-ai-workflow/
├── README.md              ← you are here — overview and usage instructions
├── CONTEXT.md             ← workspace routing (Layer 1): list of stages and navigation
├── references/
│   └── README.md          ← stable reference material shared across all stages
├── stages/
│   ├── 01-example-stage/
│   │   ├── CONTEXT.md     ← stage contract: inputs, process, output schema
│   │   ├── schemas/       ← JSON schemas for validating stage output
│   │   └── output/        ← per-run artifacts produced by this stage
│   └── 02-example-stage/
│       ├── CONTEXT.md
│       ├── schemas/
│       └── output/
└── runs/
    └── README.md          ← instructions for managing per-run working copies
```

---

## How to Run a Workflow

Each stage is run manually, in order. The workflow pauses between stages for human review.

**Step 1 — Give the agent its starting context**

Tell the agent:
```
Read CONTEXT.md, then read stages/01-example-stage/CONTEXT.md.
Follow the process defined there.
Write your output to stages/01-example-stage/output/.
```

**Step 2 — Review the output**

Open the output file. Read it. Edit it if needed. Only proceed when you are satisfied.

**Step 3 — Run the next stage**

Tell the agent:
```
Read CONTEXT.md, then read stages/02-example-stage/CONTEXT.md.
The input for this stage is in stages/01-example-stage/output/.
Follow the process and write output to stages/02-example-stage/output/.
```

Repeat for each stage.

---

## Adapting This Template

To use this for a real workflow:

1. Rename `01-example-stage/` and `02-example-stage/` to match your actual stages
   (e.g., `01-research/`, `02-outline/`, `03-draft/`)
2. Edit `CONTEXT.md` to list your actual stage names and brief descriptions
3. Edit each stage's `CONTEXT.md` to define the real contract for that stage
4. Add real JSON schemas to `schemas/` if you need structured output validation
5. Add stable reference material (style guides, rules, schemas) to `references/`
6. Clear `output/` folders between runs, or use the `runs/` pattern (see `runs/README.md`)

---

## Hybrid Architecture: ICM + Application Code

ICM structures the AI reasoning layer. Your application code handles everything else.

| ICM layer (this template) | Application code |
|--------------------------|-----------------|
| Stage contracts and context | API calls and retries |
| Intermediate file artifacts | State persistence (database) |
| Human review gates | Authentication and authorization |
| Reference material organization | Concurrency and parallelism |
| Prompt structure and layering | Deployment and infrastructure |

**The division of responsibility:**
- If a step involves language understanding, reasoning, or judgment → ICM stage
- If a step involves calling an API, writing to a database, or running code → application code

Mechanical transformations (formatting, sorting, deduplication) should use deterministic code,
not AI. AI is expensive and non-deterministic. Use it where it is irreplaceable.

---

## The Edit-Source Principle

When a stage produces wrong output repeatedly, do not just fix the output file.
Fix the source — the stage's `CONTEXT.md` or its `references/` material.

- Editing output fixes one run.
- Editing the source fixes every future run.

This is the most important operational principle in ICM. A workflow's quality over time is
determined by how well you maintain its context files, not how many times you correct its outputs.

---

## Further Reading

- `research/icm/summary.md` — what ICM is and how it works
- `research/icm/adoption-checklist.md` — whether this pattern fits your workflow
- Original paper: `research/icm/interpretable-context-methodology.pdf`
