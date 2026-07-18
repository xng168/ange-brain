# Mandarin Kids App — Build Plan

> ⚠️ **SUPERSEDED (2026-07-18).** This is the web-first **PWA** build plan, written before the claude.ai web session's Expo decision was known. The canonical path is **React Native + Expo** (Windows + Expo Go + EAS cloud builds) per that session's no-Mac build guide (pending import — see [[Ventures/Mandarin Kids App/index|the venture note]]). Kept as a fallback reference only.

Step-by-step plan for building the app with zero coding experience, using Claude Code as the builder. Read this first; the actual build instructions Claude follows are in [[Ventures/Mandarin Kids App/Super Prompt|Super Prompt]].

## The approach in one paragraph

Same model as [[Ventures/Meridian/index|Meridian]] and [[Ventures/TCM App/index|TCM App]]: you don't write code — Claude Code writes all of it. Your job is founder + product owner: paste the super prompt, test each phase on your phone-sized browser like a real parent/child would, say what feels wrong, and make product decisions when asked. The build is 7 phases with a hard stop after each. This app is **simpler than your other two in the ways that matter**: no login, no database, no server, no runtime AI. But it has one thing they don't — **it's the content that's hard**: the ~150 words, the native-speaker audio, and consistent images are the real work, and that happens outside Claude Code, in parallel with the build.

## Why web-first, not the SwiftUI the research suggested

Your market-research session recommended a native iPhone app in SwiftUI. **SwiftUI can only be built on a Mac, and you're on Windows — so that path is a dead end for you right now.** A web-based **PWA** ("Progressive Web App" — a website that installs to the home screen like an app and works offline) gives you everything v1 needs on the stack you already know:

- **Offline:** a "service worker" caches the whole app + all audio + images, so it works in airplane mode.
- **Installable:** parents tap "Add to Home Screen" and get an app icon — no App Store needed.
- **No subscription / buy once:** works fine on web.
- **No data collected:** there's no server, so nothing *can* leave the device — which is literally your marketing pitch.
- **Ships this month, ~$0 to run** — same instant-ship path as your other apps.

The only things a native app adds — App Store discovery, native billing, and the smoothest stroke-tracing/speech — are all things your research already **deferred** past v1. So going web-first costs you nothing now. **If the app takes off, we later wrap this exact same code into a real App Store / Google Play app using a tool called Capacitor — and that step can be done from Windows via cloud build, still no Mac required.** That's written into the backlog.

## Step 0 — Accounts (you already have these — ~2 min)

Reuse from your other builds. **No new accounts needed for the app itself:**

| Account | What it's for | Cost |
|---|---|---|
| GitHub | Code storage | Free |
| Vercel | Hosting; gives you a live URL | Free tier |

You do **not** need Supabase or an Anthropic key for this app — it has no backend and no runtime AI. (The one exception: if you decide to put an email waitlist on the marketing landing page, you can reuse the same Supabase insert-only pattern from TCM App. Optional — you can also just link your TikTok instead.)

## Step 1 — Create the project (5 min)

1. Make a new folder: `C:\Users\Angela\Projects\mandarin-kids-app` — **not inside the Brain vault** (the vault is for notes; apps live in their own folders, same rule as your other two apps).
2. Open that folder in VSCode (File → Open Folder).
3. Start a Claude Code session there.

## Step 2 — Paste the super prompt

Copy everything below the `---` line in [[Ventures/Mandarin Kids App/Super Prompt|Super Prompt]] and paste it as your first message. Claude builds **Phase 1 only** (project skeleton + installable offline PWA shell + landing page) and then stops and tells you how to look at it.

## Step 3 — Test each phase like a parent and a child

After every phase Claude stops and tells you how to check its work (`npm run dev`, open `http://localhost:3000`, click around **on a phone-sized browser window**). Two extra tests that matter for THIS app:

- **The airplane-mode test:** after loading the app, turn off your Wi-Fi/network and reload — it should still work. This is the core promise; check it every phase.
- **The "would a 4-year-old get it" test:** can you use the child screens by ear, with big taps, without reading instructions?

Describe anything that feels wrong in plain English, then say "continue to the next phase." In later sessions, start with: **"Read PROGRESS.md and continue with the next phase."**

## Step 4 — Go live early and validate demand in parallel

Deploy to Vercel as soon as the landing page exists in Phase 1 (Claude gives you the exact steps). Then:

- Use that link in your TikTok/IG bio and post heritage-parent-targeted content ("teaching my kid Mandarin — offline, no subscription, no ads"). Watch whether parents save/comment/sign up.
- If the interest is dead after a few honest attempts, that's a cheap, early signal — far cheaper than recording all the audio and building 7 phases first.

## Step 5 — Phases 2–7

Realistically **faster to code than your other apps** (no login, no database, no AI), but gated by content:

