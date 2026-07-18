# Mandarin Kids App

*(working name — rename once the venture has a real name, same as [[Ventures/Meridian/index|Meridian]] did. Keep the brand string in one config file so a rename is a one-line change.)*

An **offline-first bilingual (English ↔ Mandarin) learning app for young heritage-speaker children**, sold to parents on a **buy-once, no-subscription, no-data-collection** promise. The parent is the buyer and account-holder; there are no child accounts, no chat, no ads, and nothing leaves the device. First language pack is Mandarin; the content-pack architecture makes adding more languages later cheap.

- **Stage:** Spec'd 2026-07-18 — [[Ventures/Mandarin Kids App/Build Plan|Build Plan]] + [[Ventures/Mandarin Kids App/Super Prompt|Super Prompt]] ready, awaiting build kickoff. Not yet built.
- **Origin:** Angela's market-research session on claude.ai web (Jul 2026), imported into the vault 2026-07-18. Research arc: mined complaint threads for solo-buildable gaps → narrowed to the intersection of two strong signals: (1) the **kids-learning** pain (parents want offline, no-subscription, privacy-safe apps and distrust billing-heavy incumbents) and (2) the **post-Duolingo language** gap (plateau/streak-anxiety backlash; heritage speakers and single language-pairs underserved).
- **Model:** One-time purchase ("buy once, own forever") — deliberately **not** a subscription. This is a positioning pillar, not just a price. Free v1 to validate demand; paid unlock added only once there's traction.
- **Platform decision (REVISED 2026-07-18, supersedes the PWA plan below):** **React Native + Expo (TypeScript), built entirely from Windows.** The fuller import of Angela's claude.ai web session revealed it had already moved past the SwiftUI recommendation to Expo — and Angela ratified that path there. Dev loop: code on Windows with Claude Code, test live on Angela's own iPhone via the free **Expo Go** app (scan a QR code, app live-updates on the phone — no simulator, no Mac). Shipping: **EAS cloud builds** compile the iOS binary on rented Macs and upload to Apple — no Mac ever needed. A Mac developer can join the project any time with zero conversion (standard React Native; git repo is fully portable).
  - **Why native won over the PWA plan:** the app's three core promises — offline reliability, one-time purchase, parent trust — are all stronger native on iOS (installed-PWA storage on iPhones is evictable/murky vs. native storage; App Store one-time purchase is the payment pattern parents already trust for kids apps; the **App Store Kids Category is itself a discovery + trust channel** for this exact buyer). The deferred v1.5 features (stroke tracing, speech) are also much stronger native. Expo solves the same no-Mac problem the PWA was solving, without giving up the native end-state.
  - **Costs specific to this path:** EAS free tier is limited (then ~US$19/mo or pay-per-build) — only bites when TestFlight shipping starts; Apple Developer **$99/yr becomes due at TestFlight time** (not launch). Expo Go testing is free.
  - **Validation funnel unchanged:** a simple landing page + waitlist on Vercel (same pattern as Meridian/TCM App) remains the TikTok-bio link while the native app is built. The app itself doesn't need to be web for the funnel to work.
- **Superseded (kept for reference):** the 2026-07-18 web-first PWA + Capacitor plan (see the superseded [[Ventures/Mandarin Kids App/Build Plan|Build Plan]] / [[Ventures/Mandarin Kids App/Super Prompt|Super Prompt]]). It was written before the web chat's Expo decision was known. Still a valid fallback if the Expo path ever proves unworkable.

## The product

A parent buys/installs the app for their pre-literate or early-reader child (roughly ages 3–7) to build and retain Mandarin. The child uses it **offline**, audio-first (so pre-readers can use it), through short, forgiving activities — no streaks, no timers, no punishment for missing a day. The parent controls what's active and sees light progress, behind a parent gate.

**Audience:** parents of young **heritage-speaker** children (Chinese-diaspora families who want their kids to acquire or keep Mandarin), plus non-heritage parents who want a calm, private early-Mandarin tool. The parent is always the user who pays and configures; the child only ever sees the learning flow.

