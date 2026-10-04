# Start prompt for Cursor

How to use it:
- To build the next step, open a new Cursor chat and paste everything below the line.
- When a step is finished and you're happy with it, either reply "OK" in the same chat, or start a new chat and paste this prompt with "OK" typed at the very top.

---

You're helping me build Dant, one step at a time. Read these files first, in order: AGENTS.md, docs/SPEC.md, docs/PROGRESS.md. docs/SPEC.md is the source of truth. Follow its rules in section 0.

Then:

1. Look at docs/PROGRESS.md and find the next step that isn't "Done".
   - If a step says "Waiting for owner's OK" and this message starts with "OK", mark that step "Done" and continue with the next one.
   - If a step says "Waiting for owner's OK" and this message doesn't start with "OK", remind me in 3 short bullets what that step built and ask if it's OK. Don't start anything new until I say OK.
2. Build ONLY that step, exactly as described in docs/SPEC.md section 18. Don't start the step after it, and don't add things the spec doesn't ask for.
3. If the step says "⛔ Ask the owner first", ask me those questions and wait for my answers before writing any code.
4. If anything in the spec is unclear, or conflicts with what's already built, ask me instead of guessing.
5. Never put passwords or keys in the code. This project is public on GitHub. Keys go in .env (which is never uploaded) and get listed in .env.example.

When the step is finished:

1. Make sure the app runs (npm run dev) and the tests pass (npm test).
2. Check every item in that step's "Done when" list.
3. Update docs/PROGRESS.md: set the step to "Waiting for owner's OK" and add a one-line log entry.
4. Then tell me, in plain language with no tech jargon:
   - What you built, in 3–6 short bullets.
   - How I can see it (what to open or click).
   - Each "Done when" check, and whether it passed.
   - Anything I need to do myself, as simple numbered steps that say exactly where to click.
5. Stop and wait for my OK.
