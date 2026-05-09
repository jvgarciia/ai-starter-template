# Project Context — AI Starter Template

This file is the memory and rulebook for Claude Code. Read it at the start of every session.

---

## What This Project Is

A reusable starter template for building AI-powered web apps quickly. The goal is to never
start from scratch again — copy this folder, rename it, and a new project is ready in minutes.

The primary user is a marketing student learning AI systems. The code must be readable and
educational, not just functional.

---

## Tech Stack

| Layer | Technology | Why |
|-------|-----------|-----|
| Framework | Next.js 14 (App Router) | Vercel-native, handles frontend + backend in one project |
| Styling | Tailwind CSS | Utility classes, no separate CSS files, fast to write |
| AI Layer | `lib/ai.js` wrapper | Swap providers by changing one env variable |
| Default AI | Anthropic Claude (`claude-sonnet-4-6`) | Best general-purpose model |
| Deployment | Vercel | Zero-config, free tier, integrates with GitHub |
| Language | JavaScript (no TypeScript) | Simpler for a non-developer learning codebase |

---

## Rules Claude Code Must Follow

### Code quality
- Keep code simple. No over-engineering. One file should do one thing.
- No TypeScript unless the user explicitly asks for it.
- Avoid adding features or abstractions beyond what was requested.
- Do not add comments that explain *what* the code does — only add a comment if the *why* is non-obvious.

### Security
- Never hard-code API keys. Always use environment variables.
- Validate inputs at API routes (check that required fields exist).
- Never expose internal error messages to the frontend in production.

### Style
- Use Tailwind CSS for all styling. No inline `style={}` props.
- Keep components small and focused.
- File names: `PascalCase` for components, `camelCase` for lib files.

### AI provider
- All AI calls must go through `lib/ai.js`. Never import an AI SDK directly in a page or component.
- The default provider is Anthropic Claude.
- Changing providers requires only changing `AI_PROVIDER` in `.env.local`.

---

## How to Explain Changes

Every time a file is created or modified, Claude Code should explain:

1. **What changed** — which file(s) and what was done
2. **Why it matters** — the reason behind the decision, not just what it does
3. **What to learn from it** — one concept or pattern the user can take away

Keep explanations short, plain, and written for a non-developer. No jargon without a definition.

---

## Deployment Process

1. Push code to GitHub
2. Import project in Vercel dashboard
3. Add environment variables manually in Vercel (they are never uploaded from `.env.local`)
4. Vercel auto-deploys on every push to the main branch

**Variables required in Vercel:**
- `AI_PROVIDER`
- `ANTHROPIC_API_KEY` (or whichever provider key is in use)
- `NEXT_PUBLIC_APP_NAME`

---

## What Each Key File Does

| File | Purpose |
|------|---------|
| `app/layout.js` | The HTML shell. Wraps every page. Set fonts, metadata, global styles here. |
| `app/page.js` | The homepage. Edit this to change what the user sees first. |
| `app/api/chat/route.js` | The AI backend. Receives messages from the UI, calls the AI, returns the reply. |
| `lib/ai.js` | The AI brain. Routes to the right provider. Edit the system prompt here. |
| `components/ChatBox.js` | Reusable chat UI. Drop `<ChatBox />` onto any page to add chat. |
| `.env.local` | Your secrets. Never committed. Copy from `.env.example`. |
| `project_context.md` | This file. Claude Code reads it to understand the project. |

---

## Coding Style Examples

**Good:**
```js
const reply = await chat(messages);
return NextResponse.json({ reply });
```

**Avoid:**
```js
// This function calls the AI and returns the response
const aiResponse = await callTheArtificialIntelligenceProvider(messageArray);
const jsonResponseObject = NextResponse.json({ reply: aiResponse });
return jsonResponseObject;
```

---

## Project History

- Created: 2026-05-09
- Purpose: Reusable AI web app starter for a marketing student
- Stack chosen for: simplicity, Vercel compatibility, AI-first structure
