# Mandarin Kids App — Super Prompt

How to use: create the folder `C:\Users\Angela\Projects\mandarin-kids-app` (NOT inside the Brain vault), open it in VSCode (File → Open Folder), start Claude Code there, and paste **everything below the line** as your first message. See [[Ventures/Mandarin Kids App/Build Plan|Build Plan]] for the surrounding steps.

---

You are my technical co-founder and lead engineer. I am a non-technical founder building my third app (Meridian and TCM App use the same web stack). You own every technical decision; I own the product. Work with me like this:

- **Explain in plain English.** Assume I have never coded. When you make a technical choice, one sentence on what it is and why — no jargon walls.
- **Build in phases, defined below. After each phase:** commit to git with a clear message, update `PROGRESS.md` (what's done, what's next, how to run and test the app), tell me exactly how to test what you built on my phone-sized browser window, then **STOP and wait for me**.
- **Never put secrets in code.** This app has no backend and needs no secret keys for its core features — if that ever changes, use `.env.local`, keep it gitignored, and tell me exactly what to paste where.
- If something I ask for is a bad idea, say so and propose better — don't silently comply.
- Keep a `DECISIONS.md` noting big technical choices in one line each, and a `BACKLOG.md` for the deferred features listed at the bottom, so future sessions have context.

## The product

**Name:** "Mandarin Kids App" (working name — keep all brand strings in one config file so a future rename is a one-line change).

An **offline-first bilingual (English ↔ Mandarin) learning app for young heritage-speaker children** (roughly ages 3–7), used by the child but **bought and configured by the parent**. The child practises Mandarin through short, gentle, audio-first activities that work with no internet connection. Sold on a promise the big language apps break: **buy once (no subscription), works offline, collects no data, no ads, no chat, no streak pressure.**

**This is a calm, private, offline learning tool — not a gamified engagement machine.** There are NO streaks, NO timers, NO hearts/energy system, NO leaderboards, NO push notifications, and NO punishing fail states. Do not build any of those. Missing a day costs the child nothing. If "engagement mechanics" seem tempting later, that's a deliberate anti-goal here — the whole positioning is being the opposite of that.

**Purpose:** be the trustworthy, private, offline place for a heritage-speaker family to build and keep a young child's Mandarin — positioned against subscription-heavy, online-required, data-hungry kids apps and against Duolingo-style streak anxiety.

**Differentiator:** curated bilingual content + native-quality audio + a visibly private, offline, buy-once product for a *specific* audience (heritage Mandarin kids). The activities (flashcards, matching) are commodities; the moat is the content pack, the trust/privacy stance, and the narrow audience focus.

**Audience:** parents of young heritage-speaker children who want their kids to acquire or retain Mandarin. The parent is always the user who pays and configures; the child only ever sees the learning flow.

## Non-negotiable architecture rules

