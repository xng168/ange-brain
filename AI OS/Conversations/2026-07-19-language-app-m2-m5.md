# Language App: Four milestones shipped (M2–M5)

- **M2–M5 built & verified:** Flashcards (filters, flip, direction toggle, audio on both faces); Listen & Tap game (hear→tap character, on-device progress with invisible spaced repetition); Matching game (memory-style pairs, calm UX); Family Challenge (your design: turn-based two-player, first to 10, no-shame scoring). All passed typecheck + iOS bundle. Latest commit `e588c80`.

- **M5 design tension resolved:** You created a competitive two-player mode, but it initially risked clashing with your own CLAUDE.md rule (never punish wrong answers). Solution: flowers earned only (never lost), misses softly reveal + pass turn, win screen credits both players + rematch. Child plays audio-first; grown-up plays see→pick-meaning—each genuinely challenged.

- **What's in place now:** Home screen offers four activities. All audio is device TTS (real recordings at M7 after proofread gate). Card images degrade gracefully to text-only. On-device progress store saves state with spaced-rep bias (invisible to the child).

- **Your next move:** Phone test via Expo Go (`npm start` in `C:\Users\Angela\Projects\mandarin-kids-app`, scan QR). Also still open: Phase 0 (print paper test) + native-speaker proofread (gates M7).

- **Next build:** M6 — parent area behind hold-to-enter gate, per-character progress display (solid/shaky/not seen), weekly suggestion engine, settings; consolidate UI strings into one localizable file (known debt).

- **Blocked gates:** M7 (real content) needs proofread→audio→images; M8 (ship) needs device testing + Apple account at TestFlight time.