1. ~~Phase 1~~ — Skeleton + installable offline PWA shell + landing page
2. Phase 2 — Content pack schema + build pipeline + ~15–20 placeholder starter words
3. Phase 3 — Flashcards activity (the core recognition loop)
4. Phase 4 — Audio–image matching game
5. Phase 5 — Parent mode + parent gate + on-device progress
6. Phase 6 — Polish, kid-UX, offline hardening
7. Phase 7 — Launch prep (privacy page, how-to, final audio review, production deploy)

## Step 6 — The content (the real work — start it early, in parallel)

This isn't "building an app" — it's compiling the actual curriculum, and it can run alongside Phases 1–5. This is your bottleneck, so start now:

1. **Draft the ~150-word curriculum.** Concrete, picture-able nouns first (animals, food, family, colours, numbers, body parts, greetings). Get a native speaker or Mandarin tutor to sanity-check the list and the ordering.
2. **Settle two schema decisions before recording audio** (see the Open content decisions in [[Ventures/Mandarin Kids App/index|the venture note]]): simplified vs. traditional characters, and pinyin vs. zhuyin. The build stores *both* forms per word — you just choose the v1 default (recommended: simplified + pinyin).
3. **Record native audio** (~150–170 short clips). A native-speaker friend/community member recording clearly is fine and can be near-free; a pro voice actor is ~USD $150–500. **Every clip must be checked by a native speaker — one wrong tone teaches a mistake.**
4. **Source consistent images** (~100–150). One visual style across the whole set. A licensed icon set (~$50–150) keeps it consistent and cheap; custom illustration is far pricier; AI art is cheap but risks inconsistency/licensing issues for a kids' product — tread carefully.
5. Claude gives you the exact spreadsheet template in Phase 2. Fill it in, drop the audio + image files in the folder it tells you, run one command, and your words appear in the app. Re-run any time the sheet changes — no code touching.

## Step 7 — Beta test with real families

Give the link to 5–10 heritage-speaker parents with young kids. Watch: does the child actually tap and listen unprompted? Does the parent trust it (privacy/offline pitch landing)? Which words/categories do they want next? Is the audio unmistakably native and correct? Audio quality and "does my kid engage calmly without me hovering" are the make-or-break signals.

## Step 8 — Later (only after traction)

- One-time paid unlock (Stripe on web) — deliberately not in MVP.
- Custom domain (~USD $15/yr) once a real name is chosen.
- v1.5: stroke-order tracing; then speech/pronunciation practice (the point where a native app may finally be worth it).
- **Native App Store / Google Play wrap via Capacitor** — turns this web app into a store-listed app with native one-time billing, WITHOUT buying a Mac. You wrap the same code with Capacitor, and the iOS build runs on a cloud Mac: **Codemagic** or **Ionic Appflow** (both built for Capacitor) or **GitHub Actions macOS runners** compile and submit for you from your Windows machine. You'll need an **Apple Developer account ($99/yr)** and (for Android) a one-time **Google Play fee ($25)**; check current cloud-build free tiers when you get there. Note: Apple won't accept a bare website, but the Capacitor wrap is a real native app, which is accepted — this is a standard path. The build is kept Capacitor-compatible from day one (see architecture rule 2b in the Super Prompt) so this wrap stays a small, late step rather than a rewrite. Do it only once web validation proves parents want it.
- Additional language packs — the architecture is built so a second language is mostly new content, not new code.

## Things to keep in mind

- **The content is the product.** Same lesson as TCM App. The code is the easy part; the curriculum + native audio + consistent images are where your time and money go. Start the content early and in parallel.
- **No backend means no bugs to chase and no cost — but also no cloud save.** Progress lives on the one device. If a parent switches phones, progress resets. That's an accepted v1 tradeoff (and part of the privacy promise), not an oversight.
- **Audio correctness is sacred.** Budget for a native-speaker review pass before you ship a single word. This is the one place "good enough" isn't.
- **Resist gamification.** The whole pitch is being the calm, no-streak-anxiety alternative. If it ever feels tempting to add streaks/timers to boost "engagement," that's the competitor's playbook, not yours.
- **"Mandarin Kids App" is a generic working name** — fine for now, but pick a real (ideally language-neutral, since more languages can follow) name before a custom domain or logo. Keep the brand string in one config file so renaming is a one-line change.
- **Don't build v1.5/v2 features early.** Tracing and speech are the two hardest features and are deliberately deferred — building them now is the fastest way to stall.

Related: [[Ventures/Mandarin Kids App/index|Mandarin Kids App]] · [[Ventures/Mandarin Kids App/Super Prompt|Super Prompt]] · [[Ventures/Meridian/index|Meridian]] · [[Ventures/TCM App/index|TCM App]]
