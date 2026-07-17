# Mandarin Kids App — Build Plan & Venture Setup

- **Completed a full venture specification** for an offline, privacy-first Mandarin learning app for heritage-speaker kids; created venture index, build kit, and super prompt in the vault under `Ventures/Mandarin Kids App/`
- **Architecture locked in**: PWA (progressive web app) on Next.js/Vercel, no backend/accounts/data collection/ads/streaks; single permanent purchase model; offline-first (nothing leaves device)
- **v1 scope**: three core activities (flashcards, audio-image matching game, parent mode with gate) plus installable shell + landing page; stroke-tracing and speech deferred to v2
- **Deliberately overrode research recommendation** from SwiftUI (native app) to web-first PWA for faster validation without requiring a Mac or App Store submission
- **Content bottleneck identified**: ~150-word list + ~150–170 audio clips (native speaker) + consistent images; this runs parallel to development
- **Next immediate steps**: (1) create project folder, (2) paste super prompt into Claude Code to build Phase 1, (3) test offline on phone-sized window, (4) deploy to Vercel early for TikTok bio link & demand validation; **pending decision**: Simplified + Pinyin (recommended) or Traditional + Zhuyin as v1 default character/romanization set
