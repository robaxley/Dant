# Build Prompt: Dant

> Saved from the owner's message on 2026-10-03. This is the source of truth for what to build.
> **Status: not started. Do not build anything until the owner says go.**
> ⚠️ The message was cut off: section 8 ("Money") and the "Build order" section are missing. Ask the owner for them before step 1.

## Instructions for the AI coding assistant (Cursor)

- Build this in the current project folder, following the Build order at the bottom, one step at a time.
- After each step: make sure the app runs locally (`npm run dev`), summarize what you built, and stop and wait for my OK before starting the next step.
- If something in this spec is unclear, ask me instead of guessing.
- Never hardcode API keys or secrets. Put them in `.env` (git-ignored) and list them in `.env.example`.
- I'm not a developer, so explain anything I need to do myself (for example creating a Supabase project, or pasting a key into `.env`) in simple numbered steps.

## What Dant is

You are building Dant, a website for non-technical people ("for dummies") that works like YouTube + GitHub for AI, simplified.

People upload two kinds of things:

- **Agents:** ready-made AI helpers (instructions/prompts that make an AI act as an expert, e.g. "Small Business Marketing Agent"). You paste them into the AI you already use.
- **Dants:** everything else that helps get a job done: prompts, code, information (guides, templates, know-how), and websites (links to useful tools/resources).

Dant AI sits front and center: the home page is one big text box, "What do you want done?" (like Google or ChatGPT). Everything else lives in three tabs in the top navigation:

| Where | What it does |
|---|---|
| Dant AI (home page text box) | Type what you want done ("Market my company"). Dant AI picks the top-rated agent for the task, pulls information from relevant Dants, and does it. Optionally, connect your platforms so it can do the work for you. |
| Agents tab | Browse AI agents by topic. The top-rated agents for each topic show first. Copy one into ChatGPT, Claude, etc. |
| Find tab | Browse and search Dants (prompts, code, information, websites) by topic. |
| Upload tab | Share an Agent or a Dant. You earn money when people use it, like YouTube. |

One-liner: **"Find it, share it, or just tell Dant AI what you want done."**

Why it's different from ChatGPT/Claude:

- You don't need to know what to ask. Dant AI starts from agents and Dants that real people built and rated.
- No API keys, no setup. Dant AI runs on Dant's own AI, powered by the library.
- The people who create the best agents and Dants get paid.

## Audience and tone

- Beginners. No jargon in the UI: say "agent", "your website", "connect"; never "system prompt", "API", "token".
- Users never paste API keys anywhere on Dant. Dant AI works out of the box. Connecting a platform is optional and is always a one-click "Log in with ..." button.
- Every screen answers: what will happen, is it safe, how do I undo it.

## Brand

- Name: **dant** (lowercase wordmark). Logo files are already in `public/brand/`: `dant-logo-light.svg` / `dant-logo-dark.svg` (full wordmark) and `dant-mark-light.svg` / `dant-mark-dark.svg` (round icon, use it for the favicon).
  - ⚠️ As of 2026-10-03 these files are **not in the repo yet**. The owner needs to add them.
- Black and white, Helvetica Neue / system sans, lots of whitespace. Use an accent color only for primary actions and success. Light and dark mode.

## Tech stack (match my other projects)

- Node 22+, Express 5, ES modules, vanilla HTML/CSS/JS in `/public` (no framework).
- Supabase (Postgres + Auth + Storage for uploaded files). Row Level Security on every table.
- Anthropic SDK (`@anthropic-ai/sdk`) for Dant AI, using Dant's server-side key only (env var). Model comes from the `ANTHROPIC_MODEL` env var.
- Resend for email, Stripe for subscriptions, Stripe Connect for creator payouts. Deploy on Railway.
- Secrets only come from `.env` / Railway variables. Never hardcode them, and ship a `.env.example`.

## 1. Home = Dant AI

- Top navigation: logo (left); Agents · Find · Upload tabs; Log in / profile (right).
- The page is mostly empty space with the logo and one large text box in the center: "What do you want done?", auto-focused and multi-line, with a send button. This IS Dant AI. No separate page is needed to start.
- Under the box:
  - Example chips that fill the box when clicked ("Market my company", "Fix the layout on my homepage", "Write a week of Instagram posts", "Make a sales email for my new product").
  - An optional "+ Add your website" link.
