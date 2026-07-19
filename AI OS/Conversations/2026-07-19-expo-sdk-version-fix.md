# Fixed Expo SDK version mismatch blocking iPhone testing

- **Problem diagnosed:** Project was scaffolded on Expo SDK 57 (create-expo-app default), but Apple's App Store review is typically 2-3 SDK versions behind. Only SDK 54's Expo Go app is currently installable; SDK 57 isn't available yet on the App Store, making the "Project is incompatible with this version of Expo Go" error unfixable by redownloading.

- **Solution applied:** Pinned the project down to Expo SDK 54 (the only public, App Store-approved version) using the officially supported downgrade path: `npx expo install expo@^54.0.0` + `npx expo install --fix`. Also updated React Native to 0.81.5. TypeScript still compiles cleanly; iOS bundle verified (598 modules).

- **Committed:** `d4dd52a fix: pin to Expo SDK 54 (App Store-approved) so Expo Go can run it`

- **Key insight:** App Store lag on Expo Go approval is a recurring issue, not a one-time problem. Worth checking before any future `create-expo-app` scaffolds.

- **Next step:** Angela should rescan the QR code with her iPhone Camera in Expo Go — it should now open and show the "Heritage Words" home screen with four activity buttons (M1–M5 complete, awaiting next builds).
