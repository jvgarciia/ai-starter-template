# References (Layer 3)

This folder holds stable reference material that applies across multiple stages of this workflow.
Reference material is anything that stays the same from run to run: style guides, schemas,
rules, taxonomies, formatting standards.

---

## What Belongs Here

Put files here when:
- The content is the same across every run of the workflow
- Multiple stages need to refer to the same rules or standards
- You want to update a rule once and have it apply everywhere

Do NOT put here:
- Per-run inputs or working data (those go in each stage's `output/` folder)
- Stage-specific instructions (those go in each stage's `CONTEXT.md`)
- Raw source material for a specific run

---

## How Stages Use This Folder

Stage contracts (in each stage's `CONTEXT.md`) specify which reference files to load for
that stage. Load only what the stage contract specifies — do not load all reference files at once.

---

## Suggested File Types

| File name | What to put in it |
|-----------|------------------|
| `style-guide.md` | Tone of voice, formatting rules, vocabulary |
| `output-schema.json` | JSON schema for validating structured outputs |
| `taxonomy.md` | Categories, labels, or classification systems |
| `rules.md` | Constraints, requirements, or quality criteria |
| `examples.md` | Representative good examples of expected output |

---

## File Naming Convention

Use descriptive kebab-case names: `tone-guidelines.md`, `classification-rules.md`.
Avoid generic names like `notes.md` or `data.md`.
