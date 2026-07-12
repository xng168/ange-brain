# Daily Stack

Discovered in the Phase 4 interview — what Angela actually uses day-to-day, and connector status for each.

| Tool | Use | Connector status |
|---|---|---|
| Gmail | Email | Registered as a claude.ai connector, shows "Connected" on the web, but its tools are not yet appearing inside this Claude Code (VSCode) session. See [[Open Items]]. |
| Google Calendar | Calendar | Same status as Gmail — connected on the web, not yet available here. See [[Open Items]]. |
| Phone notes app | Day-to-day planning/notes | No connector exists for a generic phone notes app. Best current path: capture into `_inbox.md` directly, or via the Telegram bridge (Phase 10) once built. |
| Canva | Design (thumbnails, graphics) | No official connector or well-maintained MCP server found. Later build if this becomes a bottleneck. |
| CapCut | Video editing | Mobile-only editing tool — no connector applicable. Not a candidate for automation right now. |
| Shopify | E-commerce platform | No connector pre-loaded in this session. Shopify has an official Admin API and community MCP servers exist — worth revisiting as a later build once the store is live (see [[Ventures/index|Ventures]], fleshed out in Phase 12). |
| File storage | Photos, docs, exported videos | Just phone/laptop — no cloud storage service in use, nothing to connect. |

## Later builds
- Gmail / Google Calendar: investigate why claude.ai connectors aren't surfacing as tools in Claude Code.
- Canva: no connector yet — revisit if manual design work becomes a time sink.
- Shopify: connect via Admin API/MCP once a store is actually live.
