# Log

Running record of setup and major activity.

## 2026-07-12
- Vault initialized at `C:\Users\Angela\Documents\Obsidian\Brain`.
- Phase 0 complete: git, node, npm, python, bun, ollama, Obsidian verified; nomic-embed-text pulled.
- Phase 1: five-pillar folder structure created.
- Phase 2: git + GitHub remote configured, Obsidian Git plugin set to auto commit-and-sync every 10 min, sync.ps1 scheduled every 20 min via Task Scheduler. Verified end-to-end.
- Phase 3: secrets.env created at C:\Users\Angela\.claude\secrets.env, permissions locked down, python-dotenv installed and verified.
- Phase 4: daily stack discovered (Gmail, Google Calendar, phone notes app, Canva, CapCut, Shopify, local file storage). Gmail/Calendar connectors registered but not yet surfacing as tools in this session (open item). No connectors/MCP found for Canva, CapCut, Shopify — logged as later builds in AI OS/Technology/Daily Stack.md.
- Phase 5: researched Metricool vs Buffer vs Later vs Planable, recommended Metricool free tier (best free analytics + TikTok/IG + calendar combo). Saved to AI OS/Technology/Social Media Tools.md. Weekly analytics review routine added. Metricool signup + TikTok/IG connection deferred to Open Items (Angela's choice).
- Phase 6: gbrain installed (bun install -g github:garrytan/gbrain), initialized with PGLite + local Ollama embeddings (nomic-embed-text, 768d), vault imported (9 pages), doctor health check passed (embeddings 100%, correct provider/dims). Registered as MCP server at user scope via standalone claude CLI (installed for this purpose). Search mode kept at conservative (no paid LLM expansion, $0 cost). gbrain guidance added to CLAUDE.md. Confirmed via `claude mcp list` that Gmail/Calendar connectors are genuinely healthy — the earlier "not appearing" issue is a session-scoping quirk, not a broken connection.
- Phase 7: full vault CLAUDE.md written (who Angela is, five pillars, wikilink conventions, filing rules, single-source-of-truth rule). Pointer CLAUDE.md added at C:\Users\Angela\CLAUDE.md.
- Phase 8: automode permissions written to C:\Users\Angela\.claude\settings.json (user scope) — standard ops (edits, builds, local git, gbrain MCP) proceed automatically; push, destructive resets, force branch delete, and file/folder deletion require confirmation; unlisted/future tools (e.g. social publishing) default to asking since defaultMode is "default".
