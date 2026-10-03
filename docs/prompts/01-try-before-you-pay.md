Read AGENTS.md and docs/SPEC.md first and follow their rules: one step at a time, ask me instead of guessing, never put secrets in code, explain anything I have to do myself in simple numbered steps, and stop and wait for my OK when you're done.

# Task: add "Try before you pay" to Dant AI

Goal: people see Dant AI do real work for them before we ask for anything. We ask for an account only after their first result, and for money only when they want Dant to do more FOR them.

## Before you start

1. Check what's already built. This feature needs three things: the Dant AI text box and task page (/ai/task/:id), login (Supabase Auth), and a place where tasks are saved.
2. If any of those are missing, do NOT build them now. Instead, make sure the rules below are in docs/SPEC.md under "8a. Try before you pay", tell me which build step this belongs in, and stop.
3. If anything below conflicts with what's already built or with docs/SPEC.md, ask me before changing it.

## The three levels

| | Logged out | Free account | Pro |
|---|---|---|---|
| Dant AI tasks | 1 free try | 5 per month (resets on the 1st) | Up to 200 per month (fair use) |
| Full plan + finished work to copy | Yes | Yes | Yes |
| "Let Dant do it for me" (post, send, schedule, open a pull request) | No | No | Yes |
| Connect your stuff (Mailchimp, Instagram, GitHub…) | No | No | Yes |
| Dant remembers your business | No | No | Yes |
| Works in the background while you do other things | No | No | Yes |

Put every number (free tries, monthly tasks, Pro fair-use limit, messages per task, logged-out tries per network) in ONE config file, for example config/plans.js, so I can change them later without touching anything else. Don't repeat these numbers anywhere else in the code.

## What counts as a task

- One goal typed into the big box ("Market my company") = 1 task. Starting from "Use with Dant AI" on an agent or Dant page counts the same way.
- Dant AI's follow-up questions, my answers, and follow-up messages inside the same task are free (up to 20 messages per task).
- If a task fails or Dant AI can't finish it, it doesn't count. Give it back automatically.

## Never make the free version worse

- Free tries get the same quality and the full finished result as Pro. The difference is what Dant does FOR you, not how good the work is.
- Never hide, blur, or cut off part of a result to push an upgrade.

## Logged-out visitors

1. A visitor types in the big box and presses Enter. No sign-up screen first.
2. Dant AI runs the task like normal: plan, "Built with" credits, finished work.
3. Under the result, show: "Like it? Create a free account to save this and get 5 more tasks every month." with "Continue with Google" and "Use my email" buttons.
4. After they sign up or log in, this task is saved in their account and shows up on /tasks. Never lose their work.
5. If they try a second task while logged out, show: "You've used your free try. Create a free account to keep going. It's free and takes one click." Keep what they typed in the box so they don't have to retype it.

How to build it:
- Use Supabase anonymous sign-in for logged-out visitors, so their task belongs to a real (temporary) user and Row Level Security still works. When they sign up, upgrade that same user by linking their Google account or email, so the task stays theirs. If they log into an account that already exists instead, move the task to that account on the server.
- Protect our AI bill: turn on Cloudflare Turnstile (the invisible "are you a human" check) for anonymous sign-ins, and allow at most 3 logged-out tries per network per day. Tell me in numbered steps how to get the Turnstile keys and where to paste them in .env, and add them to .env.example.

## Free accounts

- Show a small, calm counter near the big box: "4 of 5 free tasks left this month". No pop-ups.
- When they run out, show a friendly screen instead of an error: "You've used your 5 free tasks this month. They come back on [date]. Want to keep going now? Go Pro." Below it, link to what they've already made (/tasks).
- Keep whatever they were typing.

## When to ask for Pro

Only ask at moments where Pro clearly helps:

1. **After a result Dant could act on.** Example: "Your posts are ready. Copy them for free, or go Pro and Dant will schedule them for you." Match the message to the result: posts → schedule them, email → send it, website fix → set up the change for you to approve.
2. **When they press a Pro-only button** ("Let Dant do it for me", "Connect", "Remember my business"). These buttons show a small lock and a "Pro" label. Clicking one opens a small panel that explains in one sentence what the feature does, with a "Go Pro" button. Never a dead button that does nothing.
3. **When they run out of free tasks** (see above).

Every upgrade panel also says "Cancel anytime in one click." and has a "Not now" button that closes it. Don't show the same upgrade panel more than once per task.

## The "Go Pro" button

- If Stripe subscriptions are already built, open Stripe Checkout.
- If not, open a simple /pro page that explains what Pro includes, with a "Tell me when it's ready" button that saves their email. Don't build Stripe in this step.
- Don't show any price until I give you one.

## Rules that keep it safe and fair

- Check the person's remaining tasks on the SERVER before running any Dant AI task. Never trust the browser.
- Do the check-and-count in one database step, so double-clicking Send or opening two tabs can't use extra tasks or sneak past the limit.
- Block Pro-only actions on the server too, not just by hiding buttons.
- Row Level Security: people can only see their own usage, and only the server can change it.
- Words in the app: say "tasks", "free account", and "Pro". Never say "credits", "tokens", "quota", or "API".

## When you're done

Test each of these yourself and tell me in plain language whether each one passed:

1. Logged out: the first task works with no sign-up.
2. Logged out: a second task shows the "free try used" message and keeps my typing.
3. Signing up after the free try keeps the first task on /tasks.
4. Free account: the counter goes down by 1 per task, and follow-up messages don't count.
5. A task that fails doesn't count.
6. After 5 tasks, the "they come back on [date]" screen shows instead of an error.
7. Double-clicking Send only uses 1 task.
8. Pro-only buttons show a lock and the upgrade panel, and the server refuses the action for a free account even if someone forces the button.
9. A Pro test account can use everything, up to the fair-use limit. Tell me in numbered steps how to make one.

Then update docs/SPEC.md if anything changed, summarize what you built, list anything I need to do myself as numbered steps, and stop and wait for my OK.
