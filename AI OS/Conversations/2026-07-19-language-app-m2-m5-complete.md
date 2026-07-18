# Language Learning App: Milestones 2–5 Complete

- **Built four activity modules** (M2–M5) and shipped them to production on `main`: Flashcards with audio flip, Listen & Tap spaced repetition game, Matching pairs game, and Family Challenge (two-player competitive mode to first 10). All passed typecheck and iOS bundle verification.

- **Design decision on M5 (Family Challenge):** Resolved tension between competitive framing and child-safe ethos by making points flowers-only (never red), wrong answers gently reveal instead of punish, and win screen credits both players with co-op language ("together you grew N words"). Child gets audio-first rounds, grown-up gets character-identification rounds for asymmetric challenge.

- **Current state:** Home screen now offers all four core activities. Placeholder tech debt: device text-to-speech (real audio/images come at M7 post-proofread). All milestones recorded in `PROGRESS.md` and vault.

- **Next for Angela:** Phone test—`npm start`, scan QR, play through all activities as a 6-year-old would. Also Phase 0 (print test cards) and native-speaker proofread gate remain open.

- **Next for Claude (M6):** Parent dashboard behind hold-to-enter gate with per-card progress tracking (solid/shaky/unseen), weekly suggestion engine, and settings. Also consolidate UI strings for localization.

- **Blocked gates:** M7 (real content) needs proofread ✓ audio ✓ images. M8 (TestFlight polish) needs device testing + Apple account.