**Positioning / the wedge (from the research):** deliberately narrow — **one language pair, one audience, one job done well.** Not "learn any language." The pitch is everything Duolingo-style apps are criticised for *not* being:

- **Offline** — works on a plane, a subway, a road trip, with no signal. Table stakes the incumbents fumble.
- **No subscription** — buy once, own forever. Directly answers the #1 parent complaint about kids apps (billing/renewal traps, "$13/mo for a 4-year-old's app").
- **No data collection, no ads, no chat** — nothing phones home. COPPA-safe by construction because there's no server and no personal data. This is also the entire *marketing* pitch, not a footnote.
- **No gamification-for-its-own-sake** — no streak anxiety, no energy/hearts system. Gentle, honest, calm.
- **Native-quality audio** — every clip recorded/verified by a native speaker. One wrong tone teaches a mistake, so audio correctness is sacred.

**Differentiator vs. free content + vs. Duolingo:** curation + calm + privacy + offline for a *specific* audience (heritage kids), sold once. The activities themselves (flashcards, matching) are commodities; the moat is the curated bilingual content pack, the trust/privacy stance, and the heritage-speaker focus.

## MVP scope (v1)

Deliberately small. Three activities, all fully offline, all audio-first:

1. **Flashcards (recognition)** — a card shows an image + hanzi + pinyin; tap to hear native audio; flip for the English word. Browse a deck by category/level.
2. **Audio–image matching game** — hear a word, tap the matching picture from 2–4 choices. Gentle "try again," never a punishing fail state. Difficulty scales by number of choices. No ML required.
3. **Parent mode + parent gate** — a parent gate (hold-to-enter or simple math, per Kids-Category norms) guards a parent area where the parent picks active categories/levels and sees light progress (words seen/practiced). All on-device.

**Content:** ~150-word starter curriculum across a few concrete-noun categories (animals, food, family, colours, numbers…), each with native Mandarin audio (~150–170 clips) and a consistent image. Authored in a spreadsheet → exported to a bundled JSON content pack (same "content is the product, author in a sheet" pattern as [[Ventures/TCM App/index|TCM App]]).

**Deliberately cut from v1 (see Backlog):** stroke-order tracing, speech/pronunciation practice, spaced-repetition scheduling, multiple child profiles, additional languages, the paid unlock. These are held back on purpose — tracing and speech are the two highest-risk features and were deferred in the research itself.

## Why this scope fits a solo, nights/weekends, no-code founder

- **No backend = no server bugs, no ongoing cost, no data-privacy surface.** The single biggest simplifier. Everything ships inside the app.
- **No accounts = no auth to build or secure.**
- **No runtime AI** — content is fixed and bundled, so unlike TCM App there isn't even a one-time AI generation step on the critical path. Running cost is ~$0 regardless of traffic.
- **The hard part is content, not code** — same lesson as TCM App. The curriculum + native audio + consistent images are the real work; Claude Code writes all the code.

## Market signal (from the research, treat as directional)

