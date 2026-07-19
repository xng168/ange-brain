# Mandarin Kids App — M0–M5 Build & Deployment Complete

- **Completed 4 core milestones** (M0–M5) of the bilingual Mandarin children's app; all built, verified, typechecked, and committed to `main`
  - M0: Expo skeleton + build kit
  - M1: Pack engine with plain-English validation
  - M2: Flashcards activity (with audio bidirectional support)
  - M3: Listen & Tap (character recognition game with spaced repetition)
  - M4: Matching game (memory-style pairs)
  - M5: Family Challenge (competitive 2-player, first-to-10)
  - All activities now wired into home screen

- **Created image asset registry** (`src/assets/images.ts`) to handle card image bundling for Metro; stubbed for M7 real licensed images

- **Resolved production launch blocker**: User encountered Windows PowerShell execution policy blocking npm; provided one-time fix (`Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned`) and terminal basics explanation for first-time user

- **Next steps**: User to verify execution policy fix, confirm `npm start` launches iOS bundle successfully via Expo Go, then test app on device with QR code scan