- Pressing Enter expands the page into the Dant AI conversation/plan view (`/ai/task/:id`). The text box stays pinned at the bottom for follow-ups, like a chat.
- Below the fold: "Top agents this week", "Trending Dants", and topic tiles, which link into the Agents and Find tabs.

## 2. Agents tab

- Topic tiles: Marketing, Coding & Websites, Business & Sales, Writing, Social Media, Design, Money & Finance, Education, Productivity, Personal Life. Topics are admin-editable.
- Clicking a topic shows the top agents for that topic first, then Top / New / Trending tabs, and a "works with" filter (ChatGPT, Claude, Gemini, any).
- Agent card: name, what it does, author, "It worked ✓" %, uses count, and a comment count.
- Agent page:
  - What it does, and an example conversation/result.
  - Fill-in blanks (`[your business name]`) that become a simple form.
  - Copy agent, and "Open in Claude" / "Open in ChatGPT".
  - "Use with Dant AI" button.
  - "Did it work?" Yes/No, comments, Remix, and version history.

## 3. Find tab (Dants)

- The same topic tiles, plus a search bar at the top.
- Filter by Dant type: Prompt / Code / Information / Website.
- Ranked by quality: "It worked ✓" rate × uses × recency. Top / New / Trending.
- Dant page:
  - Prompt: copy button + blanks.
  - Code: syntax-highlighted view + download, with a "review before running" label.
  - Information: formatted text.
  - Website: link, preview image, and summary.
- Every Dant page also has "Did it work?", comments, Remix, and "Use with Dant AI".

## 4. Upload tab

- Step 1: "What are you sharing?"
  - Agent (goes in the Agents tab), or
  - Dant: Prompt, Code, Information, or Website (goes in Find).
- Step 2: a simple form: title, what it does, topic, "works with", the content (text editor; code editor or file upload; or a URL with an auto-fetched title and preview), and an optional example result.
- Preview before publishing. Edits create a new version.
- Show: "You earn when people use this. The better it works, the more you earn."

## 5. Dant AI (the home page text box)

- It starts from the home page text box (see Home), and is also reachable from "Use with Dant AI" on any agent or Dant page, which pre-loads that agent.
- No API keys, no setup required. It runs on Dant's own AI.
- How it works:
  1. Understand the request, and ask up to 2 short follow-up questions if needed ("What does your company sell?", "What's your website?").
  2. Pick the top-rated agent for that task from the Agents tab.
  3. Pull relevant Dants (information, prompts, code, websites) from Find.
  4. Show a plan with clear steps, and "Built with:" credit cards linking to each agent and Dant used.
  5. Deliver finished work the user can copy: marketing copy, posts, emails, code, step-by-step instructions.
  6. Optional: "Let Dant do it for me." If the user has connected a platform (one-click login, never API keys), show a preview of every action → the user approves → Dant AI does it → the result, with Undo where the platform allows it.
  7. After it's done: "Did it work?", which credits the agent and Dants that were used. Offer: "Share this as a Dant and earn."
- Example: "Market my company"
  1. The user gives their website URL.
  2. Dant AI uses the top marketing agent + brand-voice and email-template Dants.
  3. It reads the website to learn the business.
  4. It delivers an email campaign and 2 weeks of social posts.
  5. If Mailchimp/Instagram are connected, it schedules them after approval.

## 5b. "Do it for me" mode (Pro)

It should feel like handing a job to a capable helper, not operating a tool:

- **Give it a goal, not instructions.** "Market my company" is enough. Dant AI asks at most 2 questions, shows a short plan, then works in the background while the user does other things.
- **It checks its own work.** After each step, Dant AI reviews the result against the goal (on-brand? right length? does the code build?). If it falls short, it fixes it and tries again, up to 3 times, before showing the user. Short "what went wrong" notes go to the creator's feedback inbox, so the agents and Dants in the library keep getting better. This is Dant's own twist.
- Short progress updates ("Drafted 10 posts ✓ → Ready for your OK"), and a `/tasks` page listing every task with its result, the credited Dants, and Undo.
- Remembers the user's business and brand voice, so each task needs fewer questions. Users can view and delete this memory.
- Approval before anything goes public or live. Posting, sending, or changing a site needs one "Approve" tap with a preview. v1 never spends money.

## 6. Connections (optional, "Connect your stuff")

