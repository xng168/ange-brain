# Open Items

Active tasks, open questions, and decisions pending.

## Setup (in progress)
- [ ] Vault setup phases 0–12 (see [[log]] for progress)
- [ ] Gmail/Google Calendar are confirmed connected and healthy (verified via `claude mcp list`), but their tools still aren't appearing inside this specific Claude Code (VSCode) session, even after a window restart. gbrain's MCP tools DID become available mid-session (used successfully during setup), so this looks specific to the pre-existing claude.ai cloud connectors rather than a general MCP-loading issue. Starting a brand-new session should resolve it — check next time you open Claude Code.
- [x] Metricool signed up, TikTok connected. [ ] Still need to connect Instagram — steps in [[AI OS/Technology/Social Media Tools]].
- [ ] gbrain's 9 bonus skills (book-mirror, article-enrichment, etc.) did not scaffold — `gbrain skillpack scaffold --all` expects a specific "agent repo" structure that doesn't match this vault setup. Not blocking; skipped for now.
- [x] The Stop hook (Phase 9) is confirmed working — it fired multiple times during this setup session and wrote several good-quality summary files into AI OS/Conversations/. One instance reported a permission error, but it's clearly not a systemic problem given how many succeeded. Not a blocker; watch for recurrence.
- [ ] **Known gotcha:** editing `secrets.env` (e.g. via a text editor or certain tools) can reset its file permissions back to Windows defaults, undoing the Phase 3 lockdown. After any edit to that file, re-run: `icacls "C:\Users\Angela\.claude\secrets.env" /inheritance:r` then `/grant:r "Angela:F"` and `/grant:r "SYSTEM:F"`. Caught and fixed once already during the post-setup bug check.
