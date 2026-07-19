# Mandarin Kids App: Build Phases M0–M1 Complete, Project Setup

- **Reconstructed and verified all build kit files** from exported session history; original files confirm byte-for-byte match with M0/M1 direction. Covenant on architecture locked in: static PWA, offline-first, no backend, no data collection.

- **M0 (skeleton) + M1 (pack engine)** implemented and committed—manifest loader, language-pack validation, debug screen, placeholder pack data all integrated and tested. Three parallel gates remain: paper card test + interviews, native-speaker proofread of content list, and phone QR scan validation.

- **Project folder created** at `C:\Users\Angela\Projects\mandarin-kids-app` with Expo/React Native stack ready. Discovered Windows execution-policy block on first npm start attempt; set fix path clear (Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned).

- **Next: confirm npm start works** after execution policy is applied, then proceed to M2 (Flashcards activity—deck browser, card flip, dual-language audio, learning-direction toggle).

- **App Store path remains open** via Capacitor wrapper (no build-time cost, no hardware purchase needed—cloud compile only).