- One-click "Log in with ..." buttons (OAuth). Never ask users for API keys.
- Pluggable connector interface: `connect`, `readContext`, `planActions`, `applyActions`, `undo`.
- v1:
  - Website URL (read-only).
  - GitHub. Changes arrive as a pull request the user merges, never pushed straight to their live code.
  - Mailchimp.
  - Meta (Facebook/Instagram).
- Later: Shopify, WordPress, Wix, Google Ads, LinkedIn, X, HubSpot.

## 7. Creator pay (YouTube-style)

- Creators earn based on how much their agents/Dants get used and how good they are:
  - Every copy, Dant AI citation, and completed Dant AI task counts as a use.
  - Uses are weighted by quality: the "It worked ✓" rate, and completed tasks that weren't undone.
  - Spam protection: count one use per user per Dant per day, ignore self-use, and flag sudden spikes.
- Monthly creator pool: a set % of Dant's revenue (Pro subscriptions + ads later) is split by weighted uses. Put rates in config.
- Monetization threshold (like the YouTube Partner Program): e.g. X weighted uses and a Y% "It worked" rate before payouts turn on. This keeps quality high.
- Creator Studio (`/studio`):
  - Uses, "It worked ✓" rate, and estimated earnings per agent/Dant.
  - Charts over time.
  - A feedback inbox that collects all comments and "didn't work" reports on their uploads, so they can improve and publish a new version.
  - Payout history, and a "Connect payouts" button (Stripe Connect Express).
- Comments = feedback: threaded comments on every agent/Dant. Creators can reply and pin a comment. "Didn't work" votes prompt: "What went wrong?" (optional text sent to the creator).
- Profiles/channels: their agents and Dants, followers, total uses, and "It worked ✓" rate. Users can follow creators.

## 8. Money (Dant AI is a Pro feature)

> ⚠️ **Partly missing.** The original message ended at this heading. Only 8a has been decided so far. Ask the owner for the rest (price, ads, etc.).

### 8a. Try before you pay (approved by the owner, 2026-10-03)

People see Dant AI do real work before we ask for anything. We ask for an account only after their first result, and for money only when they want Dant to do more *for* them.

| | Logged out | Free account | Pro |
|---|---|---|---|
| Dant AI tasks | 1 free try | 5 per month (resets on the 1st) | Up to 200 per month (fair use) |
| Full plan + finished work to copy | Yes | Yes | Yes |
| "Let Dant do it for me" (post, send, schedule, open a pull request) | No | No | Yes |
| Connect your stuff | No | No | Yes |
| Dant remembers your business | No | No | Yes |
| Works in the background | No | No | Yes |

- All numbers live in one config file so they can change without code changes.
- **One task = one goal typed into the big box** (or started from "Use with Dant AI"). Follow-up questions and messages inside a task are free, up to 20 per task. Failed tasks are given back automatically.
- **The free version is never made worse.** Same quality and the full result as Pro. The difference is what Dant does for you, not how good the work is. Nothing is hidden or blurred.
- **Logged out:** no sign-up before the first task. After the result: "Like it? Create a free account to save this and get 5 more tasks every month." The task carries over into their account after signing up. A second logged-out try asks them to make a free account and keeps what they typed. Abuse protection: Supabase anonymous sign-in + Cloudflare Turnstile, and at most 3 logged-out tries per network per day.
- **Free account:** a calm counter near the box ("4 of 5 free tasks left this month"). Running out shows a friendly screen ("They come back on [date]. Want to keep going now? Go Pro.") instead of an error.
- **Asking for Pro happens only when Pro clearly helps:**
  - After a result Dant could act on, e.g. "Your posts are ready. Copy them for free, or go Pro and Dant will schedule them for you."
  - When someone clicks a locked Pro button (it shows a lock + "Pro" label and is never a dead button).
  - When the free tasks run out.
  - Every upgrade panel says "Cancel anytime in one click." and has "Not now". Show it at most once per task.
- **Enforced on the server:** the allowance check, atomic counting (no double-click cheating), and blocking Pro-only actions. RLS: people can only read their own usage.
- **Words:** "tasks", "free account", "Pro". Never "credits", "tokens", "quota", or "API".
- No price is shown until the owner sets one. If Stripe isn't built yet, "Go Pro" opens a `/pro` page with a "Tell me when it's ready" email sign-up.

## Build order

> ⚠️ **Missing.** The spec says "following the Build order at the bottom", but it was not included. Ask the owner for it. A suggested order is in `docs/IDEAS.md` §8, for use only if the owner approves it.
