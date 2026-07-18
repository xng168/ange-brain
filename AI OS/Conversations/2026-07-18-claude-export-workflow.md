# Claude.ai Export & Vault Integration Workflow

## Summary

Clarified how to integrate the claude.ai conversation export into the vault using a layered approach, with _sources/ as the archive location for raw data.

## Key Decisions

- **Export Location**: Store claude.ai export in `C:\Users\Angela\Documents\Obsidian\Brain\_sources\claude-export\` (as a subfolder, separate from existing automation scripts)
- **Migration Strategy**: Use layered approach — archive ALL raw conversations in _sources/ for backup, then curate only valuable threads (ventures, content, investing) into their proper pillars with wikilinks
- **Note Depth**: Keep full transcripts in the curated vault notes (not summaries alone)
- **Archive Protection**: _sources/ is already gitignored, so raw exports stay local and won't be pushed to GitHub

## Workflow

1. Trigger data export from claude.ai Settings → Account → Export data
2. Wait for download link via email
3. Download .zip file and place in `_sources/` or `_sources/claude-export/`
4. Run migration script to:
   - Extract and organize conversations
   - Curate valuable threads into Ventures, Content/Ideas, Investing pillars
   - Preserve full transcripts with wikilinks to related projects
   - Leave throw-away chats in raw archive

## Next Steps

- Await claude.ai export email
- Execute layered ingest workflow when export lands
- Link curated conversations to active venture specs (Mandarin Kids App, TCM App, Meridian)
