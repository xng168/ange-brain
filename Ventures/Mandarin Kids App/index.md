# Mandarin Kids App

*(working name — rename once the venture has a real name, same as [[Ventures/Meridian/index|Meridian]] did. Keep the brand string in one config file so a rename is a one-line change.)*

An **offline-first bilingual (English ↔ Mandarin) learning app for young heritage-speaker children**, sold to parents on a **buy-once, no-subscription, no-data-collection** promise. The parent is the buyer and account-holder; there are no child accounts, no chat, no ads, and nothing leaves the device. First language pack is Mandarin; the content-pack architecture makes adding more languages later cheap.

- **Stage:** Spec'd 2026-07-18 — [[Ventures/Mandarin Kids App/Build Plan|Build Plan]] + [[Ventures/Mandarin Kids App/Super Prompt|Super Prompt]] ready, awaiting build kickoff. Not yet built.
- **Origin:** Angela's market-research session on claude.ai web (Jul 2026), imported into the vault 2026-07-18. Research arc: mined complaint threads for solo-buildable gaps → narrowed to the intersection of two strong signals: (1) the **kids-learning** pain (parents want offline, no-subscription, privacy-safe apps and distrust billing-heavy incumbents) and (2) the **post-Duolingo language** gap (plateau/streak-anxiety backlash; heritage speakers and single language-pairs underserved).
- **Model:** One-time purchase ("buy once, own forever") — deliberately **not** a subscription. This is a positioning pillar, not just a price. Free v1 to validate demand; paid unlock added only once there's traction.
- **Platform decision (2026-07-18):** **web-first installable PWA on Angela's existing Next.js/Vercel stack — NOT native SwiftUI.** The research recommended SwiftUI, but SwiftUI requires a Mac + Xcode and is impossible to build on Angela's Windows 11 machine. A PWA delivers everything v1 needs (offline, no backend, no data collection, installable, one-time purchase) on tools she already knows from Meridian + TCM App. Native App Store wrap (via Capacitor, no Mac required for cloud build) is a documented **later** step if it takes off — see Backlog.

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

## Open content decisions (settle during Phase 2, before recording audio)

- **Simplified vs. Traditional characters.** Heritage audiences split (Mainland = simplified; Taiwan/HK/many Cantonese-heritage families = traditional). **Design the content schema to hold both hanzi forms per word from day one** — cheap now, expensive to retrofit. Ship simplified as the default, with traditional as a toggle if time allows.
- **Pinyin vs. Zhuyin (bopomofo).** Taiwan uses zhuyin. Same principle: let the schema carry both romanisations; default to pinyin in v1.
- **Curriculum list.** Which ~150 words, which categories, which order/levels. This is Angela's + a native-speaker's call, not a code decision.
- **Voice.** One native voice actor for consistency; child-friendly, clear, standard tone. Decide accent/register (Mainland Putonghua default).

## Backlog — do NOT build in v1 (keep a `BACKLOG.md`)

Stroke-order tracing (v1.5, the fiddly touch-path feature) → speech/pronunciation practice with honest feedback (highest-risk, weak on web — a strong reason to consider native by then) → spaced-repetition review scheduling → traditional-character + zhuyin toggles (if not already shipped) → multiple child profiles → additional language packs (the architecture is built for this) → one-time paid unlock (Stripe on web, or App Store IAP if native) → **native app wrap via Capacitor for App Store/Play discovery + native billing** (no Mac needed — Capacitor + cloud build from Windows).

## Documents

- [[Ventures/Mandarin Kids App/Build Plan|Build Plan]] — Angela's step-by-step, zero coding experience assumed (2026-07-18)
- [[Ventures/Mandarin Kids App/Super Prompt|Super Prompt]] — paste into a fresh Claude Code session in the app's project folder to build (2026-07-18)

**Key build decisions locked in:** web-first **installable offline PWA** (not native SwiftUI — Windows can't build SwiftUI); **same core stack as [[Ventures/Meridian/index|Meridian]] + [[Ventures/TCM App/index|TCM App]]** (Next.js/TypeScript/Tailwind/shadcn on Vercel) for reused knowledge and accounts; **no backend, no accounts, no analytics** — content bundled in the app, progress in on-device storage, nothing leaves the device (this IS the privacy product); **content authored in a spreadsheet** → validated JSON content pack, same pipeline pattern as TCM App; **one-time-purchase model, never subscription** (a positioning pillar); **no runtime AI** (content is deterministic and fixed); **native App Store wrap deferred** to a post-traction Capacitor step.

## Tasks

- [ ] **Pick the working scope name** (folder currently "Mandarin Kids App") and decide whether the eventual brand should stay Mandarin-specific or be language-neutral (the architecture supports more languages later)
- [ ] **Settle the two content-schema decisions** before recording audio: simplified/traditional (hold both), pinyin/zhuyin (hold both) — see Open content decisions
- [ ] Reuse existing accounts (GitHub, Vercel). **No Supabase/Anthropic key needed for the app itself** — the only optional backend use is a marketing-page email waitlist (can reuse the Supabase pattern, or skip and just link TikTok)
- [ ] Create the project folder `C:\Users\Angela\Projects\mandarin-kids-app` (NOT inside the vault), open in VSCode, start Claude Code, paste the Super Prompt → builds Phase 1 (skeleton + landing page + installable offline PWA shell)
- [ ] Line up the content: draft the ~150-word curriculum, find a native Mandarin speaker to record ~150–170 clips, choose a consistent image source — this runs in parallel with Phases 1–2 and is the real bottleneck
- [ ] Deploy Phase 1 to Vercel early for a TikTok-bio link (same funnel as Meridian/TCM App); validate parent demand before building all phases

## Notes / progress

- 2026-07-18: Venture created from the claude.ai web market-research session (previously undocumented — flagged by an exhaustive vault search that found no prior record). Research synthesised into this note; Build Plan + Super Prompt written. **Corrected the research's platform recommendation** from native SwiftUI (impossible on Angela's Windows machine) to a web-first offline PWA on her existing stack, with native wrap deferred to a post-traction step.

Related: [[Ventures/index|Ventures]], [[Ventures/Meridian/index|Meridian]], [[Ventures/TCM App/index|TCM App]]
