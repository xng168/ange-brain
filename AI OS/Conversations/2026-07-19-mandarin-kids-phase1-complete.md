# Mandarin Kids App: Phase 1 Complete & M1 Pack Engine Built

## What Was Done

- **Phase 0 PDF regenerated** — Reconstructed and verified the paper-test-cards.pdf (5 pages with 20 hanzi cards + instructions) which wasn't in the original export; ready to print
- **Phase 1 content audit complete** — 292-word Mandarin list passed QA: sequential IDs, zero empty cells, zero pinyin errors, tone sandhi applied correctly
- **Proofread guide created** — 27-row attention list (proofread-notes.txt) highlighting tone sandhi + neutral-tone rows to speed native-speaker review
- **M1 pack engine built & committed** — Pack loader with plain-English validation and debug screen; tested with deliberately broken packs (correctly caught missing language block, empty audio, unknown category, duplicate ID); shipped as commit e2403b6

## Key Decisions

- Prioritized automatable milestone work (build toolchain, content QA, M1 engine) while human-gated tasks (paper test, native speaker review) wait on Angela
- Created proofread notes as separate artifact to accelerate reviewer workflow without blocking development
- Bundled M1 engine as ready-for-iOS before waiting on Phase 0 validation (can test on device with `npm start` + Expo Go)

## What's Next

1. **User actions (blocking audio recording):**
   - Print + run paper test with interviews per validation-kit.md
   - Coordinate native-speaker proofread (hand them spreadsheet + proofread-notes.txt)
   - Test app on iPhone (`npm start` → scan QR in Expo Go)

2. **Next build milestone:** M2 (flashcards) — say the word when ready, or start fresh Claude Code session in project folder per one-milestone-per-session rhythm