- **Kids-learning pain is billing/trust, not content quality.** 1-star reviews on top kids apps cluster on billing (trials charging early, annual renewals, cancellation friction) while the teaching is often fine. A child's interest fades in weeks but an annual sub runs a year — value-to-cost collapses before renewal. Parents explicitly ask for offline, no-subscription, no-data-collection apps. Trust gaps (COPPA gray areas, strangers messaging kids in some apps) deepen the demand for a visibly private, no-social product.
- **Language-learning "post-Duolingo" gap is the loudest of the researched areas.** Top complaint in 2026: high engagement, low actual proficiency (the "plateau"); streak anxiety and backlash to the 2025 energy-system overhaul; unmet demand for honest speaking feedback, offline reliability, learning one language *from another* without routing through English, and one-time pricing. Less-common language pairs and heritage speakers are underserved.
- **The category is crowded** — every individual gap has at least one startup attacking it (LingQ, Clozemaster, PolyChat, etc.). A solo builder wins **only by going narrow**: one language, one audience, one skill. This app's answer: Mandarin, heritage kids, recognition/listening — sold on offline + privacy + buy-once.
- **Competition to respect:** Khan Academy Kids (free, excellent — so compete on a specific niche it doesn't serve, i.e. heritage Mandarin, not general early learning); big kids-app publishers on billing-heavy models; existing Mandarin-for-kids apps (many subscription-based, online-required).

## Cost forecast (from the research, AUD/USD rough — get real quotes)

Infra is ~$0; **content is the cost driver.**

- **Native Mandarin audio (~150–170 short clips):** ~USD $150–500 for a pro voice actor, or ~free if a native-speaker friend/community member records it (a few hours of work, one-time).
- **Images (~100–150 concrete nouns):** the swing factor. Licensed consistent icon set ~$50–150; custom illustration $1,000–5,000+. AI-generated art is cheap but raises consistency + licensing concerns for a kids' product — tread carefully.
- **Curriculum sanity-check by a Mandarin tutor:** optional ~$100–300; **native-speaker proofread of every entry is non-negotiable** ($50–150, or free if done by a trusted fluent person). One wrong tone teaches a mistake.
- **Stroke-order data (only when tracing is built, v1.5):** ~$0 — open Chinese stroke datasets exist; check the licence.
- **Fixed:** Vercel (free Hobby tier bars commercial use, so ~$20/mo Pro once monetising); no Apple/Google fees while web-first (Apple $99/yr + Google $25 one-time only if/when wrapped native). The AI-assisted build is covered by the existing Claude subscription.
- **Realistic content spend:** ~$250 scrappy → ~$500–1,500 careful (most likely) → ~$6,000 if pro audio + custom illustration.

## Competitors (research 2026-07-18)

### Direct — Chinese/Mandarin-for-kids apps

| App | Model | What it does well | Gap vs. this app |
|---|---|---|---|
| **Studycat (Learn Chinese)** | Subscription ("Fun Five" bundle); has offline mode | Kid-first design, ad-free, immersion-only audio (no English spoken), polished, ~400 characters taught | Subscription, not heritage-specific, general beginner content not tuned for heritage retention |
| **iHuman Chinese** | **Lifetime one-time purchase** (~AUD $99.99 base, bundles ~AUD $125–157) | Deep content (1,300 characters), 130 leveled picture books, well-known in overseas-Chinese-parent circles | Not privacy/offline-first as a stated pitch; priced high for a single "unlock everything" purchase vs. this app's leaner scope; general learner not heritage-specific |
| **Maomi Stars** | Subscription (typical) | Explicitly serves **heritage families**, supports both Mandarin + Cantonese, both Simplified + Traditional | Not positioned on offline/privacy/no-subscription; broader multi-language ambition than a focused wedge |
| **Dot Languages** | Subscription (typical) | One of few apps offering Simplified/Traditional choice + **Zhuyin** for Taiwanese Mandarin learners, 14 interface languages | Same subscription-model complaint pattern as the rest; Mainland-Mandarin-centric despite the Zhuyin support |
| **Gus on the Go** | One-time purchase (typical for this app) | Native-speaker audio, traditional characters + Hong Kong phrasing (Cantonese-focused sibling apps exist), ~90–1200 word vocab depending on version | Narrower scope (vocabulary-only, no personalization); not marketed on privacy/offline as the core pitch |
| **DinoLingo** | Subscription | Ad-free, kid-safe, **no chat/pop-ups**, trusted by 100k+ families since 2010, broad language catalog including Cantonese | Not Mandarin-specialist (generalist across many languages so shallower per-language); still subscription-based |
| **HelloChinese** | Freemium/subscription | Strong speech recognition, native-speaker video, good for casual practice | Not kid-focused, not offline-first, not heritage-specific |

**The whitespace holds up:** iHuman proves parents will pay a one-time lifetime fee for Chinese-kids content (validates the pricing model), DinoLingo/Studycat prove "ad-free, no-chat, kid-safe" is a marketable pitch, and Maomi Stars/Dot Languages prove heritage-specific + Traditional/Zhuyin support is a real, served-but-not-dominated niche. **No competitor found combines all of: offline-first, one-time purchase, zero data collection stated as the core pitch, heritage-speaker focus, and deliberately anti-gamification design.** That combination is this app's actual differentiation — not any single feature alone.

### Broader — reputable general language-learning brands (the category this app is implicitly compared against)

| Brand | 2025-26 position | Model | Relevance |
|---|---|---|---|
| **Duolingo** | Category leader, ~$1.03B revenue 2025, highest usage by far | Freemium + "Super Duolingo" subscription | The gamification/streak model this app is explicitly positioned against; also owns **Duolingo ABC**, a free kids' reading app (adjacent, not Mandarin-for-heritage-kids, but worth knowing it exists if Duolingo ever extends into this niche) |
| **Babbel** | #2 by revenue | Subscription (~$9/mo+), structured/curriculum-based | Sets the "credible, structured" bar; not kids-focused |
| **Rosetta Stone** | Legacy leader since the 1990s | Historically lifetime-purchase-friendly; "Dynamic Immersion" method | Proves immersion-style (image-to-word, no translation) methodology works at scale — same principle this app's flashcards use |
| **Busuu** | Mid-tier, community-driven | Subscription | Native-speaker correction community model — not directly relevant to an offline kids app, but shows demand for native-speaker-verified content, which this app bakes in structurally instead |

**Read for positioning:** none of the reputable general-market leaders serve this niche (kids + heritage + offline + one-time-purchase) at all — they compete on adult-learner scale and engagement metrics, the opposite of this app's calm/offline/private stance. The real competitive set is the smaller Chinese-kids-app category above, not Duolingo-tier brands. Useful anyway as the credibility bar for production quality (audio, UX polish) and as "apps parents already trust the category of," which lowers the trust barrier for a new entrant.

## Open content decisions (settle during Phase 2, before recording audio)

- **Simplified vs. Traditional characters.** Heritage audiences split (Mainland = simplified; Taiwan/HK/many Cantonese-heritage families = traditional). **Design the content schema to hold both hanzi forms per word from day one** — cheap now, expensive to retrofit. Ship simplified as the default, with traditional as a toggle if time allows.
- **Pinyin vs. Zhuyin (bopomofo).** Taiwan uses zhuyin. Same principle: let the schema carry both romanisations; default to pinyin in v1.
- **Curriculum list.** Which ~150 words, which categories, which order/levels. This is Angela's + a native-speaker's call, not a code decision.
- **Voice.** One native voice actor for consistency; child-friendly, clear, standard tone. Decide accent/register (Mainland Putonghua default).

## Backlog — do NOT build in v1 (keep a `BACKLOG.md`)

Stroke-order tracing (v1.5, the fiddly touch-path feature) → speech/pronunciation practice with honest feedback (highest-risk, weak on web — a strong reason to consider native by then) → spaced-repetition review scheduling → traditional-character + zhuyin toggles (if not already shipped) → multiple child profiles → additional language packs (the architecture is built for this) → one-time paid unlock (Stripe on web, or App Store IAP if native) → **native app wrap via Capacitor for App Store/Play discovery + native billing** (no Mac needed — Capacitor + cloud build from Windows).

## Documents

**Canonical build kit lives in the claude.ai web session and is NOT yet imported into this vault** — produced there 2026-07-18, pending download/copy-in (see Tasks):

- Project **CLAUDE.md super prompt** — includes a "Future features (post-v1)" section (printable worksheets + additional games recorded as planned-but-gated behind "ship v1 first", with rules: read from the pack, never hardcode words, handle null-image cards, no streaks/no-shame, offline/no-data) and a "stay Expo Go compatible, no exotic add-ons" portability rule
- **No-Mac build guide** (Windows + Expo Go + EAS; uses a `later.md` file as the idea parking lot during the build)
- **Symmetric two-language content schema** (both languages first-class, per-card images, phrase audio)
- **292-word bilingual content list** with audio/image/license tracking — supersedes the ~150-word estimate below; awaiting native-speaker proofread before any audio is recorded

Superseded vault docs (written before the web chat's Expo decision was known; kept as fallback reference): [[Ventures/Mandarin Kids App/Build Plan|Build Plan]] · [[Ventures/Mandarin Kids App/Super Prompt|Super Prompt]] (both PWA-path)

**Key build decisions locked in:** **React Native + Expo (TypeScript)** built from Windows, tested on-phone via Expo Go, shipped via EAS cloud builds (see Platform decision above); **no backend, no accounts, no analytics** — content bundled in the app, progress in on-device storage, nothing leaves the device (this IS the privacy product); **language-agnostic engine reading from data packs** — activities read a shared card pool, so new languages are new content, not new code; **content authored in a spreadsheet** → validated content pack, same "content is the product" pattern as TCM App; **one-time-purchase model, never subscription** (a positioning pillar); **no runtime AI**; **new-feature discipline:** mid-build ideas go to `later.md`, and post-v1 features must obey the pack/no-shame/offline rules recorded in the project CLAUDE.md.

## Tasks

- [ ] **Pick the working scope name** (folder currently "Mandarin Kids App") and decide whether the eventual brand should stay Mandarin-specific or be language-neutral (the architecture supports more languages later)
- [ ] **Settle the two content-schema decisions** before recording audio: simplified/traditional (hold both), pinyin/zhuyin (hold both) — see Open content decisions
- [ ] Reuse existing accounts (GitHub, Vercel). **No Supabase/Anthropic key needed for the app itself** — the only optional backend use is a marketing-page email waitlist (can reuse the Supabase pattern, or skip and just link TikTok)
- [ ] **Import the web-chat build kit into the vault/project** (the canonical version — see Documents): download or copy from the claude.ai session the CLAUDE.md super prompt, the no-Mac build guide, the two-language schema, and the 292-word content list
- [ ] Create the project folder `C:\Users\Angela\Projects\mandarin-kids-app` (NOT inside the vault), install Node.js, open in VSCode, start Claude Code with the web kit's CLAUDE.md in place → run its Milestone 0 prompt (Expo scaffold, test on iPhone via Expo Go QR code)
- [ ] Line up the content: get the **292-word list native-speaker proofread** (the web chat's stated gate before any audio is recorded), then record audio (word + phrase clips), choose a consistent image source — runs in parallel with early milestones and is the real bottleneck
- [ ] Deploy Phase 1 to Vercel early for a TikTok-bio link (same funnel as Meridian/TCM App); validate parent demand before building all phases

## Notes / progress

- 2026-07-18: Venture created from the claude.ai web market-research session (previously undocumented — flagged by an exhaustive vault search that found no prior record). Research synthesised into this note; Build Plan + Super Prompt written (PWA path). **Corrected the research's platform recommendation** from native SwiftUI (impossible on Angela's Windows machine) to a web-first offline PWA, with native wrap deferred.
- 2026-07-18 (later): Fuller transcript of the web session imported — it had **already evolved past SwiftUI to React Native + Expo** (Angela ratified that path there: Expo Go on-phone testing, EAS cloud builds, no Mac) and produced a complete v1 kit (CLAUDE.md super prompt with future-features section, no-Mac build guide, symmetric two-language schema, 292-word content list). **Platform decision revised to Expo/React Native**; the vault's PWA-path Build Plan + Super Prompt marked superseded (kept as fallback). Claude Code review endorsed the switch on the merits: offline reliability, one-time purchase, and Kids-Category trust/discovery are all stronger native, and v1.5 tracing/speech need native anyway. Web kit artifacts still pending import into the vault.

Related: [[Ventures/index|Ventures]], [[Ventures/Meridian/index|Meridian]], [[Ventures/TCM App/index|TCM App]]