1. **Fully offline. No backend. No accounts. No telemetry.** The app is a self-contained installable PWA. All learning content (words, audio, images) is bundled into the app and cached by a service worker so the app works completely in airplane mode after first load. All progress and settings are stored **on-device only** (IndexedDB for larger data, `localStorage` for simple settings). **Nothing about a user or a child ever leaves the device** — no analytics, no crash reporting SDKs, no third-party trackers, no fonts/scripts loaded from a CDN at runtime. This is the product's core promise, not an optimisation. If you would normally add an analytics or logging SDK, do NOT — ask me first.
2. **Installable + offline PWA is a Phase 1 requirement, not a finishing touch.** Set up the web app manifest + service worker in Phase 1 so "Add to Home Screen" works and the app loads with the network off from the very first phase. Every later phase must keep the airplane-mode test passing.
2b. **Stay Capacitor-compatible so the App Store door stays open.** I want the option to later wrap this exact codebase with Capacitor into a native iOS/Android app (built from Windows via a cloud Mac). So: keep the app a **static, client-rendered export** (Next.js `output: export` must keep working) — do NOT introduce server-only Next.js features (server actions, route handlers, server-side rendering on the read path, server image optimization) into the app itself. Any device capability should use web APIs that have a Capacitor plugin equivalent. Prefer relative asset paths. If a feature would require a server or break static export, flag it and ask me before building it. (The optional marketing waitlist page is exempt — but it must live outside the app bundle that gets wrapped.)
3. **Content is deterministic and bundled — authored in a spreadsheet.** Word data is authored in a CSV/Google Sheet with the fixed schema below, and a re-runnable build script turns it into a validated JSON content pack bundled into the app (e.g. `npm run build-content -- ./content/words.csv`). This — not a database, not an admin UI, not AI — is how content is added/edited. No runtime AI anywhere; the app never generates or alters learning content.
4. **Kid-safe by construction.** No ads, no chat, no social, no external links a child can reach, no in-app browser. Anything that leaves the child's learning flow (settings, "buy", any outbound link) sits behind a **parent gate** (hold-to-enter or a simple can't-be-solved-by-a-toddler math step, per App Store Kids-Category norms). Design as if this will one day ship in the App Store Kids Category.
5. **Audio-first for pre-readers.** The child audience can't read yet. Every activity must be usable by ear: big tap targets, a prominent "play audio" affordance on every card, minimal on-screen text in the child flow, no reliance on reading instructions.
6. **Native audio correctness is sacred.** One wrong tone teaches a child a mistake. The content pipeline must make it easy to see which entries have verified native-speaker audio vs. placeholder audio, and the build script should warn on any word missing its audio/image. Never auto-generate or synthesise Mandarin pronunciation to fill a gap.
7. **One-time-purchase model, never subscription.** v1 ships free (to validate). When monetised later it is a one-time unlock — design all copy and any future paywall around "buy once, own forever." Do not build subscription logic.
8. **Content schema holds both character forms and both romanisations.** Store simplified AND traditional hanzi, and pinyin AND zhuyin, per word — even though v1 displays simplified + pinyin by default. This is cheap now and expensive to retrofit; heritage audiences split on this.
9. **Mobile-first, young-child ergonomics.** Design every screen for a phone held by a small child or a parent: large tap targets (min ~64px), high contrast, generous spacing, forgiving hit areas. Test at 390px width.

## Tech stack (pinned — don't substitute; same core stack as Meridian + TCM App)

- Next.js (latest stable, App Router) + TypeScript + Tailwind CSS + shadcn/ui — configured so the app works as a static, client-rendered PWA (no server features required for the core app).
- PWA layer: web app manifest + a service worker that precaches the app shell and all content assets (audio + images) for full offline use. Use a well-supported approach (e.g. `next-pwa`/Workbox or an equivalent you trust); explain the choice in `DECISIONS.md`.
- On-device storage: IndexedDB (via a small, well-supported wrapper like `idb`) for progress; `localStorage` for simple settings. No database, no Supabase, no auth in the app.
- Audio: bundled audio files (MP3/AAC), played via the HTML5 `<audio>` / Web Audio API. Preload/caching handled by the service worker.
- Images: bundled, optimised (WebP), one consistent visual style across the word set.
- Deployed on Vercel as a static site — near-zero running cost.
- **Optional marketing landing page only:** a simple email waitlist may use the same Supabase insert-only pattern as TCM App, OR be skipped in favour of a plain "coming soon / follow on TikTok" page. The **app itself stays backend-free** regardless — keep any waitlist strictly on the marketing page, never wired into the child/learning flow.
- Design direction: warm, playful, calm, and trustworthy — soft rounded shapes, friendly colour, lots of whitespace, delightful-but-quiet feedback. Think "gentle Montessori", NOT "casino-bright rewards". Screens should look reassuring to a parent and inviting to a child.

## Content pack schema (starting point — refine as needed)

Author in a spreadsheet, one row per word:

- `id` (stable slug), `english`, `simplified` (hanzi), `traditional` (hanzi), `pinyin`, `zhuyin` (nullable), `category` (e.g. animals, food, family, colours, numbers, body, greetings), `level` (1–3, difficulty/order), `audio_file` (filename of the native Mandarin clip), `english_audio_file` (nullable), `image_file` (filename), `audio_verified` (yes/no — has a native speaker signed off), `notes` (nullable — for the reviewer)

The build script validates the sheet (every word has an image + a Mandarin audio file present; warns on `audio_verified = no`), copies assets into the app bundle, and emits a typed JSON content pack the app reads. Levels and category metadata (display names, order, icons) live in a small config file in the codebase, not the sheet.

## Phases

**Phase 1 — Skeleton + installable offline PWA shell + landing page.** Scaffold the project, git init, README/PROGRESS/DECISIONS/BACKLOG. Set up the PWA (manifest, icons, service worker) so the app installs to the home screen and loads offline from the start. Build a simple marketing landing page stating the promise ("Help your child learn Mandarin — offline, no subscription, no ads, no data collection. Buy once."), a couple of preview cards, and (optionally) an email waitlist on that page only. Acceptance: runs locally, looks great on a phone, "Add to Home Screen" works, and the page still loads with the network turned off (airplane-mode test), deploy-to-Vercel instructions written for me step-by-step.

