# CLAUDE.md

## Who this vault belongs to

Angela — an aspiring entrepreneur building e-commerce and app ventures, and a content creator running **Ange.beee** on TikTok and Instagram. This vault (`C:\Users\Angela\Documents\Obsidian\Brain`) is her second brain: the single source of truth for both sides of her work.

**Golden rule:** whenever anything changes — a new venture, a new tool, a decision, a routine — this vault gets updated. If it isn't written down here, it didn't happen.

## The pillars

- **AI OS/** — the system itself: `Technology/` (tools, integrations, stack decisions), `Routines/` (recurring checklists), `Builds/` (things built, tradeoffs made), `Conversations/` (session summaries, via claude-mem)
- **Ventures/** — Angela's businesses. One subfolder per venture, named once the venture has a real name. `index.md` tracks the active list.
- **Content/** — Ange.beee creator work: `Ideas/`, `Posts/`, `Analytics/`, `Brand Deals/`, `Platforms/` (handles, platform-specific notes)
- **Investing/** — learning share investing/trading across ASX, TWSE, HKEX, and US markets: `Education/` (concepts, frameworks), `Markets/` (per-market reference), `Watchlist/` (tracked stocks, one note per ticker), `Journal/` (decisions + reasoning). Research/education/decision-support only — no automated trade execution.
- **Personal/** — personal life, empty until it grows organically
- **Reference/** — general knowledge base, empty until it grows organically

System folders (not synced to GitHub — see `.gitignore`): `_sources/` (raw inputs, scripts), `_memory/` (local-only memory artifacts), `_secrets/` (never used for actual secrets — those live in `C:\Users\Angela\.claude\secrets.env`, outside the vault entirely).

Root files: `index.md` (entry point), `Open Items.md` (active tasks/decisions), `log.md` (running activity log), `_inbox.md` (unsorted capture, including from the Telegram bridge).

## Wikilink conventions

- Link liberally with `[[Note Name]]` — Obsidian resolves by filename, so prefer unique note names over generic ones (`Ventures/index` not `index` when ambiguous)
- Link to folders' `index.md` when referring to a whole pillar (e.g. `[[Ventures/index|Ventures]]`)
- New notes should link back to at least one existing note (their parent index, a related idea) so nothing becomes an orphan

## Where things get filed

- A new business idea → `Ventures/<venture-name>/` (create the subfolder once it has a real name)
- A content idea → `Content/Ideas/`
- A published post's notes/performance → `Content/Posts/` and `Content/Analytics/`
- A brand deal → `Content/Brand Deals/`
- Platform handles, platform-specific notes → `Content/Platforms/`
- A new tool, integration, or stack decision → `AI OS/Technology/`
- A recurring checklist (like the weekly analytics review) → `AI OS/Routines/`
- A build decision or tradeoff (e.g. laptop vs. VPS for the Telegram bridge) → `AI OS/Builds/`
- A stock to track → `Investing/Watchlist/<TICKER>.md` (named exactly after its Yahoo Finance ticker, e.g. `BHP.AX.md`, so the daily market briefing picks it up automatically)
- An investing decision → `Investing/Journal/`
- Investing concepts/frameworks learned → `Investing/Education/`
- Anything captured on the fly (phone, Telegram, unsure where it goes) → `_inbox.md`, triaged later
- Open questions, pending decisions, active tasks → `Open Items.md`

## gbrain semantic search

This vault is indexed into a local gbrain brain for semantic search, so use it before falling back to plain file search when the question is conceptual ("what do I know about X") rather than a literal filename/string lookup.

- Local-only: PGLite database at `C:\Users\Angela\.gbrain\brain.pglite`, embeddings via local Ollama (`ollama:nomic-embed-text`, 768d) — nothing leaves this machine, no cloud embedding API.
- Registered as an MCP server at user scope (`gbrain serve`, stdio) — its tools should appear automatically once available in a session.
- Re-index after adding/editing notes: `gbrain import "C:\Users\Angela\Documents\Obsidian\Brain"`
- Search: `gbrain query "<question>"` or `gbrain search "<keywords>"`
- Health check: `gbrain doctor`
- Search mode is set to **conservative** (no paid LLM query expansion) to keep costs at $0 for normal use — see `gbrain config show` before changing this.
