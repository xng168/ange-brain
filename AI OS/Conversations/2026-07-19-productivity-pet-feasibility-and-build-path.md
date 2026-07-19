# Productivity Self Care Pet: Feasibility, Build Path & Dual-Trigger Architecture

## Session summary

Completed a **full feasibility review and build-path spec** for "Productivity Self Care Pet"—a roaming on-screen self-care companion that nudges on screen-time usage. Reframed from a Finch-style blocker into a **desktop-pet × self-care fusion**, then mapped the exact effort and cost to ship on each platform.

## Key decisions made

1. **Platform hierarchy flips to desktop-first**: iOS is *impossible* for the hero mechanic (no third-party draw-over-other-apps API); desktop (Electron/Tauri) and Android are both feasible. Strongest fit is **Windows/macOS desktop** — matches original instinct, proven genre, viral potential (Desktop Goose precedent), zero gatekeepers.

2. **Trigger model reframed as complementary dual-engine** (Path A + B, not either/or):
   - **Path A** (scheduled/goal-based): Timers, focus sessions, streaks → cheap, no permissions, ships as v1 on any platform
   - **Path B** (usage-based): Detect real app usage, cross threshold, fire nudge → cost varies wildly by platform (cheap on desktop, expensive/risky on iOS)
   - Both feed the same pet; they share ~70% of code (the pet itself, animations, state, settings)

3. **Build phases locked**:
   - Phase 0: Pet + presence layer (the heart — art-heavy, shared across platforms)
   - Phase 1: Path A engine → v1 ships (low-to-medium effort)
   - Phase 2: Path B engine → "smart" layer (effort swings by platform)
   - Phase 3: Monetise + distribute

4. **Cost reality by platform** (Phase 2 Path B specifically):
   - **Windows desktop**: Low–medium effort, zero gatekeepers
   - **macOS**: Medium, Accessibility permission + notarisation (no Apple approval)
   - **Android**: Medium, Play policy friction on overlay
   - **iOS**: High + real approval risk (FamilyControls entitlement must be granted by Apple, not guaranteed)

## What's next

- **MVP definition**: Lock exact v1 feature list + choose lead platform (recommend desktop)
- If proceeding: Update venture spec with this build-path + dual-trigger architecture
- Timeline decision: Ship Path A desktop MVP to validate before investing in Path B or Android
- Brand + real name TBD (moat is positioning + art, not tech)
