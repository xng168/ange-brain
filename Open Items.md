# Open Items

Active tasks, open questions, and decisions pending.

## Meridian (pre-build)
- [x] Working name chosen: **Meridian** (2026-07-12). Vault folder renamed to `Ventures/Meridian/`, all links updated.
- [ ] Before launch: confirm the name — check meridian .com/.app domain + TikTok/IG handle availability (a qualifier like "Meridian App" may be needed; "meridian" alone is a busy word).
- [ ] Create build accounts: Vercel + Supabase (both "sign in with GitHub"), Anthropic Console (needs a card, ~USD $5 credit) — see [[Ventures/Meridian/Build Plan|Build Plan]] Step 0.
- [ ] Decide whether to post a build-in-public teaser on TikTok once the Phase 1 waitlist page is live.
- [x] Fixed 2026-07-13: gbrain sync had silently fallen behind since the "Timed out waiting for PGLite lock" failures (28/64 vault files indexed — everything from Meridian, TCM App, and Investing updates was missing from semantic search). A full re-sync via `mcp__gbrain__sync_brain(full=true)` caught it up to 64/64, 100% embed coverage. Root cause: the incremental sync checkpoint got stuck after the lock timeouts and didn't self-recover the way the git sync layer does — worth remembering to run a full sync occasionally, or after any "PGLite lock" error.

## TCM App (building)
- [x] Market research, competitor landscape, data-sourcing strategy, target audience, and niche-wedge decisions captured in [[Ventures/TCM App/index|TCM App]] (2026-07-12)
- [x] Pivoted from food tracker to educational ingredient lookup/repository (2026-07-12)
- [x] Build Plan + Super Prompt written (2026-07-13) — see [[Ventures/TCM App/Build Plan|Build Plan]]
- [x] Phase 1 built and committed: project scaffolded at `C:\Users\Angela\Projects\tcm-app`, landing page + waitlist form, tested locally (2026-07-13)
- [ ] **Your turn:** create a new Supabase project and add its URL + anon key to `.env.local` — exact steps in [[Ventures/TCM App/index|TCM App]] Tasks
- [ ] Push to GitHub + connect Vercel for a live link, then run the TikTok content test — see [[Content/Ideas/TCM food properties series]]
- [ ] Continue with Claude Code for Phase 2 (data model + spreadsheet import pipeline) once Supabase is connected
- [ ] Loop in the TCM practitioner reviewer early, per the Open Gaps section in the venture note

## Mandarin Kids App (pre-build)
- [x] Imported the claude.ai web market-research session into the vault and spec'd the venture (2026-07-18) — see [[Ventures/Mandarin Kids App/index|Mandarin Kids App]]
- [x] **Platform decision revised (2026-07-18):** fuller web-chat transcript showed it had already moved SwiftUI → **React Native + Expo** (Windows dev, Expo Go on-phone testing, EAS cloud iOS builds — no Mac) and Angela ratified it there. Vault's PWA-path Build Plan + Super Prompt marked superseded (kept as fallback). Claude Code endorsed the switch: offline reliability, one-time purchase, Kids-Category trust are all stronger native.
- [ ] **Import the web-chat build kit** (the canonical version) into the vault/project: CLAUDE.md super prompt, no-Mac build guide, symmetric two-language schema, **292-word bilingual content list** — download/copy from the claude.ai session before starting the build
- [ ] **Decide two content-schema questions** before recording audio: simplified vs. traditional characters, pinyin vs. zhuyin (schema holds both; just pick the v1 default — recommend simplified + pinyin)
- [ ] Get the 292-word list **native-speaker proofread** (the stated gate before any audio recording), then line up recording (word + phrase clips) + a consistent image source — the real bottleneck
- [ ] Create `C:\Users\Angela\Projects\mandarin-kids-app`, install Node.js, place the web kit's CLAUDE.md, start Claude Code → Milestone 0 (Expo scaffold, test on iPhone via Expo Go)
- [ ] Landing page + waitlist on Vercel (separate tiny site, same pattern as Meridian/TCM App) for the TikTok-bio validation link — the funnel doesn't wait for the native app
- [ ] Later gates to remember: Apple Developer $99/yr at TestFlight time; EAS free-tier limits (~US$19/mo beyond) once cloud builds start

