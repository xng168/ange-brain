# Astrology App — Build Plan

Step-by-step plan for building the app with zero coding experience, using Claude Code as the builder. Read this first; the actual build instructions Claude follows are in [[Ventures/Astrology App/Super Prompt|Super Prompt]].

## The approach in one paragraph

You are not going to write code — Claude Code writes all of it. Your job is founder + product owner: paste the super prompt, test each phase in your browser like a normal user, say what feels wrong, and make product decisions when asked. The build is split into 7 phases with a hard stop after each one so nothing runs away from you. Ship as a **mobile-friendly web app first** (a link you can put in your TikTok bio) and only wrap it into a "real" App Store app after people are actually using it.

## Step 0 — Accounts to create (~45 min, one-time)

| Account | What it's for | Cost |
|---|---|---|
| GitHub | Code storage (you already have this) | Free |
| [Vercel](https://vercel.com) — sign up **with GitHub** | Hosting; gives you a live URL | Free tier |
| [Supabase](https://supabase.com) — sign up **with GitHub** | Login system + database | Free tier |
| [Anthropic Console](https://console.anthropic.com) | API key so the app can call Claude for readings/chat | ~USD $5 to start |

⚠️ The Anthropic Console is **separate from your Claude subscription** — it needs its own card and small credit top-up. Expect a few dollars total during development. Keep the API key private; Claude Code will tell you exactly which file to paste it into (never into the code itself).

## Step 1 — Create the project (5 min)

1. Create folder `C:\Users\Angela\Projects\astrology-app` — **not inside the Brain vault**; the vault is for notes, apps live in their own folders.
2. Open that folder in VSCode (File → Open Folder).
3. Start a Claude Code session there.

## Step 2 — Paste the super prompt

Copy everything below the `---` line in [[Ventures/Astrology App/Super Prompt|Super Prompt]] and paste it as your first message. Claude will build **Phase 1 only** (project skeleton + landing page + email waitlist) and then stop and tell you how to look at it.

## Step 3 — Test each phase like a user

After every phase Claude stops and tells you how to check its work (usually: run `npm run dev`, open `http://localhost:3000` in your browser, click around **on your phone-sized browser window too**). If something looks wrong, just describe it in plain English — "the button is cut off on mobile", "this wording feels cold". Then say "continue to the next phase".

In later sessions, start with: **"Read PROGRESS.md and continue with the next phase."** — that file is the app's own memory of where the build is up to.

## Step 4 — Go live early (end of Phase 1)

Deploy to Vercel as soon as the landing page exists. You get a real URL immediately. This matters because:

- **Validate while you build.** Post the concept on TikTok ("I'm building an app that reads your Western birth chart AND your 八字…") and point people at the waitlist. If the waitlist is dead after a few honest attempts, you've learned something cheap. Build-in-public content is also just good Ange.beee content — the build itself is a content series.
- A live link keeps you motivated and testable by friends at every phase.

## Step 5 — Phases 2–7

Roughly one phase per sitting. Realistic total: **2–4 weekends** to a testable MVP.

1. ~~Phase 1~~ — Skeleton + landing page + waitlist
2. Phase 2 — Sign-up/login + onboarding (birth details, personality type)
3. Phase 3 — The chart engines (Western chart + BaZi 八字, computed properly) + profile page
4. Phase 4 — "Know Yourself" core reading (AI synthesis)
5. Phase 5 — Daily card + monthly + yearly guidance
6. Phase 6 — AI chat with guardrails and free-tier limits
7. Phase 7 — Polish, disclaimers, privacy page, launch checklist

## Step 6 — Beta test

Give the link to 10–20 friends (ideally a mix who care about astrology, 八字, or personality tests). Watch them use it. Collect: what they screenshot (that's your shareable moment), where they get bored, whether the readings feel *about them* or generic. Generic readings are the #1 failure mode of this category — iterate on Phase 4/5 prompts until people say "how did it know that?"

## Step 7 — Later (only after traction)

- Custom domain (~USD $15/yr) once the name is chosen
- Payments (Stripe) for premium tier — deliberately not in MVP; validate desirability first
- Wrap as iOS/Android app with Capacitor; Apple Developer account is USD $99/yr — don't pay it before the web version proves itself
- v2: friends & compatibility (the social layer), push notifications, built-in personality quiz

## Things to keep in mind

- **Birth data is sensitive personal data.** It stays in Supabase with row-level security (the super prompt enforces this), and the app needs a simple privacy policy (Phase 7).
- **"MBTI" is a trademark** of The Myers-Briggs Company — the app says "personality type (16-type framework)" instead. Users self-select their type in v1; a built-in quiz is v2.
- **Fortune-telling tone rules** are baked into the super prompt: reflective and empowering, never fatalistic; no health/death/pregnancy predictions; not medical/financial/legal advice. This protects users *and* future App Store approval.
- **Cost control** is designed in: readings are generated once and cached (yearly once a year, daily once a day), only chat is metered, cheap model for small texts. Development cost ≈ a few dollars; running cost near zero until you have real users.

Related: [[Ventures/Astrology App/index|Astrology App]] · [[Ventures/Astrology App/Super Prompt|Super Prompt]]
