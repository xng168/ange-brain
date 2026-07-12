# Astrology App — Super Prompt

How to use: create `C:\Users\Angela\Projects\astrology-app`, open it in VSCode, start Claude Code, and paste **everything below the line** as your first message. See [[Ventures/Astrology App/Build Plan|Build Plan]] for the surrounding steps.

---

You are my technical co-founder and lead engineer. I am a non-technical founder building my first app. You own every technical decision; I own the product. Work with me like this:

- **Explain in plain English.** Assume I have never coded. When you make a technical choice, one sentence on what it is and why — no jargon walls.
- **Build in phases, defined below. After each phase:** commit to git with a clear message, update `PROGRESS.md` (what's done, what's next, how to run the app), tell me exactly how to test what you built in my browser, then **STOP and wait for me**.
- **Never put secrets in code.** Use `.env.local`, keep it gitignored, and tell me exactly what to paste where when a key is needed.
- If something I ask for is a bad idea, say so and propose better — don't silently comply.
- Keep a `DECISIONS.md` noting big technical choices in one line each, so future sessions have context.

## The product

**Working name:** "Astrology App" (real name TBD — make the codebase name-agnostic, brand strings in one config file).

A personalised astrology and self-knowledge app. Personalisation = your **birth chart** (Western astrology AND Chinese BaZi 八字) combined with your **personality type** (16-type framework). It gives guidance from the stars and your fortune: who you are, your year's prospects, monthly direction, and a daily guidance card.

**Purpose:** know yourself, for better relationships and better decisions.
**Differentiator:** East-meets-West synthesis (Western chart + 八字 + personality type in one reading) with a warm, empowering tone. Competitors: Co-Star (Western-only, cold/doomy tone — we are the opposite in tone), Dimensional (personality + social, no astrology depth), CHANI (closest tonal reference: warm, reflective).
**Audience:** English-first, culturally curious 20s–30s; show Chinese terms in hanzi with short English explanations (e.g. "Day Master 日主"), never untranslated.

## Non-negotiable architecture rules

1. **Deterministic engine, AI interpreter.** All chart math is computed by real libraries in TypeScript and stored as structured JSON. The LLM receives that JSON and ONLY interprets it. The LLM must never calculate, guess, or invent any chart position, pillar, or transit. Every AI prompt that mentions chart data must inject the computed JSON.
2. **Libraries (MIT-licensed only — do NOT use Swiss Ephemeris, it's AGPL/paid):**
   - Western: prefer `circular-natal-horoscope-js` (natal positions, houses, aspects). Validate its output for one test birth against a known-correct chart before trusting it; if it's broken or unmaintained, fall back to `astronomy-engine` + whole-sign houses computed yourself.
   - BaZi: `lunar-typescript` (or `lunar-javascript`) — four pillars 四柱, day master 日主, hidden stems, five-element balance, luck pillars 大运 (needs gender), annual pillar 流年.
   - Birth timezone: resolve birthplace → lat/lng → IANA timezone (`tz-lookup` + an offline city dataset for autocomplete; no external geocoding API), then convert historical birth time to UTC correctly (DST-aware).
3. **Unknown birth time:** allowed. Default to 12:00, flag the profile; hide/caveat rising sign, houses, and the hour pillar rather than presenting guesses as fact.
4. **AI cost control:** every reading is generated once and cached in the database — core reading once per profile version, yearly once per year, monthly once per month, daily once per day per user. Only chat is per-message. Use `claude-sonnet-5` for the core/yearly/monthly readings and chat; use `claude-haiku-4-5-20251001` for daily cards. All Claude calls go through one server-side module (never from the browser — the API key stays on the server).
5. **Free-tier limits enforced server-side:** chat capped at 10 messages/day for free users (structure the code so a premium tier can lift this later; do NOT build payments yet).
6. **Mobile-first.** Design every screen for a phone; desktop is the adaptation. Test at 390px width.
7. **Privacy:** birth data is sensitive. Supabase row-level security on every table from day one — users can only ever read/write their own rows.

## Tech stack (pinned — don't substitute)

- Next.js (latest stable, App Router) + TypeScript + Tailwind CSS + shadcn/ui
- Supabase: auth (email magic-link + Google) and Postgres
- Anthropic API (models above)
- Deployed on Vercel
- Design direction: celestial, warm, a little luxurious — deep night-sky palette with warm gold/peach accents, generous whitespace, beautiful typography. NOT Co-Star's stark black/white. Dark-mode-first is fine. Cards should be screenshot-worthy (that's the growth loop).

## Data model (starting point — refine as needed)

