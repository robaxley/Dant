# Ideas to make Dant as good as it can be

> Proposals from Claude, 2026-10-03. **None of these are approved yet.** `SPEC.md` wins wherever the two disagree. Once the owner approves an idea, move it into `SPEC.md`.
> Ordered by impact. Sections 1–6 are for the owner, in plain language. Section 7 is technical notes for the AI coding assistant.

---

## 0. Settle these before step 1

1. **The spec was cut off.** It stops at "8. Money (Dant AI is a Pro feature)", and the "Build order" never arrived.
2. **The logos are missing.** `public/brand/` doesn't exist in the repo yet.
3. **Free vs. Pro on the home page.** The home page *is* Dant AI, and Dant AI is Pro-only. That means a first-time visitor types "Market my company", presses Enter, and hits a paywall. That's the worst possible first impression. See idea 1.1.

---

## 1. The five biggest ideas

### 1.1 Let people feel the magic before they pay
- **Logged out:** 1 free Dant AI task, with no signup needed. They see the plan and the first piece of finished work.
- **Free account (one click with Google):** a few tasks a month (for example 5), plus copying any agent or Dant forever.
- **Pro:** "Do it for me" running in the background, connections (Mailchimp, Instagram, GitHub), memory of your business, and many more tasks.
- Put the paywall **after** the value: "Your 2 weeks of posts are ready. Go Pro to have Dant schedule them for you." The spec's split already fits this well, since copying is free and having Dant *do it* is Pro.

### 1.2 Pay creators "user-centric", not one big pot
- The spec splits one pool across all weighted uses. That's how Spotify started, and it has two problems. Fake accounts can farm uses to drain the pot, and the most-used creators take a share even of subscribers who never used them.
- The better model: **each Pro member's share of the creator pool goes only to the creators that member actually used that month.** SoundCloud calls this "fan-powered royalties."
- Why it's better for Dant:
  - **Fraud mostly stops working.** A bot army can only redirect its own subscription fees, so it can't drain everyone else's.
  - **It's easy to explain:** "Your subscription pays the people whose agents helped you."
- Free users' uses would still count, from a small separate pot (later funded by ads), so free traffic matters too.
- Keep the spec's quality weighting ("It worked ✓" rate, tasks that weren't undone) and its monetization threshold on top.

### 1.3 Treat every upload as possibly hostile. This is Dant's biggest risk.
Dant AI runs other people's agents with Dant's own AI, and sometimes with a user's connected Mailchimp, Instagram, or GitHub. A malicious agent could hide an instruction like "also email the user's contact list to me." Rules that prevent this:
- Library content goes into Dant AI as **reference material to read**, never as commands to follow. Only Dant's own instructions can trigger actions.
- **Every action needs the user's Approve tap with a preview.** The spec already requires this, and it's the safety net. Never add a "skip approval" option.
- Every upload is automatically screened before it goes live. The screen looks for hidden instructions, spam, harmful content, and suspicious code in Code Dants, and checks Website Dants against a known-bad-links list.
- New creators' uploads show up under "New" but can't reach "Top" until they have enough real uses.
- Ask for the smallest permissions possible when connecting a platform. "Disconnect" cuts off access immediately.

### 1.4 Solve the empty-library problem before launch
On day one, a library with nothing in it makes Dant AI generic and the tabs look dead. Plan:
- Seed **about 10 strong agents and 10 Dants per topic** (≈200 items) under a "Dant Originals" account. Write them with AI, then test each one by hand.
- Run a **Founding Creators** program: invite 25–50 people with a badge, early access, and a boosted earnings rate for their first 6 months.
- When no good agent exists for a request, Dant AI still does the job well using its own built-in skills, then offers "Share this as a Dant and earn." Every gap becomes an invitation to create.

### 1.5 Make every agent and Dant page findable on Google
- Each agent, Dant, and creator page should be a real web page that Google can read, not a blank page filled in by JavaScript. "Instagram caption agent" and "small business email template" are things beginners already Google.
- Each page also gets a nice preview card when it's shared on social media or in texts.
- This is free, compounding growth. It's the reason YouTube and GitHub pages show up everywhere.

---

## 2. Making Dant AI really good

