# Workflow Context (Layer 1)

This file is the routing layer for this staged workflow. Read it first to orient yourself,
then navigate to the specific stage you have been asked to run.

---

## What This Workflow Does

[Replace this with a one-paragraph description of what this workflow accomplishes, what it
takes as input, and what it produces as final output.]

---

## Stages

| Stage | Folder | Purpose |
|-------|--------|---------|
| 1 | `stages/01-example-stage/` | [Brief description of what Stage 1 does] |
| 2 | `stages/02-example-stage/` | [Brief description of what Stage 2 does] |

---

## Navigation

To run a stage, read its `CONTEXT.md` file. Each stage contract tells you:
- What inputs it expects (and where to find them)
- What process to follow
- What output to produce

**Always read this file first, then the stage-specific CONTEXT.md. Never skip to a stage
without reading the workspace context.**

---

## Shared Reference Material

Stable rules, schemas, and guidelines that apply across all stages live in `references/`.
Individual stages will tell you which reference files to load. Do not load all reference
material at once — load only what each stage's contract specifies.

---

## Running Order

Stages must run in numeric order. Stage 2 depends on Stage 1's output. Do not begin a stage
until the previous stage's output has been reviewed and approved by a human.

---

## Output Location

Each stage writes its output to its own `output/` folder. Do not write a stage's output
anywhere else. Do not modify another stage's output folder.
