# ICM Adoption Checklist

Use this checklist to decide whether a workflow is a good fit for Interpretable Context
Methodology (ICM). Answer each question honestly. Mismatches at the bottom of the list are not
dealbreakers — they are signals to design the ICM layer more carefully or to push certain
responsibilities into application code.

---

## Section 1 — Workflow Shape

**Is the workflow sequential?**
- [ ] Yes — each step depends on the output of the previous step
- [ ] No — steps run in parallel or can be triggered independently

If no, ICM adds structure without much benefit. Consider plain scripts or a task queue instead.

**Is the workflow repeatable?**
- [ ] Yes — the same stages run many times with different inputs
- [ ] No — this is a one-time process

If no, ICM's stage contract investment pays off less. A single well-structured prompt may be enough.

**Does each stage have a single clear job?**
- [ ] Yes — each stage can be described in one sentence without "and"
- [ ] No — stages blend multiple responsibilities

If no, decompose before building. ICM stages that do multiple things become hard to debug and
reuse.

---

## Section 2 — Human Oversight Needs

**Do intermediate outputs need human review before the next stage runs?**
- [ ] Yes — a human should inspect and approve before moving forward
- [ ] No — the workflow should run end-to-end automatically

ICM is built around human review gates. If you need full automation, ICM's manual stage
handoffs may be a bottleneck. Consider adding automated validation steps and removing human
gates for low-stakes decisions — but be aware this reduces ICM's main safety benefit.

**Do errors in one stage need to be catchable before they cascade?**
- [ ] Yes — a bad output early can corrupt everything downstream
- [ ] No — downstream stages can recover from upstream errors

If yes, ICM's inspectable intermediate files are a strong fit. Errors surface as readable files,
not hidden state.

**Is it important that non-technical team members can understand or edit the workflow's
outputs?**
- [ ] Yes — stakeholders may need to read or modify intermediate outputs
- [ ] No — outputs are internal or technical

If yes, ICM's plain-text-first approach (Markdown, JSON) is a strong advantage.

---

## Section 3 — Context Management

**Does each stage need different context than the other stages?**
- [ ] Yes — different stages need different reference material, rules, or schemas
- [ ] No — the same context applies throughout the entire workflow

If yes, ICM's layered context loading (Layers 2–4) directly solves this problem by giving
each stage its own `CONTEXT.md` and `references/` folder.

**Is the reference material stable (doesn't change run-to-run)?**
- [ ] Yes — rules, schemas, and guidelines stay the same across runs
- [ ] No — what "correct" means changes with each run

If no, the boundary between `references/` (stable) and `output/` (per-run) becomes unclear.
Plan for this explicitly before designing stage contracts.

**Is the total context per stage manageable (under ~5k tokens per stage)?**
- [ ] Yes — each stage reads a small, focused set of files
- [ ] No — stages need large amounts of context

If no, revisit whether stages are too broad. Large context loads are a signal to split the stage
or move material into application code.

---

## Section 4 — Technical Fit

**Can the workflow's inputs and outputs be represented as plain text or JSON?**
- [ ] Yes — text, structured data, Markdown documents
- [ ] No — binary data, images, audio, real-time streams, database records

If no, ICM's plain-text interface assumption breaks down. You may need an ICM layer alongside
application code that handles the non-text portions.

**Is the workflow timing-tolerant?**
- [ ] Yes — it's fine to pause between stages for review
- [ ] No — the workflow needs to complete quickly end-to-end

If no, human review gates will create unacceptable delays. Consider whether automated
validation checks can replace some or all human gates for time-sensitive steps.

**Is a single agent doing all the work (not multiple agents in parallel)?**
- [ ] Yes — one agent runs each stage in sequence
- [ ] No — multiple agents run simultaneously and share state

If no, ICM's filesystem-based approach does not handle concurrent write conflicts. Use a proper
orchestration layer or database for shared state in multi-agent scenarios.

---

## Reading the Results

**Strong ICM fit (most boxes checked):**
Sequential, repeatable, stage-specific context, human review needed, plain text outputs.
Build the full ICM structure from the template in `templates/staged-ai-workflow/`.

**Moderate fit (mixed answers):**
ICM works for the core workflow, but some stages need application code to handle the exceptions.
Design the ICM layer for the sequential reasoning parts. Wrap it with application code for
API calls, concurrency, state management, and edge cases.

**Poor fit (many unchecked boxes):**
Real-time, parallel, event-driven, or fully automated. Use application code and orchestration
frameworks (queues, state machines, workers). ICM's value comes from human review gates and
inspectable intermediates — if you're removing those, you're also removing most of the benefit.

---

## Before You Build

Answer these three questions before designing any stage:

1. What does this stage receive as input, and from which layer?
2. What exact file does this stage produce as output?
3. What would a human check before approving this output?

If you cannot answer all three for a given stage, the stage is not ready to build yet.
