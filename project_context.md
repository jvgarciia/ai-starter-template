# Project Context — AI Starter Template

This file contains project-specific state only: what the project is, its stack, its file map,
and its history. All process rules and conventions live in `CLAUDE.md` — do not duplicate them here.

---

## What This Project Is

A reusable starter template for building AI-powered web apps quickly. The goal is to never
start from scratch again — copy this folder, rename it, and a new project is ready in minutes.

[BUILDER PROFILE — fill in per project. Who is the primary user or maintainer, and what does their technical level mean for how the code should be written?]

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

## What Each Key File Does

| File | Purpose |
|------|---------|
| `app/layout.js` | The HTML shell. Wraps every page. Set fonts, metadata, global styles here. |
| `app/page.js` | The homepage. Edit this to change what the user sees first. |
| `app/api/chat/route.js` | The AI backend. Receives messages from the UI, calls the AI, returns the reply. |
| `lib/ai.js` | The AI brain. Routes to the right provider. Edit the system prompt here. |
| `components/ChatBox.js` | Reusable chat UI. Drop `<ChatBox />` onto any page to add chat. |
| `.env.local` | Your secrets. Never committed. Copy from `.env.example`. |
| `project_context.md` | This file. Read by Claude Code at the start of every session. |
| `CLAUDE.md` | Permanent operating rules for Claude Code — session protocol, conventions, workflow. |
| `AGENTS.md` | Same as CLAUDE.md, adapted for non-Claude agents (Codex, Cursor, etc.). |
| `todo.md` | Active task list — phases, statuses, what's left to do. Generated if missing. |

---

## Vercel Environment Variables

These must be added manually in the Vercel dashboard (they are never uploaded from `.env.local`):

| Variable | Value |
|----------|-------|
| `AI_PROVIDER` | `anthropic` (or `openai` / `gemini`) |
| `ANTHROPIC_API_KEY` | Real key from console.anthropic.com |
| `NEXT_PUBLIC_APP_NAME` | Display name shown in the browser tab and UI |

---

## Project History

- Created: 2026-05-09
- Purpose: Reusable AI web app starter [fill in per project]
- Stack chosen for: simplicity, Vercel compatibility, AI-first structure

---

## Process Rules

All workflow rules live in `CLAUDE.md`. Quick reference:

| Topic | See |
|-------|-----|
| Session protocol (what to read first) | `CLAUDE.md` → Session Protocol |
| What Claude Code may do automatically | `CLAUDE.md` → High Autonomy Development Mode |
| Git commit and push rules | `CLAUDE.md` → Git Workflow |
| Code quality, style, naming conventions | `CLAUDE.md` → Development Rules / Code Quality Expectations |
| When and how to test in the browser | `CLAUDE.md` → Browser Testing Workflow |
| Multi-AI review workflow | `CLAUDE.md` → Secondary AI Review Workflow |
| AI skills (llm-council, ui-ux-pro-max, etc.) | `CLAUDE.md` → Core AI Builder Stack |
| Marketing skills | `CLAUDE.md` → Marketing Skills |
| Task tracking and todo.md format | `CLAUDE.md` → Task Tracking |
| How to deploy to Vercel | `CLAUDE.md` → Deployment Workflow |
| How to format responses after code changes | `CLAUDE.md` → Communication and Output Expectations |
