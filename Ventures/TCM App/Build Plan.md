# TCM App — Build Plan

Step-by-step plan for building the app with zero coding experience, using Claude Code as the builder. Read this first; the actual build instructions Claude follows are in [[Ventures/TCM App/Super Prompt|Super Prompt]].

## The approach in one paragraph

Same model as [[Ventures/Meridian/index|Meridian]]: you are not going to write code — Claude Code writes all of it. Your job is founder + product owner: paste the super prompt, test each phase in your browser like a normal user, say what feels wrong, and make product decisions when asked. The build is split into 7 phases with a hard stop after each one. This app is simpler than Meridian in one important way: **no login/accounts and no daily-logging habit to design for** — it's a search-and-browse reference tool, so the whole build is lighter. Ship as a **mobile-friendly web app first** (a link for your TikTok bio) — same reasoning as Meridian: instant shipping, no App Store fee or review queue up front.

## Step 0 — Accounts to create (~10 min — much shorter than last time)

You already have these from building Meridian — reuse them:

| Account | What it's for | Cost |
|---|---|---|
| GitHub | Code storage | Free |
| Vercel | Hosting; gives you a live URL | Free tier |
| Supabase | Database (content only — no login system this time) | Free tier |
| Anthropic Console | API key so the import pipeline can generate ingredient explainers | A few dollars — you'll barely touch this since AI only runs once per ingredient, not per visitor |

The only new thing: create a **new, separate Supabase project** for this app (don't reuse Meridian's — keep the two apps' data apart). Same sign-in-with-GitHub flow as before.

## Step 1 — Create the project (5 min)

1. Make a new folder: `C:\Users\Angela\Projects\tcm-app` — **not inside the Brain vault**, same rule as Meridian: the vault is for notes, apps live in their own folders.
2. Open that folder in VSCode (File → Open Folder).
3. Start a Claude Code session there.

## Step 2 — Paste the super prompt

Copy everything below the `---` line in [[Ventures/TCM App/Super Prompt|Super Prompt]] and paste it as your first message. Claude will build **Phase 1 only** (project skeleton + landing page + email waitlist) and then stop and tell you how to look at it.

## Step 3 — Test each phase like a user

Same as before: after every phase Claude stops and tells you how to check its work (`npm run dev`, open `http://localhost:3000`, click around **on your phone-sized browser window too**). Describe anything that looks wrong in plain English, then say "continue to the next phase."

In later sessions, start with: **"Read PROGRESS.md and continue with the next phase."**

## Step 4 — Go live early, and start the content test in parallel

Deploy to Vercel as soon as the landing page exists in Phase 1.

- This is the same link you can use for the TikTok content test already planned — see [[Content/Ideas/TCM food properties series]]. Post "is ginger hot or cold?" style content, point people at the waitlist, and watch save/comment rates. You don't need to wait for the full app to validate demand.
- If the waitlist is dead after a few honest attempts, that's a cheap, early signal — much cheaper than building all 7 phases first.

## Step 5 — Phases 2–7

Realistic total: likely **faster than Meridian's 2-4 weekends**, since there's no login system or chart-computation engine to build — the hardest part of this build is the content, not the code.

1. ~~Phase 1~~ — Skeleton + landing page + waitlist
2. Phase 2 — Data model + spreadsheet-based content import pipeline + starter ~15-20 entries
3. Phase 3 — Search, browse, and ingredient detail pages (the core loop)
4. Phase 4 — AI-generated plain-English explainer per ingredient (one-time, cached)
5. Phase 5 — Constitution quiz + personalized badges
6. Phase 6 — Seasonal content ("this season") + favorites
7. Phase 7 — Polish, disclaimers, privacy page, launch checklist

## Step 6 — Feed the content pipeline in parallel with the build

This is the part that isn't "building an app" — it's compiling the actual TCM data, and it can happen alongside Phases 1-3:

1. Claude Code will give you an exact spreadsheet column template in Phase 2 (ingredient name, thermal nature, five flavors, organ affinity, actions/indications, contraindications, source citation, confidence level).
2. Fill it in for the ~15-20 dampness/digestion-wedge ingredients first, using the sources already logged in [[Ventures/TCM App/index|the venture note]] (Compendium of Materia Medica via ctext.org, Pitchford's *Healing with Whole Foods* as a structural model — don't copy text directly, compile your own entries from these as references).
3. Get your TCM practitioner reviewer to check the sheet — ideally bring them in now, not just before launch (see the Open Gaps section in the venture note on why earlier is better).
4. Re-run the import script any time the sheet changes — no need to touch code for this.

## Step 7 — Beta test

Give the link to 10-20 friends. Watch what they search for unprompted (that tells you what content to prioritize next), what they screenshot (that's your shareable moment), and whether the constitution quiz result feels personal or generic. A generic-feeling badge is the main failure mode to watch for — iterate on the `constitution_compatibility_rules` data with your practitioner if it doesn't feel right.

## Step 8 — Later (only after traction)

- Custom domain (~USD $15/yr) once a real name is chosen
- Payments/monetization — deliberately not in MVP; the Revenue ideas section of [[Ventures/TCM App/index|the venture note]] has the options to revisit once there's traffic to monetize
- Wrap as a native app only if it turns out people want push notifications or app-store discovery — not needed for the reference-tool model the way it might have been for a daily-logging tracker
- v2 candidates: accounts + cross-device sync, the food/symptom tracker (only if usage shows people want to log, not by default), AI chat assistant, practitioner directory/booking

## Things to keep in mind

- **The content is the product.** Unlike Meridian, where the hard technical problem was the chart-computation engine, here the hard problem is getting TCM properties right and cited. Budget your own time and the practitioner-review cost accordingly — see the cost forecast in [[Ventures/TCM App/index|the venture note]].
- **No accounts means no login bugs to chase**, but also means favorites/quiz results are per-browser, not per-person — if someone switches phones, they lose their saved list. That's an accepted v1 tradeoff, not an oversight.
- **Every ingredient page needs a visible source citation.** This is the whole differentiation argument against free blog content — don't let Claude Code bury it in a footnote during Phase 3.
- **"TCM" as a name is generic/descriptive** — fine to keep as a working name, but it likely can't be trademarked as-is. Worth a real name before you invest in a custom domain or logo.
- **Cost control is designed in:** the only AI calls happen once per ingredient at import time, not per visitor — so running cost stays near zero no matter how much traffic the TikTok content drives.

Related: [[Ventures/TCM App/index|TCM App]] · [[Ventures/TCM App/Super Prompt|Super Prompt]]
