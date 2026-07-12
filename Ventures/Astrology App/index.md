# Astrology App

Personalised astrology and self-knowledge app: fortune telling from your birth chart — **Western astrology + Chinese BaZi (八字)** — combined with your **personality type** (16-type / MBTI-style). Guidance from the stars and your fortune, personalised to who you actually are.

- **Stage:** Spec'd — build plan and super prompt ready (2026-07-12). Not yet named, not yet built.
- **Model:** Freemium — free profile + daily card; paid subscription for deep readings and unlimited AI chat.
- **Objective:** Know yourself → better relationships. Guidance for the year, month, and day.

## Positioning

The East-meets-West gap: Co-Star and Dimensional are Western-only. Good BaZi apps are Chinese-market only. Nobody does **Western chart + 八字 + personality type in one synthesis, in English** with a warm (not doom-y) tone. Angela can market to both cultural worlds through Ange.beee (lifestyle/travel/Chinese culture niche — perfect content fit).

## MVP scope (v1)

1. Onboarding: birth date/time/place (+ gender, needed for BaZi luck pillars 大运) + personality type
2. Your profile: Western natal chart + BaZi four pillars, computed properly (not by AI)
3. "Know Yourself" core reading — AI synthesis of all three systems
4. Guidance: daily card / affirmation, monthly direction, yearly outlook
5. AI chat to explore your fortune and personality (rate-limited on free tier)

**Deliberately cut from v1:** social/friends & compatibility (Dimensional's moat — needs a user base to be useful), push notifications, native App Store apps. All in v2 backlog inside [[Ventures/Astrology App/Super Prompt|Super Prompt]].

## Competitor research

- **Co-Star** — Western astrology, NASA ephemeris data, blunt/poetic daily push notifications, chart comparison with friends. Aesthetic: stark black/white, doom-adjacent tone. Weakness: Western-only, tone alienates people who want warmth.
- **Dimensional** — personality assessments (Big Five etc.), colourful profile, strong friend-compatibility social layer, premium subscription. Weakness: no astrology depth, no Chinese metaphysics.
- **The Pattern** — timing-based readings, deep relationship analysis. Same Western-only gap.
- **CHANI** — astrology + wellness, warm tone (closest tonal reference). Western-only.
- Chinese BaZi apps (测测, 问真八字 etc.) — deep 八字 but Chinese-language, dated UX, no Western/personality fusion.

## Key decisions made

- **Web app first, not App Store** — instant shipping, shareable link for TikTok, no $99 Apple fee or review queue. Wrap with Capacitor for stores only after traction.
- **Deterministic engine + AI interpreter** — charts are computed by real astronomy/calendar libraries; the AI only interprets structured chart data. AI never computes or invents chart positions.
- **Stack:** Next.js + TypeScript + Tailwind, Supabase (auth + database), Vercel hosting, Claude API for readings/chat. Details in [[Ventures/Astrology App/Super Prompt|Super Prompt]].
- **Safety/tone:** empowering and reflective, never fatalistic; no death/health/pregnancy predictions; "for reflection and entertainment" disclaimer (also required for app stores later).

## Documents

- [[Ventures/Astrology App/Build Plan|Build Plan]] — Angela's step-by-step, no coding experience assumed
- [[Ventures/Astrology App/Super Prompt|Super Prompt]] — paste into a fresh Claude Code session in a new project folder to build

## Open questions

- Real name for the app (then rename this folder) — tracked in [[Open Items]]
- Pricing point for premium (~USD $7–10/mo hypothesis, validate later)

Related: [[Ventures/index|Ventures]] · [[Content/index|Content]] (build-in-public marketing)
