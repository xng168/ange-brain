# Expo SDK 54 Switch with Version Preservation

- **Upgraded Expo project from SDK 57 to SDK 54** as a clean new commit (`d4dd52a`) on top of existing history, preserving all prior work
- **Bookmarked SDK 57 version** with git tag `sdk-57-scaffold` for easy future reference without memorizing commit hashes
- **Clarified version control strategy**: SDK 57 commit (`e588c80`) remains fully intact; the switch is a forward commit, not a rewrite/destructive operation
- **Explained upgrade path forward**: Once Expo Go's App Store version catches up to SDK 57+, upgrading in the future will be straightforward (standard `npx expo install expo@^57.0.0 --fix` pattern)
- **Key command to reference**: `git checkout sdk-57-scaffold` lets you instantly jump back to the SDK 57 scaffold if needed for comparison or recovery
- **Next**: Project is now on SDK 54; continue development normally. Tag remains as an insurance bookmark with no action needed.
