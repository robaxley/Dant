# Ideas: status

> Updated 2026-10-04. The owner asked to "make Dant better and fix current flaws", so most ideas from the first list are now part of `docs/SPEC.md` (v2). Appendix B there lists every change.
> This file tracks only what's **not** in the spec yet: decisions waiting on the owner, and ideas for after launch.

## Waiting on the owner's decision (the spec has ⛔ checkpoints for these)

| Decision | When | Recommendation |
|---|---|---|
| Pro price (monthly / yearly / trial) | Before step 12 | Owner's call. Watch AI cost per task from step 9 to make sure the price covers it. |
| Creator payout model | Before step 16 | **User-centric:** each Pro member's share goes only to the creators they used. It's fairer, and fake accounts can only redirect their own fee. SoundCloud's "fan-powered royalties" works this way. |
| Creator pool % of revenue | Before step 16 | Owner's call. |
| Monetization threshold | Before step 16 | Placeholder: 500 weighted uses in 90 days + 70% "It worked". |
| Remix royalties | Before step 16 | Yes, 10–20% of a remix's earnings to the original creator. It encourages sharing over copying. |

## After launch

- **Export agents** as Claude Projects, ChatGPT custom GPTs, or Gemini Gems.
- **Dant inside Claude and ChatGPT:** a connector that lets people search the Dant library from their chat. Those uses still pay creators.
- **Weekly email:** "Top agents this week" in the topics you follow.
- **Creator links and badges:** a "Use it on Dant" link for YouTube descriptions, newsletters, and websites, plus a small bonus when a creator brings in someone who goes Pro.
- **More connections:** Shopify, WordPress, Wix, LinkedIn, X, HubSpot, and Google Ads (read-only until spending rules exist).
- **Smarter search:** meaning-based search (pgvector) on top of keyword search, once the library is big enough to need it.
- **Ads** (§14d in the spec).
