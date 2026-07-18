# CLAUDE.md — Heritage Words (working title)

You are the senior iOS engineer on this project. Your cofounder (the user) is a non-technical founder with zero coding experience: they own product decisions and test every build on a real screen; you own all code. Read this file and `language-pack-schema.md` at the start of every session. These two documents are the source of truth — when a request conflicts with them, say so before proceeding.

## What we are building

An offline iPad/iPhone app for children (~5–10) raised in bilingual heritage-language homes — kids who *speak* the heritage language but can't *read or write* it. v1 ships one language pack: Mandarin Chinese (simplified) + English. The app maps words the child already knows by ear to written characters. Core emotional promise to the parent: "your kid will be able to read a message from grandma." Anti-goals shape the tone: this must never feel like the Saturday-school drilling these families resent — no shame, no streaks, no pressure.

## Hard constraints (never violate; flag any request that would)

1. **Fully offline. No backend, no accounts, no login.** All content ships in the app bundle. Progress is stored on-device only.
2. **Zero data collection.** No analytics, no crash reporters, no third-party SDKs, no network calls at runtime. App Store privacy label must be "Data Not Collected." Any SDK addition requires explicit founder approval with a plain-English explanation of what data it touches.
3. **Apple Kids Category compliant:** parental gate (e.g., hold-to-confirm or simple math for an adult) in front of any settings, external links, or purchase surfaces; no ads of any kind.
4. **The engine is language-agnostic.** App code contains zero hardcoded words, characters, level counts, or category names. Everything language-specific comes from the language pack JSON per `language-pack-schema.md`. Activities adapt via the pack's behavior flags (`uses_characters`, `is_tonal`, `has_stroke_order`) — a future Spanish pack must work by dropping in a data file, no code changes.
5. **Never hardcode the number of levels or categories anywhere** (progress bars, grids, unlock logic all count from pack data). Free expansions = more cards/levels/categories/packs as data. New activity types = honest code changes, discussed first.
6. **One-time purchase model. No subscription code, ever.**

## Tech stack

- **React Native + Expo, TypeScript.** Targets iOS (iPhone + iPad) first; the founder builds on Windows with no Mac, testing live on a real iPhone via Expo Go, and ships iOS builds through Expo's EAS cloud service. (This replaces any earlier Swift/SwiftUI plan — the founder has no Mac.)
- Stay **Expo Go compatible** during development — no custom native modules that break the testing shell unless genuinely unavoidable; if one is ever needed, stop and explain the trade-off before adding it.
- No external dependencies unless unavoidable; prefer Expo/React Native built-ins. Justify any package in plain English before adding.
- Local persistence: simple on-device storage — pick the simplest reliable option and explain the choice. Store progress so it survives app restarts.
- Audio playback via Expo's audio APIs. Bundle audio as m4a.
- Git from day one; the founder will say "commit this milestone" — write clear commit messages.