## claude.ai web export migration (2026-07-18)
- [x] Exported the full claude.ai account history (29 conversations) → archived raw in `_sources/Export Data 18072026/` (gitignored).
- [x] Reconstructed the Mandarin Kids App build kit from the export's tool-command history (the rendered files weren't in the export); verified + fixed a replay gap; kit now in `Ventures/Mandarin Kids App/build-kit/`. See [[Ventures/Mandarin Kids App/index|Mandarin Kids App]].
- [x] Layered migration of the other conversations: **23 full-transcript notes** filed into pillars; 6 trivial ones (WinRAR, wifi troubleshooting, ollama, product-image gen, a WeChat-post read, an empty chat) left in the raw archive only.
- [x] **Two significant undocumented things surfaced — need Angela's follow-up:**
  - [ ] **Eyewear/sunglasses brand venture** now created at [[Ventures/Eyewear Brand/index|Eyewear Brand]] — confirm whether "NEU" / the Asian-inspired fashion naming is the *same* venture or a separate fashion brand, and capture the real current state (manufacturers contacted, samples, timing — only research convos are in the vault so far).
  - [ ] **Potential move to Hong Kong** + active finance/audit job search — captured in [[Personal/index|Personal]]. If the HK move is live, promote the key tax/visa/residency decisions into this Open Items list (it affects [[Investing/index|investing]] and where ventures are based).
- [ ] One conversation left unclassified in the raw archive: "Can you read this WeChat post?" (10 msgs) — topic unknown from the title; re-file if it matters.

## Content (Ange.beee)
- [ ] Edit black sesame video for TikTok
- [ ] Film/post the TCM food properties series (ginger hot/cold, flu-symptom foods) — cheap validation test for [[Ventures/TCM App/index|TCM App]] before building anything; see [[Content/Ideas/TCM food properties series]]

## Sync
- [x] 2026-07-18: gbrain checkpoint-wedge recurred with a **second trigger**: a sync that fails mid-embed (`blocked_by_failures`, files "banked", embedded 0) still advances the git checkpoint, so later incremental syncs report "synced" while search keeps serving stale chunks. Same fix as 2026-07-13: `mcp__gbrain__sync_brain(full=true)` (reads the directory directly, also catches uncommitted edits). Rule of thumb now confirmed twice: **after any gbrain sync error — lock timeout or embed failure — run a full sync and spot-check with a query.** Also: the CLI `gbrain import` always hits "Timed out waiting for PGLite lock" while the MCP `gbrain serve` process is running (single-writer DB) — use the MCP `sync_brain` tool from inside a session instead.
- [x] 2026-07-13 00:57: one `git pull --rebase` sync attempt failed (likely a timing collision between Obsidian Git's 10-min auto-commit and the 20-min sync.ps1 task during a heavy editing session). Self-healed on the next scheduled run 5 min later — confirmed no data loss, vault fully matches GitHub. Not fixed proactively since it's a rare, self-recovering race; revisit only if it starts happening frequently.

## Setup (in progress)
- [ ] Vault setup phases 0–12 (see [[log]] for progress)
- [ ] Gmail/Google Calendar are confirmed connected and healthy (verified via `claude mcp list`), but their tools still aren't appearing inside this specific Claude Code (VSCode) session, even after a window restart. gbrain's MCP tools DID become available mid-session (used successfully during setup), so this looks specific to the pre-existing claude.ai cloud connectors rather than a general MCP-loading issue. Starting a brand-new session should resolve it — check next time you open Claude Code.
- [x] Metricool signed up, TikTok connected. [ ] Still need to connect Instagram — steps in [[AI OS/Technology/Social Media Tools]].
- [ ] gbrain's 9 bonus skills (book-mirror, article-enrichment, etc.) did not scaffold — `gbrain skillpack scaffold --all` expects a specific "agent repo" structure that doesn't match this vault setup. Not blocking; skipped for now.
- [x] The Stop hook (Phase 9) is confirmed working — it fired multiple times during this setup session and wrote several good-quality summary files into AI OS/Conversations/. One instance reported a permission error, but it's clearly not a systemic problem given how many succeeded. Not a blocker; watch for recurrence.
- [ ] **Known gotcha:** editing `secrets.env` (e.g. via a text editor or certain tools) can reset its file permissions back to Windows defaults, undoing the Phase 3 lockdown. After any edit to that file, re-run: `icacls "C:\Users\Angela\.claude\secrets.env" /inheritance:r` then `/grant:r "Angela:F"` and `/grant:r "SYSTEM:F"`. Caught and fixed once already during the post-setup bug check.
