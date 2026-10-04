# Dant: notes for AI coding assistants

Read this first. Claude Code reads it through `CLAUDE.md`. Cursor and other assistants read it directly.

## Where things are

| File | What it is |
|---|---|
| `docs/SPEC.md` | **The source of truth** (v2). The product spec plus the step-by-step Build order (§18). |
| `docs/PROGRESS.md` | Which build steps are done. Update it at the end of every step. |
| `docs/prompts/00-start-here.md` | The prompt the owner pastes into Cursor to build the next step. |
| `docs/IDEAS.md` | Only decisions still waiting on the owner, and ideas for after launch. **Not requirements.** |
| `docs/archive/SPEC-v1.md` | The owner's original prompt, kept for reference. |

## Status

- Nothing is built yet. Build only when the owner asks, one step at a time, starting from the first step in `docs/PROGRESS.md` that isn't "Done".
- Open items:
  - The logo files for `public/brand/` aren't in the repo yet. Use the placeholder in SPEC §3 until they arrive.
  - Owner decisions are needed before steps 12 and 16 (SPEC §14b, §14c).

## Working rules (from the owner)

- Build one step at a time, following the Build order.
- After each step:
  1. Confirm the app runs locally (`npm run dev`) and the tests pass.
  2. Update `docs/PROGRESS.md`.
  3. Summarize what was built in plain language.
  4. **Stop and wait for the owner's OK.**
- If anything is unclear, ask instead of guessing. Don't add features the spec doesn't ask for.
- Never hardcode API keys or secrets. They go in `.env` (git-ignored) and get listed in `.env.example`. **This repo is public.**
- The owner is not a developer. Explain anything they need to do themselves, such as creating a Supabase project or pasting a key into `.env`, in simple numbered steps.

## Stack (short version)

- Node 22+, Express 5, ES modules, plain HTML/CSS/JS with no front-end framework. Public pages are rendered on the server for SEO.
- Supabase (Postgres + Auth + Storage, RLS on every table, migrations in git).
- `@anthropic-ai/sdk` with a server-side key, the model taken from `ANTHROPIC_MODEL`. Read SPEC Appendix A1 before writing any AI code.
- Resend, Stripe and Stripe Connect Express. Deployed on Railway.

## Product language rules

- The UI never says "system prompt", "API", "token", "credits", or "quota".
- Users never paste API keys.
- Every screen that changes something shows the safety box: what will happen, is it safe, how to undo it.
