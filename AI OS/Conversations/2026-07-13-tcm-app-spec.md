# TCM App: Spec & Build Plan Complete

## Summary

- **No user accounts in v1** — quiz results and favorites stored in browser localStorage; removes signup friction and auth complexity unnecessary for a "quick lookup" reference tool.

- **Content pipeline is spreadsheet-driven, not admin-UI-driven** — you and your TCM practitioner fill a shared sheet with a fixed column template; a script imports it at build time. AI enrichment happens once per ingredient at import, not live, keeping running costs near zero.

- **Reuses Meridian stack** — Next.js, Supabase, Vercel, Claude API. Same accounts, same "deterministic data + AI interprets only" principle, same phased build rhythm with stop-and-test gates.

- **Created Super Prompt.md** — full technical brief with data model, 7 build phases + acceptance criteria, content tone/guardrails. Ready to paste into Claude Code.

- **Created Build Plan.md** — plain-English walkthrough for accounts setup, project initialization, per-phase testing, and spreadsheet import pipeline. Updated index.md and Open Items.md to mark TCM App spec'd and ready.

## Next Step

Create `tcm-app` project folder, spin up new Supabase project, paste Super Prompt into Claude Code to begin Phase 1—same motion as Meridian launch.
