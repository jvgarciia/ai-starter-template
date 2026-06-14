# Managing Runs

Each time you run this workflow with new input, you have a choice about how to manage the
output files. Two approaches work well depending on how often you run the workflow and whether
you need to keep a history.

---

## Option A — Overwrite in Place (Simple)

Run each stage and let its output overwrite the previous run's output. Use this when:
- You run the workflow infrequently
- You do not need to compare outputs across runs
- Simplicity matters more than history

For this approach, just delete the contents of each stage's `output/` folder before starting
a new run.

---

## Option B — Dated Run Folders (Persistent History)

Create a folder in `runs/` for each run. Copy the final outputs there after the workflow
completes. Use this when:
- You need to track how outputs change over time
- Multiple people may run the workflow and you want to compare results
- You are iterating on the workflow and want to measure improvement

**Naming convention:**
```
runs/
  2026-06-13/
    stage-01-output.md
    stage-02-output.md
  2026-06-20/
    stage-01-output.md
    stage-02-output.md
```

Use ISO date format (`YYYY-MM-DD`) so runs sort chronologically.

---

## Option C — Git History (No Extra Folders)

Commit each stage's output as you go. Git history becomes your run history. Use this when:
- The project is already in version control
- You want diffable output history without creating extra folders
- You commit after human review of each stage (before running the next)

For this approach, add `output/` to version control (remove any `.gitignore` rules that
exclude it) and commit with a message like:
```
Stage 01 output — run 2026-06-13
```

---

## Which to Choose

| Situation | Approach |
|-----------|---------|
| One-off use, no history needed | Option A |
| Frequent runs, need to compare | Option B |
| Already using git, want clean history | Option C |

There is no wrong choice. Pick the one that matches how you actually work and stick with it
consistently so outputs are predictable to find.
