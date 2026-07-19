# Heritage Words iOS Mobile Testing Session

- **Debugging Expo React Native iOS app build**: Worked through Metro bundler connection issues between Windows dev machine and physical iPhone. Multiple SDK version compatibility issues (SDK 55 → SDK 54) and tunnel/non-tunnel connection modes tested.

- **Successfully bundled for iOS**: Metro confirmed "iOS Bundled 708 modules" — indicating clean connection and successful build for device. App architecture locked to 292 Hanzi characters + four activities (Flashcards, Listen & Tap, Matching, Family Challenge).

- **File sync & Git commits**: Pinned Expo SDK 54 (App Store-compatible), updated CLAUDE.md build docs, and committed feature branches (M4 matching game, M5 family challenge). Progress tracked in PROGRESS.md and AGENTS.md.

- **Next step: Visual verification** — awaiting screenshot or confirmation from iPhone to confirm "Heritage Words" home screen renders correctly with hanzi character, tagline, and activity buttons.

- **Known open items**: App Store pathway remains available via Capacitor/EAS cloud builds if needed later (no Mac required); prioritize web PWA validation first.
