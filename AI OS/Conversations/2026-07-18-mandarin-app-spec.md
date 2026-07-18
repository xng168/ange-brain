# Mandarin Kids App — Market Research & Venture Spec Complete

- **Identified & validated a new venture:** Offline-first, privacy-safe, buy-once Mandarin learning app for young heritage-speaker children (ages 3–7). Research mined parent complaint threads and found two strong signals: (1) demand for offline, no-subscription kids apps, and (2) post-Duolingo language gap (heritage speakers underserved, no streak anxiety alternatives).

- **Key strategic decision: PWA + Capacitor dual-track from day one.** Initially researched SwiftUI but ruled it out (requires Mac; Angela is Windows-based). Chose web-first installable PWA (uses her existing Next.js/Vercel stack from Meridian & TCM App), with constraint that codebase stays Capacitor-compatible so it can later wrap into a real App Store app via cloud macOS build (GitHub Actions / Ionic Appflow — no Mac hardware needed). This keeps the door open for distribution without rewriting.

- **Positioning & market wedge locked:** Deliberately narrow (one language, one audience, one job). Pitch is everything Duolingo-style incumbents are criticized for *not* being: **offline, no subscription, no data collection, no ads, no chat, native-quality audio, calm (no gamification anxiety).** COPPA-safe by construction since there's no server and no personal data.

- **Spec complete:** Comprehensive Build Plan + Super Prompt created and ready for build kickoff. Venture documented in vault as "Spec'd" stage, awaiting engineering phase.

- **Next:** Run `gbrain import` to index new venture docs into semantic search, then begin Phase 1 build (core app scaffold, bilingual UI, audio-playback engine, parent gate).
