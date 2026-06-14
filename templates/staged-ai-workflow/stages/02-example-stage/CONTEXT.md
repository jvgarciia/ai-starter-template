# Stage 02 — [Stage Name] (Layer 2)

Replace the title and all bracketed sections with the specifics of your stage.

---

## Purpose

[One sentence describing what this stage does. This stage typically transforms or builds
on the output produced by Stage 01.]

---

## Inputs

What this stage reads before starting work:

| Source | File or location | Description |
|--------|-----------------|-------------|
| Layer 1 | `../../CONTEXT.md` | Workspace routing — already read |
| Layer 2 | This file | Stage contract — already read |
| Layer 3 | `references/[filename]` | [What rule or reference material to load] |
| Layer 4 | `../01-example-stage/output/[filename]` | Approved output from Stage 01 |

**Important:** This stage depends on Stage 01's output. If Stage 01 has not been run and
its output has not been approved by a human, stop and notify the operator.

---

## Reference Context

Load the following reference files from `references/` before starting:

- [ ] `references/[filename.md]` — [why this reference is needed for this stage]

---

## Tools Allowed

- [File read — specify which files including Stage 01's output]
- [File write — specify which output file]
- [Any other tools or capabilities]

---

## Process

1. Read Stage 01's approved output from `../01-example-stage/output/[filename]`.
2. [Second step — what to do with Stage 01's output]
3. [Continue with stage-specific steps]
4. Write output to `output/[filename]` following the output schema below.

---

## Output Schema

**File:** `output/[filename.md]`

**Format:** [Markdown / JSON / plain text]

**Required sections / fields:**
```
[List what the output file must contain.
Be explicit. If a field or section is missing, the stage has not completed successfully.]
```

**Validation:** Before handing off, confirm:
- [ ] Output file exists at `output/[filename]`
- [ ] All required sections are present
- [ ] Output is consistent with the Stage 01 input (no contradictions or gaps)
- [ ] [Any other quality check specific to this stage]

---

## Failure Conditions

Stop and ask for human input if:
- Stage 01's output file is missing or has not been approved
- The Stage 01 output is inconsistent or incomplete in a way that makes this stage impossible
- [Any other condition where autonomous action would be risky]

---

## Human Review Gate

**This stage ends when the output file is written.**

A human must review `output/[filename]` before any subsequent stage begins.

The human will check:
- [What specifically a human should verify]
- [How this output connects back to the Stage 01 output]
- [What would cause rejection]

**Do not proceed to any subsequent stage until the human has approved this output.**