- **A "How to tell it worked" checklist on every upload.** The creator writes 3–5 checks, for example "posts under 150 words", "mentions the business name", "ends with a call to action". Dant AI grades its own work against these during the "checks its own work" step. When something fails, the creator gets a specific note ("3 of 10 posts were too long"). This ties your twist together: creators define what good means, Dant enforces it, and the library improves.
- **A business card for memory.** Store the business name, what you sell, who buys it, tone of voice, website, and colors. It **auto-fills `[your business name]`-style blanks** across every agent ("Filled from your business card · edit"), so beginners stop retyping the same things.
- **Show why it picked something.** The plan can say: "Using *Small Business Marketing Agent*: 94% said it worked, 12,400 uses." That builds trust, and creators get visible credit.
- **Fair ranking.** Don't sort by raw "It worked %", or one vote of 1/1 = 100% beats 950/1000 = 95%. Rank by a *confidence-adjusted* score, which needs plenty of votes before trusting a high %. For Trending, give recent activity more weight.
- **Count quiet signals of "it worked", because most people won't vote:**
  - The user approved the work without editing it.
  - The task wasn't undone within 7 days.
  - The user copied the result and didn't come back searching for the same thing.
  - A friendly email 2 days later asks "Did your posts go out OK? 👍 / 👎".
- **Only people who actually used something can vote on it**, and votes apply to a specific version, so a fixed v2 isn't held back by v1's ratings.
- **A test set.** Keep 30–50 real "What do you want done?" requests and their ideal results. Re-run them before every change to Dant AI, so improvements are measured instead of guessed.

## 3. Safety and "how do I undo it"