**Phase 2 — Content pack schema + build pipeline + starter words.** Define the content schema above. Give me an exact spreadsheet column template to fill in. Build the re-runnable `build-content` script (validates, bundles assets, emits typed JSON; warns on missing/unverified assets). Seed ~15–20 starter words in ONE category (e.g. animals) with clearly-labelled placeholder audio + placeholder images so the whole pipeline is proven end-to-end before I invest in real recordings. Acceptance: I can edit the spreadsheet, run one command, and see the new words appear in the app; missing assets produce a clear warning.

**Phase 3 — Flashcards activity (the core recognition loop).** A deck browser (pick a category/level) and the flashcard itself: image + simplified hanzi + pinyin; a big tap-to-hear-native-audio control; flip to reveal the English word (and English audio if present); next/previous through the deck. Fully offline, big tap targets, audio-first. Acceptance: a child can flip through the starter deck and hear audio for each word, on a phone, with the network off.

**Phase 4 — Audio–image matching game.** Play a word's native audio, show 2–4 image choices, the child taps the matching picture. Gentle, encouraging feedback for correct; a soft "try again" (never a harsh fail, no score-shaming) for wrong. Difficulty scales by the number of choices. Pulls only from the categories/levels the parent has enabled. Acceptance: playable, genuinely fun, forgiving, fully offline.

**Phase 5 — Parent mode + parent gate + on-device progress.** A parent gate (hold-to-enter or simple math) guarding a parent area. In it: choose which categories/levels are active for the child, and see light progress (words seen/practised, per category) — all stored on-device, nothing uploaded. The child flow respects the parent's selection. Acceptance: the parent gate keeps a curious child out, settings + progress persist across a refresh and offline, and the child activities only show enabled content.

**Phase 6 — Polish, kid-UX, and offline hardening.** Big tap targets and audio-first everywhere, loading/empty/first-run states, delightful-but-calm feedback (no addictive loops), app icon + splash + themed install experience, accessibility pass (contrast, tap size, reduced motion), and a thorough offline audit — a real airplane-mode run through every screen with all content cached. Acceptance: airplane-mode test passes end-to-end with real content, the child flow is navigable by a pre-reader, and it feels polished and calm on a phone.

**Phase 7 — Launch prep.** A trivially short, honest privacy page ("This app has no accounts and no servers. It collects nothing and works offline. Your child's activity never leaves your device."), a short "how to use" for parents, a final content-pack review pass (confirm every shipped word has native-speaker-verified audio), and a Vercel production deploy checklist. Acceptance: a stranger can open the link, add it to their home screen, turn off the network, and use it with their child with zero rough edges.

## Tone & content guardrails (bake into every screen and any copy)

- Voice to parents: warm, calm, trustworthy, respectful of their time and their child's privacy. Lead with offline + no-subscription + no-data.
- Voice to children: gentle, encouraging, playful, never pressuring. Praise effort softly; never punish, shame, or create urgency.
- No dark patterns: no fake scarcity, no manipulative "your child will fall behind" fear copy, no nagging to buy, no interrupting the child's flow with upsells.
- Cultural care: correct, respectful representation of Mandarin and Chinese culture in words, images, and audio. Prefer a native-speaker reviewer's judgement over guessing.
- Never claim educational outcomes you can't support ("fluent in 30 days"). Frame honestly as practice and exposure.

## v1.5 / v2 backlog — do NOT build any of this yet, keep a `BACKLOG.md`

Stroke-order tracing (v1.5, the fiddly touch-path feature; open Chinese stroke datasets exist) → speech/pronunciation practice with honest feedback (highest-risk; weak on web — likely the trigger to consider a native wrap) → spaced-repetition review scheduling → traditional-character + zhuyin display toggles (schema already supports them) → multiple child profiles → additional language packs (architecture is built for this) → one-time paid unlock (Stripe on web, or App Store IAP if native) → native app wrap via Capacitor for App Store/Play discovery + native billing (buildable from Windows via cloud build — no Mac needed).

---

Start now with Phase 1. Before writing code, give me a two-paragraph plain-English summary of what Phase 1 will contain and how you'll make the app installable and offline-capable from the start. The landing page displays the name "Mandarin Kids App".
