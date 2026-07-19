# Mandarin Kids App

*(folder is a working descriptor; the build kit's working title is **"Heritage Words"**. Rename once a real name is chosen — keep the brand string in one config file so a rename is a one-line change, same as [[Ventures/Meridian/index|Meridian]] did.)*

An **offline iOS app that teaches heritage-language children to *read* a language they already *speak*.** v1 ships one language pack: **Mandarin (simplified) + English**, for kids roughly **ages 5–10** who talk with their family in Mandarin but can't read a single character beyond 一二三. The app maps words the child already knows by ear onto their written form. The emotional promise to the parent: **"your kid will be able to read a message from grandma."** Sold on a **buy-once, no-subscription, no-ads, no-data-collection** pledge. The parent buys and configures; the child only sees the learning flow.

- **Stage:** **M0–M6 built (2026-07-19) — all of v1's buildable-without-real-content work is done.** Pinned to Expo SDK 54 (App Store's approved version; scaffold defaulted to 57, which Apple hadn't approved yet — old SDK 57 state tagged `sdk-57-scaffold` in git for later). Phase 0 validation running in parallel (Angela). Latest commit `50f8324`.
  - **Device-testing troubleshooting (2026-07-19, ongoing):** Angela's first real-device connection attempt surfaced a chain of environment issues, each diagnosed and fixed in turn: (1) PowerShell script execution disabled by default on Windows → fixed via `Set-ExecutionPolicy -Scope CurrentUser RemoteSigned`; (2) plain LAN `npm start` failed to connect → tried tunnel mode as a workaround; (3) the disk was essentially full (316KB free of 476GB) causing a silent, partial `@expo/ngrok` install (the actual `ngrok.exe` binary — an npm optionalDependency — failed to download but npm reported success) → freed via Windows' Disk Cleanup "Clean up system files" (System Restore had consumed the bulk of it) → repaired via `npm install` once space existed; (4) a stale cached tunnel URL in Expo Go (`ERR_NGROK_3200`, ngrok's free/anonymous tunnels are known to be flaky) → force-quitting Expo Go and rescanning fixed the immediate case; (5) an active VPN (Astrill) was identified as a likely LAN-connectivity blocker (VPNs commonly break same-network device discovery) — disconnected, but connection still not yet confirmed working end-to-end as of this session's pause. **Not yet resolved: Angela has not yet seen the app running on her physical iPhone.** Resume from here next session.
  - **Disk space needs periodic rechecking** on this machine (`df -h /c/`) — was critically low once already; freed to 7.7GB then already back down to ~2.6GB from normal dev work. All four v1 activities live on placeholder content: flashcards (M2), Listen & Tap recognition (M3, with on-device progress + invisible spaced repetition), matching game (M4), and **Family Challenge** (M5 — Angela's own design: turn-based two-player, first to 10, implemented no-shame). Latest commit `e588c80`. Next build: M6 parent area + gate. M7 (real content) blocked on the proofread/audio/image gates; M8 (ship) blocked on device testing. Earlier detail below. Expo project at `C:\Users\Angela\Projects\mandarin-kids-app` (SDK 57 / RN 0.86, TypeScript). M0 skeleton + M1 pack engine (loader, plain-English validation, debug screen) done, verified (typecheck, iOS bundle, broken-pack validator test), committed (`main` @ `e2403b6`). Phase 1 content QA passed (292-word list clean; sandhi attention list generated). The paper-test PDF was regenerated for Phase 0 — `build-kit/paper-test-cards.pdf` (it never existed on disk; only its build script survived the export). **Gates open:** native-speaker proofread (before any audio), Angela's Expo Go phone test, Phase 0 go/no-go. **Next build:** M2 flashcards. Build kit reconstructed from the claude.ai web session lives in `build-kit/` (see Documents).
- **Origin:** A claude.ai web market-research session (Jul 2026), reconstructed into the vault 2026-07-18 from the account data export. Research arc: mined complaint threads for solo-buildable gaps → narrowed to the intersection of two strong signals — (1) the **kids-learning** pain (parents want offline, no-subscription, privacy-safe apps) and (2) the **post-Duolingo language** gap (heritage speakers underserved). The session then converged on the sharpest wedge inside that: **heritage kids who speak but can't read**, which no incumbent serves well.
- **Model:** One-time purchase (~USD $15–25), **never a subscription** — a positioning pillar, not just a price. Directly answers the #1 parent complaint about kids apps (billing/renewal traps).
- **Platform:** **React Native + Expo (TypeScript), built entirely from Windows**, iOS-first (iPhone + iPad). Dev loop: code on Windows with Claude Code, test live on a real iPhone via the free **Expo Go** app (QR code, live reload — no simulator, no Mac). Shipping: **EAS cloud builds** compile the iOS binary on rented Macs and submit to Apple — no Mac ever needed. The codebase is deliberately kept **web-compatible** so the same code can also run as a **PWA beta channel** (a shareable URL for cheap, wide, pre-App-Store testing — see Roadmap Phase 6). A Mac developer can join the project any time with zero conversion.
  - **Why not native SwiftUI (the research's first idea):** SwiftUI needs a Mac + Xcode, impossible on Angela's Windows machine. Expo removes the Mac dependency while still shipping a real native App Store app — the best of both.
  - **Costs specific to this path:** Apple Developer **$99/yr** only from Phase 6 (TestFlight); EAS free tier works (~$19/mo optional to speed builds during the shipping month); **$0 servers forever** (no backend). Content is the real spend.

## The product

A parent installs the app for a child (~5–10) who **speaks Mandarin at home but can't read it**. The child practises **offline**, audio-first, through short, gentle activities that map a spoken word they already know ("māma!") to its character. Anti-goal that shapes the whole tone: it must **never feel like the Saturday-school drilling these families resent** — no shame, no streaks, no timers, no punishment. The parent controls what's active and sees light progress behind a parental gate.

**Audience:** heritage-language families (Chinese-diaspora households) whose kids can speak but not read/write. The parent is always the buyer/configurer; the child only ever sees the learning flow. Existing apps fail this audience by starting from zero ("this is how you say hello!"), which bores a fluent-speaking child, or by feeling like homework.

**Positioning / the wedge:** deliberately narrow — **one language pair, one audience, one job done well.** The pitch is everything Duolingo-style apps are criticised for *not* being: **offline · no subscription · no data collection · no ads · no chat · native-quality audio · calm (no streak anxiety).** COPPA-safe *by construction* because there is no server and no personal data.

**Differentiator:** the specific audience (heritage kids who speak-but-can't-read) + the calm/private/offline/buy-once stance + a language-agnostic engine that makes future language packs pure content work. The activities themselves (flashcards, matching) are commodities; the moat is the curated bilingual content pack, the trust posture, and the narrow focus.

## MVP scope (v1) — from the build kit's CLAUDE.md

**In** (all fully offline, audio-first, no-shame):

1. **Flashcard browser** — card shows character + pinyin + English with audio in *both* languages; flippable; filter by level/category; a learning-direction toggle (study either language from the other).
2. **Recognition game** — hear a word → tap the right character from 3–4 options; gentle feedback; feeds progress.
3. **Matching game** — memory-style pairing of cards (uses the per-card images where present).
4. **Parent-child mode** — two-player co-op on one device (e.g. parent reads the English prompt aloud, child finds the character); designed for laps and couches, celebrates joint wins.
5. **Parent area (behind a parental gate)** — per-character progress (solid / shaky / not seen), one weekly off-screen suggestion tied to a learned word, settings.
6. **Spaced repetition under the hood** — invisible to the child; a missed word is quietly rescheduled, never punished.

**Out (v1.5+, do not build even if asked casually):** writing/tracing, speech recognition, traditional-character pack, additional languages, cloud sync, notifications. (Android is cheap later since the stack is cross-platform — but stay iOS-first for v1.)

**Content:** a **292-word list** across **15 categories** and **4 levels** (First Words → Everyday Words → Around Me → Putting It Together / short phrases). **211 concrete words carry an image; 81 abstract words are correctly image-free.** Both languages are fully recorded (~**584 audio clips** total). Authored in `heritage-words-content-list.xlsx`; a **native-speaker proofread is a hard gate before any audio is recorded.**

**Hard architecture constraints (from CLAUDE.md — non-negotiable):** fully offline, no backend, no accounts · zero data collection (App Store label "Data Not Collected"), no third-party SDKs/analytics · Kids-Category compliant (parental gate on settings/links/purchase; no ads) · **language-agnostic engine** — zero hardcoded words/characters/levels/categories, everything read from the pack per the schema · never hardcode the number of levels or categories · **one-time purchase, no subscription code ever.**

## Why this scope fits a solo, nights/weekends, no-code founder

- **No backend = no server bugs, no ongoing cost, no data-privacy surface.** Everything ships inside the app.
- **No accounts = no auth to build or secure.**
- **No runtime AI** — content is fixed and bundled. Running cost ~$0 regardless of installs.
- **The hard part is content, not code** — the 292-word curriculum, native audio (both languages), and consistent images are the real work; Claude Code writes all the code.

## Decisions locked (from the schema's "Decisions locked" section)

- **Simplified vs. Traditional → two separate packs**, not a `text_alt` toggle. A family picks at install: v1 ships `zh-hans-en` (simplified); a `zh-hant-en` traditional pack is future work. (This supersedes the earlier "hold both forms in one pack" idea.)
- **Level-4 phrase audio → one file per whole phrase** (simpler to record; teaches natural phrase rhythm/tone flow).
- **Images → a standard per-card field**: one image per concrete word, `null` for abstract words, one consistent commercially-licensed visual style, source/licence tracked per word in the spreadsheet.
- **Symmetric two-language schema:** `language_1` and `language_2` carry identical fields (each with its own text, audio, script flags), so which language the child is learning is a runtime setting, and a future Spanish/English or Korean/Japanese pack drops in with no code change.
- **Pinyin is the v1 romanisation** (zhuyin deferred with the traditional pack).

## Market signal (from the research, treat as directional)

- **Kids-learning pain is billing/trust, not content quality.** 1-star reviews on top kids apps cluster on billing (trials charging early, annual renewals, cancellation friction) while the teaching is often fine. A child's interest fades in weeks but an annual sub runs a year — value-to-cost collapses before renewal. Parents explicitly ask for offline, no-subscription, no-data-collection apps.
- **Language-learning "post-Duolingo" gap is the loudest of the researched areas:** high engagement but low real proficiency (the "plateau"); streak anxiety; unmet demand for offline reliability, honest feedback, learning one language *from another*, and one-time pricing. Less-common pairs and **heritage speakers are underserved.**
- **The category is crowded** — a solo builder wins **only by going narrow**: one language, one audience, one job. This app's answer: Mandarin, heritage kids who speak-but-can't-read, recognition/reading — sold on offline + privacy + buy-once.
- **Competition to respect:** Khan Academy Kids (free, excellent — so compete on the specific niche it doesn't serve); big kids-app publishers on billing-heavy models; existing Mandarin-for-kids apps (mostly subscription/online-required, and mostly start from zero rather than serving a fluent-speaking child).

## Cost forecast (rough — get real quotes)

Infra ~$0; **content is the cost driver.**

- **Native audio (~584 clips: ~292 Mandarin + ~292 English):** near-free if a native-speaker friend records it (a few hours), or ~USD $150–500+ for a pro voice actor. A warm human voice matters most on the Mandarin side.
- **Images (211 concrete words):** licensed consistent icon set ~$50–150; custom illustration far more. AI art is cheap but risks consistency/licensing issues for a kids' product — tread carefully. Log every image's source + licence (spreadsheet has a column).
- **Native-speaker proofread of every character/pinyin/tone/meaning:** non-negotiable gate; ~$50–300 or free if done by a trusted fluent person. One wrong tone teaches a mistake.
- **Fixed:** Apple Developer $99/yr (from Phase 6 only); EAS $0–19/mo (shipping month only); $0 servers. The AI-assisted build is covered by the existing Claude subscription.
- **Total cash to v1:** roughly **USD $500–2,000** depending on content choices, plus your time (budget 3–5 months of nights/weekends).

## Competitors (research 2026-07-18)

### Direct — Chinese/Mandarin-for-kids apps

| App | Model | What it does well | Gap vs. this app |
|---|---|---|---|
| **Studycat (Learn Chinese)** | Subscription ("Fun Five" bundle); has offline mode | Kid-first design, ad-free, immersion-only audio (no English spoken), polished, ~400 characters | Subscription; not heritage-specific; starts from beginner, not tuned for a fluent-speaking child |
| **iHuman Chinese** | **Lifetime one-time purchase** (~AUD $99.99 base, bundles ~AUD $125–157) | Deep content (1,300 characters), 130 leveled picture books, known in overseas-Chinese-parent circles | Not privacy/offline-first as a pitch; priced high; general learner, not heritage-reading-specific |
| **Maomi Stars** | Subscription (typical) | Explicitly serves **heritage families**, supports Mandarin + Cantonese, both Simplified + Traditional | Not positioned on offline/privacy/no-subscription; broader ambition than a focused wedge |
| **Dot Languages** | Subscription (typical) | Simplified/Traditional choice + **Zhuyin** for Taiwanese learners, 14 interface languages | Same subscription pattern; Mainland-Mandarin-centric despite Zhuyin support |
| **Gus on the Go** | One-time purchase | Native-speaker audio, traditional characters + Hong Kong phrasing | Narrower (vocabulary-only, no personalization); not privacy/offline-marketed |
| **DinoLingo** | Subscription | Ad-free, kid-safe, no chat/pop-ups, trusted by 100k+ families since 2010, includes Cantonese | Generalist across many languages (shallower per-language); still subscription |
| **HelloChinese** | Freemium/subscription | Strong speech recognition, native-speaker video | Not kid-focused, not offline-first, not heritage-specific |

**The whitespace holds up:** iHuman proves parents will pay a one-time fee for Chinese-kids content (validates pricing); DinoLingo/Studycat prove "ad-free, no-chat, kid-safe" sells; Maomi Stars/Dot Languages prove heritage-specific + Traditional/Zhuyin is a real, served-but-not-dominated niche. **No competitor combines all of: offline-first, one-time purchase, zero data collection as the core pitch, the speak-but-can't-read heritage focus, and deliberately anti-gamification design.** That combination is the differentiation — not any single feature.

### Broader — reputable general language-learning brands (the implicit comparison set)

| Brand | 2025–26 position | Model | Relevance |
|---|---|---|---|
| **Duolingo** | Category leader, ~$1.03B revenue 2025, highest usage | Freemium + subscription, gamified | The streak/gamification model this app is explicitly positioned against; also owns **Duolingo ABC** (free kids' reading — adjacent, worth watching) |
| **Babbel** | #2 by revenue | Subscription (~$9/mo+), structured | Sets the "credible, structured" bar; not kids-focused |
| **Rosetta Stone** | Legacy leader since the 1990s | Historically lifetime-purchase-friendly; "Dynamic Immersion" | Proves image-to-word immersion works at scale — the same principle behind the flashcards/recognition game |
| **Busuu** | Mid-tier, community-driven | Subscription | Shows demand for native-speaker-verified content, which this app bakes in structurally |

**Read for positioning:** none of the big brands serve this niche — they optimise for adult-learner scale and engagement metrics, the opposite of this app's calm/offline/private stance. They matter as the production-quality bar and as proof the category is trusted, which lowers the trust barrier for a new small entrant.

## Backlog / future features (from CLAUDE.md — do NOT build in v1; parked in `later.md` during the build)

Every future feature must still obey the v1 rules (reads from the pack, handles null-image cards, no streaks/no-shame, offline/no-data, Kids-Category compliant, works from pack data so it supports every language pack). Known items: **more games** (listening quizzes, category sorting, sentence-building — new screens on the shared card pool) → **writing/tracing** (v1.5; uses the pack's `stroke_data`; confirm stroke-data licence first) → **printable worksheets** (architecturally different — a *generated PDF*, its own sub-project; reuses stroke data) → **traditional-character pack (`zh-hant-en`) + additional language packs** (pure data, the payoff of the language-agnostic engine) → speech/pronunciation practice → cloud sync → notifications → Android build.

## Documents

**Canonical build kit — reconstructed from the web session and imported to `Ventures/Mandarin Kids App/build-kit/` (2026-07-18):**

- **`build-kit/CLAUDE.md`** — the super prompt / project brain; Claude Code auto-reads it each session. Hard constraints, tech stack, v1 scope, milestones M0–M8, "Future features (post-v1)" rules.
- **`build-kit/language-pack-schema.md`** — the symmetric two-language data format all content follows; the second source-of-truth read alongside CLAUDE.md.
- **`build-kit/build-guide.md`** — the no-Mac Windows/Expo day-to-day operating guide (install, Expo Go loop, EAS/TestFlight, working with outside developers).
- **`build-kit/master-roadmap.md`** — the single ordered plan from today to launch (Phases 0–8), orchestrating the Build track and Content track in parallel.
- **`build-kit/validation-kit.md`** — the Phase 0 validation sprint: where to post, a parent-interview script, the go/no-go scorecard. Companion to the landing page.
- **`build-kit/landing-page.html`** — the Phase 0 validation landing page (replace `YOUR_FORM_ID` with a Formspree ID; also measures the simplified-vs-traditional split).
- **`build-kit/heritage-words-content-list.xlsx`** — the 292-word content list + audio/image/licence tracker (Read Me + Word List sheets; yellow columns are the native-speaker reviewer's).

Superseded vault docs (my earlier PWA-path speculation, written before the real kit was in hand; kept as fallback reference only): [[Ventures/Mandarin Kids App/Build Plan|Build Plan]] · [[Ventures/Mandarin Kids App/Super Prompt|Super Prompt]].

**Provenance (settled 2026-07-19):** the kit was first *reconstructed* from the export's tool-command history (the export contains commands, not rendered files). Angela then downloaded the **original five output files** from the claude.ai session into `_sources/App files/`. A full diff — every markdown file and all 293×12 spreadsheet cells — found the reconstruction **byte-identical** to the originals (trailing newline only). The originals are now the canonical copies in `build-kit/` and in the project. Three artifacts remain reconstruction-only (not in Angela's download, verified by replay): `validation-kit.md`, `landing-page.html`, and the regenerated `paper-test-cards.pdf`.

## Tasks

- [ ] **Phase 0 — validate demand first** (per `validation-kit.md`): host `landing-page.html` (Netlify Drop + a Formspree form), post the interview-style questions in heritage-parent communities, talk to ~10 parents, optional paper-card test. Go/no-go: ~100 genuine signups or 5/10 parents saying "I'd pay today."
- [ ] **Native-speaker proofread of the 292-word list** (hard gate) — every character, pinyin, tone, English meaning; watch tone sandhi (不/一, 3rd-tone pairs) and neutral tones. **Nothing gets recorded until this is done.**
- [ ] Install toolchain: paid Claude plan, Node.js (LTS), Claude Code, Expo Go on the iPhone. Put `CLAUDE.md` + `language-pack-schema.md` in the project folder.
- [x] **M0 built (2026-07-18):** Expo project at `C:\Users\Angela\Projects\mandarin-kids-app`, build kit installed, 20-card placeholder pack, home screen, iOS bundle verified, committed (`main`, `3f05df5`).
- [ ] **Angela: see it on your phone** — install Expo Go, run `npm start` in the project folder, scan the QR code (phone + PC on same Wi-Fi). Success = the "Heritage Words" home screen appears.
- [ ] **M1 — pack engine:** open the project folder in a *fresh* Claude Code session (so its own CLAUDE.md governs) and say "Read PROGRESS/CLAUDE.md and build M1." Loader that parses/validates the pack and exposes cards/levels/categories, with a debug screen.
- [ ] Content track (parallel, the real bottleneck): line up the native recorder for ~584 clips, choose a licensed image set for the 211 concrete words, log each image's licence.
- [ ] Decide the real name (kit uses working title "Heritage Words"); consider a language-neutral name since more packs can follow. Keep the brand string in one config file.

## Notes / progress

- 2026-07-18: Venture created from a claude.ai web market-research session (previously undocumented). Initial spec written from the *pasted* chat; platform corrected SwiftUI → (PWA →) **Expo/React Native**.
- 2026-07-18 (M0): Kicked off the build. Scaffolded the Expo app (`create-expo-app`, blank-typescript, SDK 57 / RN 0.86) at `C:\Users\Angela\Projects\mandarin-kids-app`; installed the reconstructed build kit (CLAUDE.md + schema at root, reference docs in `docs/`); added a 20-card placeholder pack conforming to the symmetric two-language schema (15 with images, 5 abstract/null-image), a `src/config.ts` brand config, a calm home screen, and `content-todo.md` + `later.md`. Verified: TypeScript typechecks clean and the app bundles for iOS (582 modules, clean `expo export`). Committed to git (`main`, `3f05df5`). Not yet run on a physical device — that's Angela's Expo Go test. Confirmed the build uses the **verified reconstruction** (the browser's literal output files were not in the export and aren't on the machine).
- 2026-07-18 (later): Full account data export imported. The web session's actual build kit — **CLAUDE.md, language-pack-schema.md, build-guide.md, master-roadmap.md, validation-kit.md, landing-page.html, and the 292-word .xlsx** — was **reconstructed from the export's tool-command history** (the rendered files weren't in the export) and placed in `build-kit/`. A verification pass caught and fixed a gap where an inline-Python cleanup step (message 58) hadn't been replayed, which had left CLAUDE.md/schema/build-guide with stale "Xcode"/"~150-word" content; after re-applying it, the kit matches the session's own final state. This note (`index.md`) was then rewritten to match the authoritative kit — correcting earlier speculation (the real product is **292 words, ages ~5–10, "speaks but can't read", 5 activities + spaced repetition**, not ~150 words / ages 3–7 / 3 activities). The PWA path is retained not as the primary plan but as a **beta channel** (Roadmap Phase 6, Route A). Raw export archived (gitignored) in `_sources/Export Data 18072026/`.

Related: [[Ventures/index|Ventures]], [[Ventures/Meridian/index|Meridian]], [[Ventures/TCM App/index|TCM App]]