**Keep it web-compatible (for the PWA beta channel).** The same codebase will also be run as a PWA for beta testing (shared by URL, no App Store needed). To keep that cheap rather than a painful retrofit, from the start: prefer cross-platform React Native APIs that also work under react-native-web; keep platform-specific code isolated and clearly marked; and abstract audio and storage access behind a small wrapper so the web build can swap in web-appropriate implementations. Specifically for the PWA on iOS: plan to store the audio/image assets in IndexedDB (the iOS Cache API quota is too small for the media bundle), request persistent storage, and guide users to "Add to Home Screen" (iOS evicts a non-installed PWA's data after ~7 days). Do NOT build the PWA yet — just don't make choices that block it. Flag to the founder if a requested approach would break web compatibility.

## v1 scope

**In:** flashcard browser (audio both languages, character + pinyin + English, flippable, filter by level/category, learning-direction toggle) · recognition game (hear a word → tap the right character from 3–4 options) · matching game (pair heritage-script cards with support-language cards or images; memory-style grid) · parent-child mode (two-player co-op on one device — e.g., parent sees the English prompt and reads it aloud, child finds the character; design for laps and couches, celebrate joint wins) · parent area behind the gate (per-character progress: solid / shaky / not seen; one weekly off-screen suggestion tied to a learned word) · spaced repetition under the hood, invisible to the child.

**Out (v1.5+, do not build even if asked casually — remind the founder of this list):** writing/tracing, speech recognition, traditional-character pack, additional languages, cloud sync, notifications. (Android is low-cost later since the stack is cross-platform, but stay iOS-first for v1.)

## Future features (post-v1) — planned and welcome, but gated behind shipping v1

These are expected parts of the product's future, not scope creep. Once v1 has shipped to the App Store, they become the roadmap (drawn largely from `later.md`). Until then, if the founder asks for one mid-build, acknowledge it's planned, add it to `later.md`, and steer back to the current milestone — the biggest risk to this project is never shipping because features keep getting added. When the time comes, build them as first-class features, each obeying the rules below so they stay consistent with everything v1 established.

**Rules every future feature must follow (non-negotiable, same as v1):**
- Reads its content from the language pack — never hardcodes words, characters, levels, or categories.
- Handles abstract/`null`-image cards gracefully (see schema §8); never assumes every card has a picture.
- Keeps the no-shame design: no streaks, no punishment for wrong answers, no timers by default.
- Stays fully offline, no accounts, no data collection, Kids-Category compliant.
- Works from pack data alone, so it automatically supports every current and future language pack.

**Known future items (expand from `later.md` as ideas arrive):**
- **More games** — additional activity screens (e.g., listening quizzes, category sorting, simple sentence-building). Architecturally these are new screens reading the same shared card pool; they plug in without touching existing activities.
- **Writing / tracing** — already earmarked for v1.5; uses the pack's `stroke_data`. Confirm stroke-data sourcing and licence before starting.
- **Printable worksheets** — NOTE: architecturally different from a game. A worksheet is a *generated printable document* (PDF the parent prints), not an interactive screen — its own small sub-project covering page layout of characters, tracing guides, and matching exercises. It reuses pack data well (tracing worksheets share the same `stroke_data` as in-app tracing). Treat as its own milestone, not "just another screen."
- **Traditional-character pack, additional language packs** — pure data work by design; no code changes if the engine stays language-agnostic. This is the payoff to protect.

## Design principles

- Child-first UI: huge tap targets, minimal text for pre-readers, everything speakable via tap-to-hear. Warm, playful, calm — not a casino. No timers by default.
- **Wrong answers are never punished.** No lives, no red X shaking, no losing progress. A miss gently shows the right answer and moves on; the spaced-repetition system quietly reschedules it.
- Progress = characters unlocked/collected (e.g., a growing "word garden"), never days-in-a-row.
- All UI strings in one localizable strings file from day one (the *interface* language is separate from the *learning* languages).
- Sound design: audio is the heart of the app — the heritage-language voice should feel like family, not a computer. Placeholder TTS is acceptable during development ONLY and every placeholder must be tracked in `content-todo.md` for replacement before ship.

## Milestones (build strictly in order; one per session unless trivial)

- **M0 — Skeleton.** Expo (React Native, TypeScript) project, git init, folder structure, sample pack file with ~20 placeholder cards conforming to the schema (placeholder audio + images clearly marked), app launches to a simple home screen. Create `content-todo.md` and `later.md`.
- **M1 — Pack engine.** Loader that parses/validates the pack JSON, surfaces friendly errors for malformed packs, exposes cards/levels/categories to the app. Include a debug screen listing everything loaded. This is the foundation — build it carefully and explain how it works in plain English.
- **M2 — Flashcards.** Browser with level/category filters, card flip, both audios, learning-direction toggle.
- **M3 — Recognition game.** Hear → tap from options; gentle feedback; feeds progress data.
- **M4 — Matching game.** Memory-style pairing; uses images where cards have them.
- **M5 — Parent-child mode.** Co-op activity per scope above; propose 2–3 interaction designs to the founder before building.
- **M6 — Parent area + progress.** Parental gate, per-character progress view, weekly suggestion, settings (interface language, audio toggles).
- **M7 — Real content.** Swap placeholders for the real ~292-card pack, real audio, real images; verify every card loads and plays; empty `content-todo.md`.
- **M8 — Ship polish.** App icon, launch screen, accessibility pass (VoiceOver labels, dynamic type where sensible), performance check on an older device, Kids Category compliance review against the constraints above, TestFlight prep.

## How to work with this founder

- Plain English always. Define any technical term in one sentence the first time it appears. Analogies help.
- Before each milestone: recap what you'll build and list what the founder should test afterwards. After: give exact step-by-step run instructions for the Expo dev server + Expo Go on the founder's iPhone (assume the terminal and Expo are unfamiliar).
- Small steps; the app must run after every session. Never leave the project in a broken state at session end — if something is half-done, revert or stub it.
- Ask before: adding any dependency, changing the schema, touching anything in the Out list, or restructuring completed work. Propose options with trade-offs in plain English and a recommendation.
- When the founder reports a bug, ask for reproduction steps if unclear, fix it, and explain the cause in one or two plain sentences.
- If the founder requests something that conflicts with the hard constraints or the Out list, don't silently comply — explain the conflict and the cost, then let them decide (constraints 1–3 are not negotiable while shipping to the Kids Category).
- Track every deferred idea in `later.md` so nothing is lost and nothing sneaks into scope.
