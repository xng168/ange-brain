# Second Brain Setup (Phases 0–9)

## Completed in This Session
- **Phases 0–9 complete** out of 12-phase setup plan
- Dev tools verified (git, node, npm, python, bun, ollama, Obsidian); nomic-embed-text model pulled
- Five-pillar vault structure created (AI OS, Ventures, Content, Personal, Reference) with system folders (_sources, _memory, _secrets) and root files (CLAUDE.md, index.md, Open Items.md, log.md, _inbox.md)
- Git initialized, GitHub remote configured, Obsidian Git plugin auto-commits every 10 min, PowerShell Task Scheduler syncs every 20 min (even when Obsidian closed)
- secrets.env created with locked permissions at `C:\Users\Angela\.claude\secrets.env`, python-dotenv configured
- Gmail and Google Calendar connectors registered and verified healthy (session-scoping quirk prevented them from appearing in this VSCode session, but confirmed working via `claude mcp list`)
- Metricool recommended and documented as primary social media tool (free tier supports TikTok + Instagram + analytics + calendar)
- gbrain semantic search installed with PGLite + local Ollama embeddings (nomic-embed-text, 768d); vault imported and doctor health check passed
- Comprehensive vault CLAUDE.md written; pointer CLAUDE.md added at `C:\Users\Angela\CLAUDE.md`
- Automode permissions configured in user settings.json (standard ops auto-proceed, push/destructive/social-publish require confirmation)
- claude-mem@thedotmack plugin installed and enabled via standalone claude CLI; Stop hook added to write session summaries to AI OS/Conversations/ after each session ends

## Key Decisions
- Vault root is `C:\Users\Angela\Documents\Obsidian\Brain` (user's clarification on initial path mismatch)
- Conservative gbrain search mode (no paid LLM expansion, stays $0 cost)
- Social media: Metricool free tier chosen over Buffer, Later, Planable (best free analytics + TikTok/IG combo)
- Skills: Enable claude-mem + Marketing Skills by default; keep GStack, ECC, C-Level Advisor disabled for on-demand use only (token efficiency)

## Session 2 Update (Phase 10 In Progress)

### Completed
- **Bun 1.3.14** installed successfully via winget (was missing in Phase 0, now on PATH after VSCode restart)
- **Phase 10 (Telegram bridge)** partially complete:
  - Created Telegram bot `angela_secondbrain_bot` via BotFather
  - Bot token and chat ID (`7098413814`) saved to `secrets.env`
  - Built Python daemon script (`telegram_bridge.py`) that:
    - Listens for new messages via Telegram bot API polling
    - Pipes messages to Claude for semantic processing
    - Saves replies back to vault and back to Telegram
  - **Fixed two critical bugs:**
    1. Windows subprocess invocation: changed to shell mode so `claude.cmd` shim resolves correctly
    2. Crash safety: added progress logging to prevent re-processing old messages after restarts
  - **Currently testing:** sent test message to bot, monitoring for successful reply via log file watcher (background task running)

### Key Decisions This Session
- TCP socket architecture replaced with simpler direct polling (Telegram bot API is more reliable on Windows than maintaining long-lived sockets)
- Progress logged to `_sources/telegram_bridge.log` with simple line format ("Replied: ...") for easy shell monitoring

## Next Steps
1. **Phase 10 completion** (this session): Verify telegram reply lands in log, then schedule daemon as Windows background task (nssm or Task Scheduler)
2. **Phase 11**: Install/enable skills deliberately via /plugins dialog  
3. **Phase 12**: Interview Angela on ventures (stage, model, partners, tracking needs) and content (niches, cadence, monetization, workflow); create starter notes
4. **Final**: Run checklist, commit everything, provide first three actions for daily use