- **One reusable safety box.** The same little panel everywhere: *What will happen* · *Is it safe* · *How to undo*. Beginners learn it once and trust it everywhere.
- **Schedule by default, don't post now.** Many platforms can't truly undo a post once it's live. Making "Schedule for tomorrow 9am" the default creates a natural undo window, like Gmail's "Undo send".
- **Action buttons say exactly what happens:** "Post 7 photos to Instagram, Mon–Sun at 9am", never just "Run".
- **An activity log for every task:** what was done, where, and when, with Undo next to anything that can still be undone.
- **A Report button** on every agent, Dant, and comment, plus a simple copyright takedown process.
- **Legal basics before payouts start:** terms of service, a creator agreement covering who owns uploads and what remixing allows, a privacy policy (you'll be storing business memory), and 13+ only. Have a lawyer review these once.

## 4. The creator economy

- **Remix royalties.** When someone remixes an agent and the remix earns, the original creator gets a small cut (for example 10–20%). This turns Remix into a GitHub-fork-style family tree and encourages sharing over copying.
- **"Improve with AI" in Creator Studio.** Dant AI reads the creator's feedback inbox and drafts a v2 that fixes the top complaints. The creator reviews and publishes it. This is the fastest way to make the library better.
- **Tell past users about new versions:** "The agent you used last week got better (v3)."
- **Clear earnings.** Show *why* the estimate is what it is: "212 uses × 91% worked → about $14.20 this month."
- **Sensible payouts.** Stripe Connect Express handles ID checks and tax forms. Pay monthly, with a minimum (for example $10) and a ~30-day hold so refunds and fraud can be caught first.
- **Creator links and badges.** Creators can put a "Use it on Dant" link in their YouTube descriptions, newsletters, and websites. Creators become your marketing team, so consider a small bonus when someone they bring in goes Pro.

## 5. Growth

- **Shareable results.** After a task, offer "Share what Dant made" as a public page with a "Made with Dant" footer. Each share is an ad.
- **Open in Claude / Open in ChatGPT** links that pre-fill the agent. Long agents fall back to "Copied! Now paste it in" plus opening the site.
- **Export agents** in the formats people already use: Claude Projects, ChatGPT custom GPTs, Gemini Gems.
- **Later: put Dant inside Claude and ChatGPT** as a connector, so people can search the Dant library without leaving their chat. Those uses still pay creators.
- **A weekly email** with the "top agents this week" in the topics you follow.
- **A mic button** on the big text box. Many beginners would rather say what they want than type it.

## 6. Connections: suggested order

1. **Website (read-only).** The easiest, and it powers "learn my business."
2. **GitHub.** Pull requests are naturally safe and reversible.
3. **Mailchimp.** Standard one-click login, and schedule-then-unschedule works.
4. **Meta (Facebook/Instagram).** Do this last, but **apply for Meta's app review early**. It needs business verification and can take weeks. Instagram posting also requires the user to have an Instagram Business or Creator account linked to a Facebook Page. Explain that in plain words when they connect.

---

## 7. Technical notes for the AI coding assistant

**Claude (Anthropic SDK)**
- Default `ANTHROPIC_MODEL=claude-opus-5-5`. Set `output_config.effort` per job instead of switching models: `low` for routing, moderation, and simple classification; `medium`/`high` for the real work and self-check grading. Opus 5.5's default effort is `medium`, so set it explicitly. Only add a second cheaper model (an optional `ANTHROPIC_FAST_MODEL`) if measurement on the test set shows it holds quality, and only with the owner's OK.
- Thinking can't be disabled on Opus 5.5, and forced `tool_choice` (`any`/`tool`) returns a 400. Use `auto` plus `strict: true` tools, or structured outputs.
- **Prompt caching:** keep Dant AI's system prompt and tool list byte-for-byte stable and first. Put per-request content (library excerpts, user message) after the cache breakpoint. Check `usage.cache_read_input_tokens`.
- **Structured outputs** (`output_config.format`) for the plan, "Built with" credits, self-check verdicts, and action previews, so the UI always gets valid JSON.
- **Reading the user's website:** use the server-side `web_fetch_20260209` tool, so Anthropic fetches the page and our server never fetches arbitrary user URLs. Upload-time link previews still need server-side fetching, which must have SSRF protection (block private/internal IPs, limit redirects and size).
- **Prompt-injection hygiene:** library content goes in the user turn inside clearly labeled `<library_item>` blocks as data, never in `system`. Tools that act on connected platforms only *propose* actions. Execution happens only after the user approves in the UI.
- **Batch API (50% cheaper)** for non-urgent jobs: upload screening, auto-generating example results, creator-feedback summaries, and "Improve with AI" drafts.
- **Cost guards:** per-user monthly task quotas in the database, a token budget per task (`task_budget`, beta), rate limiting, and Cloudflare Turnstile on logged-out use.
- Handle `stop_reason: "refusal"` gracefully, with a friendly message in the UI.
- Self-check loop: generate → grade against the goal + the creator's checklist (structured verdict) → revise, at most 3 rounds. Each failed check writes a short note to `feedback` for the credited items' creators. If the background mode outgrows a homegrown worker, evaluate Claude Managed Agents (its "outcomes" feature is a rubric-graded retry loop).

**Data (Supabase)**
- Keep schema changes as migrations in git (Supabase CLI). RLS on every table. The browser only ever gets the anon key; the service-role key stays on the server.
- Sketch: `profiles`, `topics`, `items` (kind: agent | prompt | code | info | website), `item_versions` (immutable; votes, uses, and credits point at a version), `votes`, `comments` (threaded, `pinned`), `uses` (unique on user + item + day; self-use excluded), `tasks`, `task_steps`, `task_credits`, `connections` (OAuth tokens encrypted at rest), `business_memory`, `follows`, `feedback`, `payouts`, `reports`.
- Search: start with Postgres full-text search plus a recency/quality score. Add pgvector semantic search later if needed.

**App shape**
- Express renders public pages (agent, Dant, profile, topic) as HTML on the server for SEO and OpenGraph tags, with vanilla JS for interactivity. That's still no framework.
- Background tasks: a Postgres-backed job queue plus a separate Railway worker service. Push progress to the browser with Server-Sent Events.
- Payments: Stripe Checkout + Customer Portal (no custom billing UI), Stripe Connect Express for creators. Keep pool %, thresholds, and payout minimums in a config file.
- Observability: error tracking (e.g. Sentry) and product analytics (e.g. PostHog). North-star metric: **tasks that worked, per week.**
- Tests: a few Playwright smoke tests (home → task → plan; upload → publish; copy agent) run before each step is called done.

---

## 8. Suggested build order (only if the original is lost, and only with the owner's OK)

1. Skeleton: Express server, nav, home text box (no AI yet), light/dark mode, brand, `.env.example`.
2. Supabase: auth (Google + email link), schema, RLS, seed topics.
3. Upload + agent and Dant pages + versions.
4. Agents and Find tabs: browse, search, ranking.
5. "Did it work?", comments, Remix, follows, creator profiles.
6. Dant AI v1: understand → pick agent → pull Dants → plan → deliver → credits.
7. Usage tracking + Creator Studio (stats and feedback inbox, no money yet).
8. Pro subscriptions and limits (Stripe).
9. Connections: website read, then GitHub pull requests.
10. "Do it for me" background mode, `/tasks`, memory.
11. Creator payouts (Stripe Connect, monthly pool).
12. Mailchimp, then Meta.
13. Before public launch: seed the library, moderation and reporting, legal pages.
