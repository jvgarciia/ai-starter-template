# Stage 01 — [Stage Name] (Layer 2)

Replace the title and all bracketed sections with the specifics of your stage.

---

## Purpose

[One sentence describing what this stage does and why it exists in the workflow.
Write this so that someone who has never seen the project understands the stage's job.]

---

## Inputs

What this stage reads before starting work:

| Source | File or location | Description |
|--------|-----------------|-------------|
| Layer 1 | `../../CONTEXT.md` | Workspace routing — already read |
| Layer 2 | This file | Stage contract — already read |
| Layer 3 | `references/[filename]` | [What rule or reference material to load] |
| Layer 4 | [Path to input file, or "none — this is the first stage"] | [What the input contains] |

**Note on Layer 3 vs Layer 4:**
- Layer 3 (`references/`) = stable rules, schemas, style guides. Load these but do not edit them.
- Layer 4 (`output/`) = per-run artifacts. This is the working material for this specific run.

---

## Reference Context

Load the following reference files from `references/` before starting:

- [ ] `references/[filename.md]` — [why this reference is needed for this stage]

If no reference files are needed for this stage, write "None" and remove the checklist.

---

## Tools Allowed

List any tools or capabilities this stage may use:
- [File read — specify which files]
- [File write — specify which output file]
- [Any other tools or capabilities]

If the stage should only read and write text files (no code execution, no API calls), state that explicitly.

---

## Process

Step-by-step instructions for what the agent should do:

1. [First step — what to read, assess, or understand]
2. [Second step — what to do with that information]
3. [Continue as needed — keep steps concrete and actionable]
4. Write output to `output/[filename.md]` following the output schema below.

---

## Output Schema

What this stage must produce. Be specific about format and required fields.

**File:** `output/[filename.md]`

**Format:** [Markdown / JSON / plain text]

**Required sections / fields:**
```
[List what the output file must contain.
For JSON, list required keys and types.
For Markdown, list required headings.
For plain text, describe the expected structure.]
```

**Validation:** Before handing off, confirm:
- [ ] Output file exists at `output/[filename]`
- [ ] All required sections are present
- [ ] [Any other quality check specific to this stage]

---

## Failure Conditions

Stop and ask for human input if:
- The input file is missing or empty
- The input does not match the expected format
- You cannot complete the process without making an assumption that a human should make
- [Any other condition specific to this stage where autonomous action would be risky]

---

## Human Review Gate

**This stage ends when the output file is written.**

A human must review `output/[filename]` before Stage 02 begins.

The human will check:
- [What specifically a human should verify in this output]
- [What "good" looks like for this stage's output]
- [What would cause rejection and require the stage to re-run]

**Do not proceed to Stage 02 until the human has approved this stage's output.**