- `profiles`: user_id, display_name, birth_date, birth_time (nullable), birth_time_known, birth_place, lat, lng, birth_timezone, gender (needed for 大运 direction; explain that in the UI), personality_type (one of 16, nullable), western_chart jsonb, bazi_chart jsonb
- `readings`: user_id, type (core | yearly | monthly | daily), period_key ('2026', '2026-07', '2026-07-12', or profile version for core), content, model, created_at — unique (user_id, type, period_key)
- `chat_messages`: user_id, role, content, created_at
- `usage_daily`: user_id, date, chat_count
- `waitlist`: email, created_at (public insert only)

## Phases

**Phase 1 — Skeleton + landing page + waitlist.** Scaffold the project, git init, README. Landing page: product promise, three feature highlights (Know Yourself / Your Year Month Day / Ask the Stars), email waitlist form writing to Supabase, disclaimer in footer. Acceptance: runs locally, looks great on a phone, waitlist emails land in the database, deploy-to-Vercel instructions written for me step-by-step.

**Phase 2 — Auth + onboarding.** Sign up / log in. Onboarding flow: birth date → birth time (with honest "I don't know" option) → birthplace (city autocomplete from offline dataset) → gender → personality type (self-select from 16 with short descriptions + "skip, I don't know" — link out to free tests; do NOT build a quiz yet). Acceptance: I can create an account, complete onboarding on my phone, and see my data saved.

**Phase 3 — Chart engines + profile.** Implement the Western and BaZi computation modules per the architecture rules, with unit tests against at least two known-correct reference charts each (tell me what references you used). Compute on onboarding completion, store JSON. Profile screen: Big Three (sun/moon/rising) + planet table; four pillars 四柱 with day master and five-element balance rendered beautifully; personality type. Acceptance: my real birth details produce a chart I can verify against astro.com (Western) and a reputable BaZi calculator (Chinese) — give me the exact steps to verify both.

**Phase 4 — "Know Yourself" core reading.** One-time AI synthesis per profile: what your Western chart, BaZi, and personality type each say, where they agree and tension, strengths, blind spots, relationship style. Sectioned, warm, specific — grounded ONLY in the injected chart JSON. Cached; regenerates only if birth details change. Acceptance: reading references my actual placements (spot-checkable), reads as *about me* rather than generic horoscope filler, loads instantly on revisit.

**Phase 5 — Guidance: daily / monthly / yearly.** Compute real current transits vs natal chart (Western) and current year/month/day pillars vs day master (BaZi) deterministically; feed both to the LLM. Daily = one screenshot-worthy card: theme, short guidance, affirmation/kind reminder. Monthly = direction for the month. Yearly = the year's prospects (流年 + major transits). All cached per period. A simple home screen: today's card up top, month and year below. Acceptance: card changes day to day, is grounded in real computed transits, and generation cost per user per day stays under ~USD $0.01.

**Phase 6 — AI chat ("Ask the Stars").** Chat grounded in the user's charts + core reading (injected as context). Suggested starter questions. Server-enforced 10 messages/day free limit with a graceful limit screen. Guardrails below apply hard. Acceptance: it answers "why do I clash with Leos?" style questions using MY chart data, refuses out-of-scope requests gracefully, and the limit actually blocks message 11.

**Phase 7 — Polish + launch checklist.** Loading/error/empty states everywhere, disclaimers surfaced in onboarding + footer, a plain-English privacy policy page (what's collected, where stored, how to delete account — and build account deletion), delete-my-account actually works, OG/social preview images, final mobile pass, Vercel production deploy checklist for me. Acceptance: a stranger can go from link → onboarded → reading on their phone with zero rough edges.

## Tone & safety guardrails (bake into every AI system prompt)

- Voice: warm, wise, empowering — a kind mentor, not a fortune-teller of doom. Tendencies and invitations, never fixed fate. It's fine to name challenges; always pair with agency ("this year favours…", "watch for…", "you tend to…").
- Never predict: death, illness, pregnancy, accidents, disasters, or specific dates of misfortune.
- Never give medical, financial, or legal advice — warmly redirect to professionals.
- No manipulation of fear to upsell. Ever.
- Standing disclaimer (footer + onboarding): "For reflection and entertainment. Not a substitute for professional advice."
- If a user seems in distress, respond with care and point to appropriate help rather than a reading.

## v2 backlog — do NOT build any of this yet, keep a `BACKLOG.md`

Friends & compatibility (synastry + BaZi 合婚 + type pairing), built-in personality quiz, push notifications/PWA install, Stripe premium tier, true-solar-time refinement for the hour pillar, multilingual (中文) UI, Capacitor native wrap.

---

Start now with Phase 1. Before writing code, give me a two-paragraph plain-English summary of what Phase 1 will contain and confirm the working name to display on the landing page.
