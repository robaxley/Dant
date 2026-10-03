# Dant: notes for AI coding assistants

Read this first. Claude Code reads it through `CLAUDE.md`. Cursor and other assistants read it directly.

## Status

- **Nothing is built yet, on purpose.** The owner said to save the plan and not build it. Do not start building until the owner explicitly says go.
- The full product spec is in `docs/SPEC.md`, and it is the source of truth.
- Proposals that have **not** been approved yet are in `docs/IDEAS.md`. Don't treat anything there as a requirement unless the owner approves it, and then move it into `SPEC.md`.
- Open items before step 1:
  - The spec was cut off. Section 8 "Money" is only partly written (8a "Try before you pay" is decided), and the "Build order" is missing. Ask the owner for them.
- Ready-to-paste feature prompts from the owner live in `docs/prompts/`.
  - The logo files that `public/brand/` should hold are not in the repo yet.

## Working rules (from the owner)

- Build one step at a time, following the Build order.
- After each step: confirm the app runs locally (`npm run dev`), summarize what was built in plain language, then **stop and wait for the owner's OK**.
- If anything is unclear, ask instead of guessing.
- Never hardcode API keys or secrets. They go in `.env` (git-ignored) and get listed in `.env.example`.
- The owner is not a developer. Explain anything they need to do themselves, such as creating a Supabase project or pasting a key into `.env`, in simple numbered steps.

## Stack (short version)

Node 22+, Express 5, ES modules, vanilla HTML/CSS/JS in `/public` (no framework). Supabase (Postgres + Auth + Storage, RLS on every table). `@anthropic-ai/sdk` using a server-side key, with the model taken from `ANTHROPIC_MODEL`. Resend, Stripe and Stripe Connect Express. Deployed on Railway.

## Product language rules

The UI never says "system prompt", "API", or "token". Users never paste API keys. Every screen answers three questions: what will happen, is it safe, and how do I undo it.
